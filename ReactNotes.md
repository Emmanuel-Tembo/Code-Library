### HOW TO CREATE A REACT APP
1. Check if u have node installed: node -v
2. Create the note react application using a build tool: npm install -g create-vite
3. once that is done create react application: npm create vite@latest [name of app] -- --template react
4. cd into app and npm install

## Markup and JS:
- using {} allows you to make use of Javascript within ur jsx markup, examples in avatar.jsx and DynamicAvatar.jsx 

## where to use curly braces:

1. As text directly inside a JSX tag: `<h2>{name}'s To Do List</h2>` works, but <{tag}>Gregorio Y. Zara's To Do List</{tag}> will not.

2. As attributes immediately following the = sign: src={avatar} will read the avatar variable, but src="{avatar}" will pass the string "{avatar}"

N.b to pass an object you must wrap it in another pair of curly braces:
 
person={{ name: "Hedy Lamarr", inventions: 5 }}

- NOTE: INLINE STYLE COMPONENTS ARE WRITTEN IN CamelCase E.J. :
- For example, HTML <ul style="background-color: black"> would be written as <ul style={{ backgroundColor: 'black' }}>  in your component.


## REACT STATE UI STATE MANAGEMENT: 

1. use state to manage components for live rendering.
2. u can call it to interactively render children in the component and even conditionally render styles with a little JavaScript and tailwind 👌😊



## PROP PASSING/ LIFTING STATE UP
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


## Breakdown of `<Transition show={sidebarOpen} as={Fragment}`>

1. The component Transition: used to manage the lifecycle of its child component:
- When the show proop changes from false to true the transition component applies the appropriate animmation classes like: opacity-0;

2. The Condition: show={sidebarOpen}: This prop dictates whether the child content should be visible:
- {sidebaropen} comes from the react state
- if sidebaropen is true the sidebar willopen if not fakse it will exit the view

3. The wrapper: as={Fragment} 
- as: this Proptellsreact what kindof HTMLelement or react component it should render or rapits children
- Fragment : used when u need to add a wrapper but don't want to add an extra div
- By using as={Fragment}, you ensure that the Transition component wraps its logic around the sidebar without polluting your final HTML structure with unnecessary container tags. This keeps your structure clean, especially when working with strict CSS layouts like Flexbox or Grid.
