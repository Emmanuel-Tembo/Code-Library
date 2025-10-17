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

# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse

# Breakdown of `<Transition show={sidebarOpen} as={Fragment}>`

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.

# REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊

# PROP PASSING/ LIFTING STATE UP
1. if u want to affect more that one component use prop passing (Lifting state up):

- with this method u define state in the parent component-

```
:function App(){
	const [iscollapsed, setiscollapsed] =useState(false);

```
....rest of code

- what this dies is it sets up a state management for tehe parent component then to affect child componens give them "directives"

```
 <Navbar
	directive1: 
	isOpen={iscollapsed} you are telling the sidebar if it  should be open 
	directive2: 
	setOpen={setSideBarOpen} you are giving a command to the function toclose itself

...this gives the child compoonents access to the state?
/>
}
```
2. Finnaly we call the state directives in our child component to use as we please:

```
function NavBarLeft() {
	<div className:{`${isOpen ? w-[70px] : w-[400px]} bg-red-500`}>
		<button
			onClick={setOpen(false)}
		>
			close
		</button>
	</div>
}
```

n.b always mobile first.

1. fat
Dynamic ui styling:

use a Ternary Operator ( ? :) to choose padding classes:

```html
<div className={`flex h-screen flex-col ${sidebarOpen ? 'lg:pl-72' : 'lg:pl-20'}`}>
    {/* ... Main Content Area ... */}
</div>
```
e.g. a originally static sidebar:

```html
<div className="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col"> // Always 72 units wide
    {/* ... Sidebar component ... */}
</div>
```

now made dynamic:


<div className={`hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:flex-col 
                 ${sidebarOpen ? 'lg:w-72' : 'lg:w-20'}`}> 
``

# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse

# Breakdown of <Transition show={sidebarOpen} as={Fragment}>

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.

# REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊

# PROP PASSING/ LIFTING STATE UP
1. if u want to affect more that one component use prop passing (Lifting state up):

- with this method u define state in the parent component-
:function App(){
	const [iscollapsed, setiscollapsed] =useState(false);

....rest of code

> what this dies is it sets up a state management for tehe parent component then to affect child componens give them "directives"

 <Navbar
	directive1: 
	isOpen={iscollapsed} you are telling the sidebar if it  should be open 
	directive2: 
	setOpen={setSideBarOpen} you are giving a command to the function toclose itself

.... so does this give the child compoonents access to the state?
/>
}

2. Finnaly we call the state directives in our child component to use as we please:

function NavBarLeft() {
	<div className:{`${isOpen ? w-[70px] : w-[400px]} bg-red-500`}>
		<button
			onClick={setOpen(false)}
		>
			close
		</button>
	</div>
}

n.b always mobile first.
Dynamic ui styling:

use a Ternary Operator ( ? :) to choose padding classes:

<div className={`flex h-screen flex-col ${sidebarOpen ? 'lg:pl-72' : 'lg:pl-20'}`}>
    {/* ... Main Content Area ... */}
</div>

e.g. a originally static sidebar:

<div className="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col"> // Always 72 units wide
    {/* ... Sidebar component ... */}
</div>

now made dynamic:


<div className={`hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:flex-col 
                 ${sidebarOpen ? 'lg:w-72' : 'lg:w-20'}`}> 
``

# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse

# Breakdown of <Transition show={sidebarOpen} as={Fragment}>

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.

# REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊

# PROP PASSING/ LIFTING STATE UP
1. if u want to affect more that one component use prop passing (Lifting state up):

- with this method u define state in the parent component-
:function App(){
	const [iscollapsed, setiscollapsed] =useState(false);

....rest of code

> what this dies is it sets up a state management for tehe parent component then to affect child componens give them "directives"

 <Navbar
	directive1: 
	isOpen={iscollapsed} you are telling the sidebar if it  should be open 
	directive2: 
	setOpen={setSideBarOpen} you are giving a command to the function toclose itself

.... so does this give the child compoonents access to the state?
/>
}

2. Finnaly we call the state directives in our child component to use as we please:

function NavBarLeft() {
	<div className:{`${isOpen ? w-[70px] : w-[400px]} bg-red-500`}>
		<button
			onClick={setOpen(false)}
		>
			close
		</button>
	</div>
}

n.b always mobile first.
Dynamic ui styling:

use a Ternary Operator ( ? :) to choose padding classes:

<div className={`flex h-screen flex-col ${sidebarOpen ? 'lg:pl-72' : 'lg:pl-20'}`}>
    {/* ... Main Content Area ... */}
</div>

e.g. a originally static sidebar:

<div className="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col"> // Always 72 units wide
    {/* ... Sidebar component ... */}
</div>

now made dynamic:


<div className={`hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:flex-col 
                 ${sidebarOpen ? 'lg:w-72' : 'lg:w-20'}`}> 
``

# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse

# Breakdown of <Transition show={sidebarOpen} as={Fragment}>

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.

# REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊

# PROP PASSING/ LIFTING STATE UP
1. if u want to affect more that one component use prop passing (Lifting state up):

- with this method u define state in the parent component-
:function App(){
	const [iscollapsed, setiscollapsed] =useState(false);

....rest of code

> what this dies is it sets up a state management for tehe parent component then to affect child componens give them "directives"

 <Navbar
	directive1: 
	isOpen={iscollapsed} you are telling the sidebar if it  should be open 
	directive2: 
	setOpen={setSideBarOpen} you are giving a command to the function toclose itself

.... so does this give the child compoonents access to the state?
/>
}

2. Finnaly we call the state directives in our child component to use as we please:

function NavBarLeft() {
	<div className:{`${isOpen ? w-[70px] : w-[400px]} bg-red-500`}>
		<button
			onClick={setOpen(false)}
		>
			close
		</button>
	</div>
}

n.b always mobile first.
Dynamic ui styling:

use a Ternary Operator ( ? :) to choose padding classes:

<div className={`flex h-screen flex-col ${sidebarOpen ? 'lg:pl-72' : 'lg:pl-20'}`}>
    {/* ... Main Content Area ... */}
</div>

e.g. a originally static sidebar:

<div className="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col"> // Always 72 units wide
    {/* ... Sidebar component ... */}
</div>

now made dynamic:


<div className={`hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:flex-col 
                 ${sidebarOpen ? 'lg:w-72' : 'lg:w-20'}`}> 
``

# Ternery Operator: 
- condition ? valueIftrue : valueIfFalse

# Breakdown of <Transition show={sidebarOpen} as={Fragment}>

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.

# REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊

# PROP PASSING/ LIFTING STATE UP
1. if u want to affect more that one component use prop passing (Lifting state up):

- with this method u define state in the parent component-
:function App(){
	const [iscollapsed, setiscollapsed] =useState(false);

....rest of code

> what this dies is it sets up a state management for tehe parent component then to affect child componens give them "directives"

 <Navbar
	directive1: 
	isOpen={iscollapsed} you are telling the sidebar if it  should be open 
	directive2: 
	setOpen={setSideBarOpen} you are giving a command to the function toclose itself

.... so does this give the child compoonents access to the state?
/>
}

2. Finnaly we call the state directives in our child component to use as we please:

function NavBarLeft() {
	<div className:{`${isOpen ? w-[70px] : w-[400px]} bg-red-500`}>
		<button
			onClick={setOpen(false)}
		>
			close
		</button>
	</div>
}

n.b always mobile first.
    
# BACKEND, TYPESCRIPT AND EMAIL APIS THROUGH DESTRUCTURING

```typescript
    if (
      !confirmation.data?.data ||
      emailSent ||
      !confirmation.data.data.guestEmail
    )
    return;
```

1. This above snippet is a guard clause if any of the conditions:
- Condition 1 : check if teh confirmation data is missing null or undefined and the the optional chaining operator (?.) prevents a runtime crash if confirmastion.data is null
- condition 2: checks if emailSent is already true
- condition 3: 
