<< [README](./README.md)

# React
  - UI rendering library
  - Better DOM manipulation
	  - DOM - Document Object Model
![](Images/Pasted%20image%2020240725094042.png)
Before, we would have to directly manipulate the DOM. With React, we get to work with a virtual DOM, which helps manage some of that complexity.
  - Old way in JS:
```
document.getElementByTagName('h1').textContent = "hiiii"
const lstItem = document.createElement('li')
document.getElementByTagName('ol').appendChild(lstItem)
```
 - New way with React:

In React, **view is a function of state**.
- There are react states.
- When a value is changed, a state changes.
- However, when a state changes, the view doesn't.
- This is a one-way binding.

Single Page Application
 - Avoids page reloads
 - Dynamically swaps out content on the page
 - Not reloading an entire page and recreating the DOM each time

![](Images/Pasted%20image%2020240725095903.png)

## Notes
What is React?
 - It's a UI library
What is Vite?
 - It's a build tool for React
JSX
 - JavaScript and XML
	 - Lets us put markdown in our Javascript
	 - Gets transpiled back to javascript
![](Images/Pasted%20image%2020240725105038.png)
 - Transpiler munches on any filetype, as long as the contents are correct syntactically 
	 - Could be JSX, Typescript, etc.
	 - ==Our Transpiler is Babel==
Other Steps
- Minification
	- We want files to load fast
	- Minification removes whitespace and shortens var names to load less
Virtual DOM
 - More performant than working directly with the DOM
 - Simpler to work with - API makes working with the DOM easy
 - Rendering optimizations
	 - Can algorithmically find the minimum number of changes to be made to re-render the DOM
	 - Instead of letting the DOM do frequent reflows and repaints, it runs logic to decide when to do these - improving performance
 - Easier integration with State management
Named Exports
 - Can have as many as you want
Import Notation
- `import { whatever, whatever } from "./path/file`
Export Notation
 - `export const num = 42;`
Note: Use `StrictMode` only for development. It "mounts", "unmounts", and "mounts" each component again, which isn't great for performance, but is good for memory leaks.
 - It checks to see if there was a memory leak by mounting, checking to see if there was any remaining memory, and then re-mounting for functionality.
Using Images
 - You can either include them in the `public` or `src/assets` folders
 - Need to be imported, like `import logo from './logo.svg`

---

## Building our example project

### Getting started
 - We're *building* it with React, but we're using Vite to actually build the project - putting the code together.
![](Images/Pasted%20image%2020240725103034.png)

### Next Steps
We want to start building our code in modules that can be loaded through JSX into `index.html`. 
 - Note that we *don't want to touch `index.html`*, we want to build into `/src`.
```
ReactDOM.createRoot(document.getElementById('root')).render(
	<React.StrictMode>
		<App />
	</React.StrictMode>,
)
```
See `main.jsx`, above. It gets loaded by `index.html`, and then `main.jsx` inserts it's own dynamically-determinable structure into the website.

### Building
`npm run build`, unsurprisingly, builds the project.
 - Gets built into `/dist`
 Note that `npm run dev` is suitable for development/testing, while `npm run build` cleans (minifies) the project for serving to a client (when hosted on AWS, for example).

### Working in `App.jsx`
 - Note: Be careful, make sure you're using `function`, not `classes`, if following a tutorial!

