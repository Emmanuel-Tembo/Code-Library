# Pundit Authorization in Rails

## What is Pundit?
Pundit is a **authorization gem** that provides a clean way to define who can do what in your Rails application.

## Core Concept
```ruby
# Every authorization check answers:
"Can [user] perform [action] on [resource]?"

# Translated to code:
authorize(user, resource)  # Checks: PolicyClass#action?(user, resource)
```

# Basic Usage Patterns

## 1. Default Convention (Most Common)

```ruby
# Controller action
def show
  @folder = Folder.find(params[:id])
  authorize @folder  # Automatically calls FolderPolicy#show?
end

# What happens:
# 1. Infers policy: FoldersController → FolderPolicy
# 2. Infers action: show → show?
# 3. Passes: current_user and @folder to policy
```

## 2. Authorizing a Class (for Collection Actions)
```ruby
def index
  authorize Folder  # Calls FolderPolicy#index?
  @folders = Folder.all
end
```

## 3. Custom Action Names
```ruby
def archive
  @document = Document.find(params[:id])
  authorize @document, :update?  # Use existing policy method
  # OR
  authorize @document, :archive?  # Needs DocumentPolicy#archive?
end
```

## 4. Explicit Policy Specification
```ruby
def tree
  authorize current_account, policy_class: FolderPolicy
  # Uses FolderPolicy with current_account as user
  # Calls FolderPolicy.new(current_account, nil).tree?
end
```

# Policy Files Structure


## Basic Policy Template

```ruby
# app/policies/folder_policy.rb
class FolderPolicy < ApplicationPolicy
  attr_reader :user, :record

  def initialize(user, record)
    @user = user     # current_user
    @record = record # The resource (instance or class)
  end

  # Standard RESTful actions
  def index?
    user.present?  # Any logged-in user
  end

  def show?
    # User can only see folders from their account
    record.account_id == user.account_id
  end

  def create?
    user.admin? || user.manager?
  end

  def update?
    show? && (user.admin? || record.owner_id == user.id)
  end

  def destroy?
    user.admin? || (record.owner_id == user.id && record.empty?)
  end

  # Custom actions
  def tree?
    user.present?  # Any logged-in user can see tree
  end

  def contents?
    show?  # Same permission as show
  end

  # Scope for filtering collections
  class Scope
    attr_reader :user, :scope

    def initialize(user, scope)
      @user = user
      @scope = scope
    end

    def resolve
      if user.admin?
        scope.all
      else
        scope.where(account_id: user.account_id)
      end
    end
  end
end
```

# Policy Scopes

## Using Scopes in Controllers

```ruby
def index
  authorize Folder
  @folders = policy_scope(Folder)  # Automatically filtered by policy
  # Shows only folders user is allowed to see
end
```

## Scope Inheritance

```ruby
# app/policies/application_policy.rb
class ApplicationPolicy
  class Scope
    def initialize(user, scope)
      @user = user
      @scope = scope
    end

    def resolve
      scope.all  # Default: show everything (override in subclasses!)
    end
  end
end
```

# Common Authorization Patterns

## 1. Role-Based Authorization

```ruby
class DocumentPolicy < ApplicationPolicy
  def show?
    case user.role
    when 'admin'
      true
    when 'editor'
      record.department == user.department
    when 'viewer'
      record.public? || record.viewers.include?(user)
    else
      false
    end
  end
end
```

## 2. Ownership-Based Authorization

```ruby
class FolderPolicy < ApplicationPolicy
  def update?
    # Owners can update
    record.owner_id == user.id ||
    # Shared editors can update
    record.editors.include?(user) ||
    # Admins can update anything
    user.admin?
  end
end
```

## 3. Time-Based Authorization

```ruby
class ReportPolicy < ApplicationPolicy
  def download?
    # Can only download reports during business hours
    Time.current.hour.between?(9, 17) &&
    # And user has correct role
    user.finance_role?
  end
end
```

# View Helpers

## Checking Authorization in Views\

```erb
<% if policy(@folder).edit? %>
  <%= link_to "Edit", edit_folder_path(@folder) %>
<% end %>

<% if policy(Folder).create? %>
  <%= link_to "New Folder", new_folder_path %>
<% end %>

<!-- With scopes -->
<% policy_scope(@user.folders).each do |folder| %>
  <!-- Only shows folders user can see -->
  <%= folder.name %>
<% end %>
```

# Error Handling

## Custom Error Responses

```ruby
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  include Pundit::Authorization
  
  rescue_from Pundit::NotAuthorizedError, with: :user_not_authorized

  private

  def user_not_authorized(exception)
    policy_name = exception.policy.class.to_s.underscore
    
    render json: {
      error: "Not authorized to #{exception.query} this #{policy_name}"
    }, status: :forbidden
  end
end
```

# Skip Authorization When Needed

```ruby
class PublicController < ApplicationController
  skip_after_action :verify_authorized  # No auth needed
  
  def public_data
    # Publicly accessible
  end
end
```

# Testing Authorization

## Controller Tests

```ruby
RSpec.describe FoldersController do
  describe "GET #show" do
    it "denies access to other account's folders" do
      folder = create(:folder, account: other_account)
      
      get :show, params: { id: folder.id }
      
      expect(response).to have_http_status(:forbidden)
    end
    
    it "allows access to own folders" do
      folder = create(:folder, account: current_account)
      
      get :show, params: { id: folder.id }
      
      expect(response).to be_successful
    end
  end
end
```

## Policy Tests

```ruby
RSpec.describe FolderPolicy do
  let(:user) { create(:user) }
  let(:folder) { create(:folder, account: user.account) }
  
  describe "#show?" do
    it "allows user to see folders from their account" do
      expect(policy(user, folder).show?).to be true
    end
    
    it "denies user from seeing other account's folders" do
      other_folder = create(:folder, account: create(:account))
      expect(policy(user, other_folder).show?).to be false
    end
  end
end
```

# Common Pitfalls & Solutions

## 1. Forgetting to Create Policy Files

```bash
# Generate policy files automatically
rails generate pundit:policy folder
rails generate pundit:policy document
```

## 2. Default Policy is Too Permissive

```ruby
# BAD: ApplicationPolicy defaults (dangerous!)
def show?
  scope.where(id: record.id).exists?  # Allows access if record exists!
end

# GOOD: Explicitly deny by default
class ApplicationPolicy
  def initialize(user, record)
    raise Pundit::NotAuthorizedError unless user
    
    @user = user
    @record = record
  end
  
  def show?
    false  # Deny by default, override in subclasses
  end
end
```

## 3. Not Using Scopes for Collections

```ruby
# BAD: Shows all records then filters in view
def index
  @folders = Folder.all  # Loads ALL folders
  # Then need to filter in view with policy checks
end

# GOOD: Use policy_scope
def index
  @folders = policy_scope(Folder)  # Only loads permitted folders
end
```

## 4. Overcomplicating Policy Logic

```ruby
# BAD: Complex logic in policy
def update?
  if user.admin?
    true
  elsif user.manager? && record.department == user.department
    if record.created_at > 1.week.ago
      user.permissions.include?(:edit_recent)
    else
      false
    end
  # ... more nested conditions
end

# GOOD: Extract to methods
def update?
  admin? || manager_in_same_department? || owner?
end

private

def manager_in_same_department?
  user.manager? && record.department == user.department
end
```
# Installation & Setup

## 1. Add to Gemfile

```ruby
gem 'pundit'
```

## 2. Install and Generate

```bash
bundle install
rails generate pundit:install
```

## 3. Configure ApplicationController

```ruby
# app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  include Pundit::Authorization
  
  # Optional: customize the user method
  def pundit_user
    current_account  # or current_user
  end
  
  # Verify authorization in all actions
  after_action :verify_authorized, except: :index
  after_action :verify_policy_scoped, only: :index
end
```