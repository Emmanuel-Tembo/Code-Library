# HOW TO CREATE A REACT APP
1. Check if u have node installed: node -v
2. Create the note react application using a build tool: npm install -g create-vite
3. once that is done create react application: npm create vite@latest [name of app] -- --template react
4. cd into app and npm install

# Markup and JS:
- using {} allows you to make use of Javascript within ur jsx markup, examples in avatar.jsx and DynamicAvatar.jsx 

# where to use curly braces:
1. As text directly inside a JSX tag: <h1>{name}'s To Do List</h1> works, but <{tag}>Gregorio Y. Zara's To Do List</{tag}> will not.

2. As attributes immediately following the = sign: src={avatar} will read the avatar variable, but src="{avatar}" will pass the string "{avatar}"

N.b to pass an object you must wrap it in another pair of curly braces:
 
person={{ name: "Hedy Lamarr", inventions: 5 }}

- NOTE: INLINE STYLE COMPONENTS ARE WRITTEN IN CamelCase E.J. :
- For example, HTML <ul style="background-color: black"> would be written as <ul style={{ backgroundColor: 'black' }}>  in your component.
