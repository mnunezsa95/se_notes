See [[React - Introduction to React.js]]

---

#### What is the Virtual DOM
* The Virtual DOM is a lightweight, in-memory, and virtual representation of the actual Document Object Model (DOM), which is the structured representation of a web page
*  React uses this representation to keep track of the components and their rendering.

#### Why is the virtual DOM needed?
* **Efficiency**: 
	* Manipulating the real DOM is relatively slow, especially when making frequent updates.
	* The Virtual DOM acts as a buffer, allowing React to make changes to the virtual tree efficiently. 
* **Consistency**: 
	* The Virtual DOM ensures a consistent view of the UI, making it easier to reason about how the UI should look at any given time

#### Creation and Representation of the Virtual DOM
* When a component renders, React creates a new Virtual DOM tree that represents the current state of the UI.
* Process
	* Initial Render: React creates a Virtual DOM tree that mirrors the component's structure and content
	* Subsequent Renders: When a component’s state or props change, React creates a new Virtual DOM tree to represent the updated UI.

#### Updating the Virtual DOM
1) React detects a change in the component's state or props
2) React re-renders the component (creating a new Virtual DOM)
3) React compares the new Virtual DOM to the previous Virtual DOM (diffing stage)
4) React identifies the differences (or diffs) between the new VDOM and previous VDOM

Allows React to only re-render what is necessary in the real DOM


#### Where is the Virtual DOM Stored?
* The Virtual DOM is stored in memory of the web browser (as a JavaScript Object)
* It is NOT a visible part of the application (rather an internal data structure)


#### Benefits of the Virtual DOM
1) Performance Optimization -> less edits to the real slower DOM
2) Consistency -> Ensures consistent view of the UI
3) Efficiency -> Only involves elements that have changed (reduces unnecessary re-renders)