# Rails API Development Patterns

## The MVC Triad for APIs


### Key Differences from Traditional Rails
- **No views** (render JSON directly in controllers)
- **No `new`/`edit` actions** (no HTML forms)
- **Focus on JSON serialization**

## API Controller Pattern

### Basic CRUD Template

```ruby
class Api::V1::FoldersController < ApplicationController
  before_action :set_folder, only: %i[show update destroy]
  
  # GET /api/v1/folders
  def index
    @folders = Folder.all
    render json: @folders
  end
  
  # GET /api/v1/folders/:id
  def show
    render json: @folder
  end
  
  # POST /api/v1/folders
  def create
    @folder = Folder.new(folder_params)
    
    if @folder.save
      render json: @folder, status: :created
    else
      render json: { errors: @folder.errors }, status: :unprocessable_entity
    end
  end
  
  # PATCH/PUT /api/v1/folders/:id
  def update
    if @folder.update(folder_params)
      render json: @folder
    else
      render json: { errors: @folder.errors }, status: :unprocessable_entity
    end
  end
  
  # DELETE /api/v1/folders/:id
  def destroy
    @folder.destroy
    head :no_content
  end
  
  private
  
  def set_folder
    @folder = Folder.find(params[:id])
  end
  
  def folder_params
    params.require(:folder).permit(:name, :parent_id, :position)
  end
end
```