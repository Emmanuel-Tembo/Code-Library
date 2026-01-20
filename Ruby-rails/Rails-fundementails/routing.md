# Rails Routing Deep Dive

## Resourceful Routing vs Simple Routes

### Resourceful Routing (`resources`)
Use for CRUD operations on resources:
```ruby
resources :folders, only: %i[index show create update destroy]

# Creates these RESTful routes:

# GET /folders → folders#index

# GET /folders/:id → folders#show

# POST /folders → folders#create

# PATCH/PUT /folders/:id → folders#update

# DELETE /folders/:id → folders#destroy
```


## Custom Actions within Resources

### Collection Routes (no ID)

```ruby
resources :folders do
  collection do
    get :search      # GET /folders/search
    post :bulk_delete # POST /folders/bulk_delete
  end
end
```

### Member Routes (requires ID)

```ruby
resources :folders do
  member do
    get :preview     # GET /folders/:id/preview
    post :duplicate  # POST /folders/:id/duplicate
  end
end
```

## Simple Routes (Non-RESTful)

```ruby
post "/login", to: "sessions#create"
delete "/logout", to: "sessions#destroy"
Use for one-off actions that don't fit CRUD patterns.
```

## Route Options

### Limiting Routes

```ruby
# Include only specific actions
resources :folders, only: %i[index show create]

# Exclude specific actions  
resources :folders, except: %i[new edit]

# Ruby symbol array shorthand
%i[index show]  # Same as [:index, :show]
```

### Namespacing

```ruby
namespace :api do
  namespace :v1 do
    resources :folders
  end
end

# Creates: /api/v1/folders
```

### Shallow Nesting
```ruby
resources :projects, shallow: true do
  resources :tasks
end

# GET /projects/:project_id/tasks (only for collection)
# GET /tasks/:id (shallow for member routes)
```

### Route Helpers
```ruby
folders_path           # /folders
new_folder_path        # /folders/new  
edit_folder_path(@folder)  # /folders/:id/edit
folder_path(@folder)   # /folders/:id
```

### Checking Routes
```bash
# See all routes
rails routes

# Filter routes
rails routes | grep folder
```