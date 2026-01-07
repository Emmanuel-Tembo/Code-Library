# Rails Getting Started

## Installation & Setup
1. Install Ruby: `rbenv install 3.2.0`
2. Install Rails: `gem install rails`
3. Create new app: `rails new myapp`
4. Start server: `rails server`

## Rails Commands Cheat Sheet
```bash
# Generators
rails generate model User name:string email:string
rails generate controller Users index show
rails generate migration AddColumnToTable

# Database
rails db:create
rails db:migrate
rails db:seed

# Console
rails console  # Interactive Ruby console
rails test     # Run tests