# Dynamic ui styling:

use a Ternary Operator ( ? :) to choose padding classes:

```
<div className={`flex h-screen flex-col ${sidebarOpen ? 'lg:pl-72' : 'lg:pl-20'}`}>
    {/* ... Main Content Area ... */}
</div>
```
e.g. a originally static sidebar:

````
<div className="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col"> // Always 72 units wide
    {/* ... Sidebar component ... */}
</div>
````

now made dynamic:

```
<div className={`hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:flex-col 
                 ${sidebarOpen ? 'lg:w-72' : 'lg:w-20'}`}> 
```
