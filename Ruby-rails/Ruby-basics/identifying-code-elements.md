# Identifying Code Elements in Ruby/Rails

## The Big Picture
When reading Ruby/Rails code, everything falls into these categories:
1. **Ruby Core** - Built into Ruby language
2. **Rails Framework** - Provided by Rails
3. **Your Code** - What you write
4. **Gem Code** - From installed gems

---

## Quick Identification Guide

### If you see... → It's...

```ruby

.method_name # Ruby/Rails built-in method
Class.method # Class method (could be yours or Rails)
variable = # Your local variable
@variable # Your instance variable
if/else/end # Ruby control flow
{} or [] # Ruby data literals
params, render # Rails controller methods
Model.where, .order # ActiveRecord queries
:method_name(&:sym) # Ruby symbol-to-proc
method_name(args) # Your custom method (no dot)

```


---

## Category 1: Ruby Core (Always Available)

### Control Flow & Keywords
```ruby
if condition
elsif condition  
else
end

case value
when condition
else
end

nil
true
false
self
```

# Data literals 

```ruby
{}                    # Empty hash
{ key: "value" }      # Hash with data
[]                    # Empty array  
[1, 2, 3]             # Array with data
"string"              # String literal
:symbol               # Symbol literal
1, 3.14               # Number literals
```

### Array/Hash Methods (Called on collections)

```ruby
# Array methods
array.map { |x| ... }     # Transform each element
array.select { |x| ... }  # Filter elements
array.find { |x| ... }    # Find first match
array.sort                # Sort elements
array.first               # Get first element
array.last                # Get last element
array.length              # Get size
array.empty?              # Check if empty
array.any?                # Check if any match
array.all?                # Check if all match
array.group_by { |x| ... } # Group by criteria

# Hash methods
hash[:key]                # Access value
hash.keys                 # Get all keys
hash.values               # Get all values
hash.merge(other_hash)    # Combine hashes
```

# Symbol-to-Proc Shorthand

```ruby
# These are equivalent:
array.map(&:name)            # Ruby shorthand
array.map { |x| x.name }     # Full block syntax

# Other examples:
users.select(&:active?)      # => users.select { |u| u.active? }
folders.group_by(&:parent_id) # => folders.group_by { |f| f.parent_id }
```

# Category 2: Rails Framework Methods

## ActiveRecord Query Methods

```ruby
# Called on models/relations
Model.where(condition)      # Filter records
Model.order(:column)        # Sort results  
Model.limit(10)             # Limit results
Model.offset(5)             # Skip records
Model.includes(:association) # Eager loading (prevents N+1)
Model.joins(:association)   # SQL JOIN
Model.pluck(:column)        # Get specific column values
Model.select(:col1, :col2)  # Select specific columns
Model.group(:column)        # GROUP BY
Model.having("count > 1")   # HAVING clause
Model.distinct              # Unique results
Model.count                 # Count records
Model.average(:column)      # Calculate average
Model.sum(:column)          # Calculate sum

# These return ActiveRecord Relations (chainable)
Folder.where(active: true).order(:name).limit(10)
```

## Model Class Methods

```ruby
Model.all                   # All records (returns Relation)
Model.find(id)              # Find by ID (raises error if not found)
Model.find_by(attr: value)  # Find by attribute (returns nil if not found)
Model.first                 # First record
Model.last                  # Last record
Model.new(attributes)       # Create new instance (not saved)
Model.create(attributes)    # Create and save
Model.update(id, attributes) # Update record
Model.destroy(id)           # Delete record
```

## Controller Methods

```ruby
# Available in all controllers
params                      # Request parameters (hash)
render                      # Send response
redirect_to(path)           # Redirect to another action
head(:status)               # Send HTTP header only
respond_to                  # Format-based responses
before_action               # Run code before actions
after_action                # Run code after actions
around_action               # Wrap actions with code

# Session & Cookies
session[:key] = value       # Session storage
cookies[:key] = value       # Cookie storage
flash[:notice] = "Message"  # Flash messages

# Request info
request.method              # HTTP method (GET, POST, etc.)
request.path                # Request path
request.headers             # HTTP headers
```

## Rails Type System

```ruby
# Type casting/conversion
ActiveModel::Type::Boolean.new.cast(value)
# Converts: "true", "false", "1", "0", true, false

# Other type casters
ActiveModel::Type::Integer.new.cast("42")   # => 42
ActiveModel::Type::Date.new.cast("2024-01-20") # => Date object
```

# Category 3: YOUR Code (What You Write)

## Local Variables (In Methods)

```ruby
def some_action
  # These are YOUR local variables:
  folders = Folder.all          # 'folders' is yours
  by_parent = {}                # 'by_parent' is yours
  include_docs = true           # 'include_docs' is yours
  
  # They only exist in this method
  # Start with lowercase letter
  # Created with = assignment
end
```

## Instance Variables & Methods

```ruby
class FoldersController < ApplicationController
  # Instance variables (yours, shared across methods)
  def show
    @folder = Folder.find(params[:id])  # @folder is yours
    @documents = @folder.documents      # @documents is yours
  end
  
  # Instance methods (yours)
  def current_account
    @current_account ||= Account.find(session[:account_id])
  end
  
  # Helper methods (become available in views too)
  helper_method :current_account
end
```

## Model Scopes & Class Methods

```ruby
class Folder < ApplicationRecord
  # These are YOUR scopes/class methods:
  scope :for_account, ->(account) { where(account_id: account.id) }
  scope :recent, -> { where("created_at > ?", 1.week.ago) }
  
  def self.by_name(name)
    where("name ILIKE ?", "%#{name}%")
  end
  
  def self.tree_structure
    # Your custom class method
  end
end
```

## Custom Helper Methods

```ruby
# In controllers or helpers
def build_tree(folders_by_parent, parent_id: nil)
  # YOUR custom method
  # Not called on an object (no dot)
  # You defined this somewhere
end

def format_date(date)
  # YOUR helper method
  date.strftime("%B %d, %Y")
end
```

# Category 4: Gem Methods (From Installed Gems)

## Common Gem Patterns

```ruby
# Pundit (authorization)
authorize @record            # From 'pundit' gem
policy_scope(Model)          # From 'pundit' gem

# Devise (authentication)
user_signed_in?              # From 'devise' gem
current_user                 # From 'devise' gem (if you use it)

# Kaminari (pagination)
Model.page(1).per(10)        # From 'kaminari' gem

# Ransack (search)
@q = Model.ransack(params[:q]) # From 'ransack' gem
```

### How to Identify Gem Methods

1. Check your Gemfile
2. Look for gem-specific patterns
3. Methods often match gem names (authorize → pundit)

# Identification Flowchart

```text
Is it a Ruby keyword? (if/else/end/nil)
    → Yes: Ruby Core
    
Is it a data literal? ({}/[]/":symbol")
    → Yes: Ruby Core
    
Does it start with a dot? (.method)
    → Yes: Ruby/Rails method on object
    
Is it Class.method?
    → Check: Common Rails? (Model.where) → Rails
    → Otherwise: Could be your class method
    
Is it variable = ?
    → Yes: Your local variable
    
Is it @variable?
    → Yes: Your instance variable
    
Is it method(args) with no dot?
    → Yes: Your custom method
    
Is it params/render/redirect_to?
    → Yes: Rails controller method
```