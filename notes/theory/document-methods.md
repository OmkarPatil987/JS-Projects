# JavaScript Document Object Methods and Tips

This notes page covers essential methods of the `document` object in JavaScript, which represents the DOM (Document Object Model) of the current web page. These allow you to select, manipulate, create, and interact with HTML elements dynamically. I'll include common methods, usage examples, tips, and best practices based on standard web development.

## Core Concepts
- The `document` object is the entry point to the DOM tree.
- It's part of the Browser Object Model (BOM) and always available in browser-based JS (not in Node.js without libraries like jsdom).
- Methods are synchronous unless specified (e.g., no async fetching here—use `fetch` for that).

## Selecting Elements
These methods help you grab existing elements from the page.

### `document.querySelector(selector)`
- Returns the **first** element matching a CSS selector.
- Example:
  ```js
  const header = document.querySelector('h1');  // Selects the first 
  header.textContent = 'Updated Title';
  ```
- Tip: Use for modern, flexible selection. Returns `null` if no match—always check with `if (header) { ... }`.

### `document.querySelectorAll(selector)`
- Returns a **NodeList** (array-like) of all matching elements.
- Example:
  ```js
  const images = document.querySelectorAll('.image');
  images.forEach(img => img.style.border = '1px solid red');
  ```
- Tip: NodeList isn't a true array—convert with `Array.from(images)` for methods like `map()` or `filter()`. It's live (updates automatically if DOM changes).

### `document.getElementById(id)`
- Returns the element with the specified `id`.
- Example:
  ```js
  const slider = document.getElementById('slider');
  slider.style.backgroundColor = 'blue';
  ```
- Tip: Faster than `querySelector` for IDs, but less flexible. Returns `null` if not found.

### `document.getElementsByClassName(className)`
- Returns a live **HTMLCollection** of elements with the class.
- Example:
  ```js
  const buttons = document.getElementsByClassName('button');
  ```
- Tip: Avoid if you need to add/remove classes dynamically, as the collection updates live.

### `document.getElementsByTagName(tagName)`
- Returns a live HTMLCollection by tag (e.g., 'div', 'img').
- Tip: Useful for bulk operations, like styling all images: `document.getElementsByTagName('img')`.

## Creating and Modifying Elements
Build new DOM nodes and insert them.

### `document.createElement(tagName)`
- Creates a new element node.
- Example:
  ```js
  const div = document.createElement('div');
  div.className = 'button';
  div.textContent = 'Click me';
  ```
- Tip: Combine with attributes: `div.setAttribute('data-index', 1)`.

### `element.appendChild(child)`
- Adds a child node to an element.
- Example:
  ```js
  const bottom = document.querySelector('.bottom');
  bottom.appendChild(div);  // Appends the new div
  ```
- Tip: Returns the appended child. For multiple, use loops or `append()` (which accepts multiple args and strings).

### `element.removeChild(child)`
- Removes a child node.
- Tip: Modern alternative: `child.remove()` (no parent needed).

### `element.insertBefore(newNode, referenceNode)`
- Inserts before a specific child.
- Tip: For more control, use `element.prepend()` or `element.after()` in modern browsers.

## Manipulating Styles and Attributes
- `element.style.property = value`: Inline styles, e.g., `slider.style.transform = 'translateX(-800px)'`.
  - Tip: Use camelCase for properties (e.g., `backgroundColor`, not `background-color`). For bulk, prefer adding classes via `classList.add('active')`.
- `element.setAttribute(name, value)` / `getAttribute(name)`: For any attribute.
  - Tip: Avoid for styles/classes—use `style` or `classList` instead.

## Event Handling
- `element.addEventListener(event, callback)`: Attaches events.
  - Example:
    ```js
    button.addEventListener('click', () => console.log('Clicked!'));
    ```
  - Tip: Use `'once': true` option for one-time listeners. Remove with `removeEventListener`.

## Other Useful Methods
- `document.createTextNode(text)`: Creates plain text nodes.
- `document.body` / `document.head`: Direct access to `` or ``.
- `document.readyState`: Checks if DOM is loaded ('loading', 'interactive', 'complete').
  - Tip: Wrap code in `document.addEventListener('DOMContentLoaded', () => { ... })` to run after DOM loads.
- `document.cookie`: Manage cookies (but use libraries for security).

## Tips and Best Practices
- **Performance**: `querySelectorAll` can be slow on large pages—cache results in variables.
- **Avoid inline styles**: Use CSS classes for separation of concerns.
- **Error handling**: Always null-check: `if (!element) return;`.
- **Modern alternatives**: For complex apps, use frameworks like React (virtual DOM) instead of direct manipulation.
- **Security**: Sanitize inputs to prevent XSS when setting `innerHTML`.
- **Debugging**: Use `console.dir(element)` to inspect properties.
- **Accessibility**: Add ARIA attributes via `setAttribute` for better screen-reader support.
- **Common pitfall**: DOM methods don't work until the page loads—defer scripts or use 'DOMContentLoaded'.

## Example: Simple Slider Snippet (from previous notes)
```js
const buttons = document.querySelectorAll('.button');
buttons.forEach((btn, i) => {
  btn.addEventListener('click', () => {
    // Reset and transform using document methods
  });
});
```
