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