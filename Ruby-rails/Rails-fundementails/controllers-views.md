# Understanding form_with in Rails

form_with is a Rails helper that generates HTML forms. The syntax variations depend on whether you're creating a form for a model (Active Record object) or a generic form.

## Key Concept: Model-backed vs Non-model Forms

Rails forms can either:

1. Be *tied to a model* (for CRUD operations)
2. Be *standalone forms* (for actions not directly tied to a model)

### Example 1: Non-Model Form (URL only)

```ruby

<%= form_with url: sign_in_path do |form| %>
  <%= form.text_field :email %>
  <%= form.password_field :password %>
  <%= form.submit "Sign In" %>
<% end %>
```
- Used for actions that do not create/ update a specific model
- HTML Result: <form action="/sign_in" method="post">
- These are for the basic form to controller actions, so simple post interactions

### Example 2: Model-Backed Form (with URL override)

```ruby
<%= form_with model: @user, url: sign_up_path do |form| %>
  <%= form.text_field :name %>
  <%= form.email_field :email %>
  <%= form.submit "Create Account" %>
<% end %>
```

*Why this combination?*


