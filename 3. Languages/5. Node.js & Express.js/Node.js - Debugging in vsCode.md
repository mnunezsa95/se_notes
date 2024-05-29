See: [[Node - Introduction to Node.js]]
Documentation: 
* [Node.js Documentation - Debugger](https://nodejs.org/api/debugger.html)

---

How to debug Node.js programs?
* 3 Ways
	1) In the Terminal (see [[Node.js - Debugging in Terminal]])
	2) In the browser (requires additional setup)
	3) In vsCode 

### How to start the debugger in vsCode
1) Set a breakpoint (clicking in the gutter to the left of the number-line)
2) Click the debug icon in the NPM scripts section (below the file browser)
	* Only works if there is package.json file w/ a script to launch app
**![](https://lh5.googleusercontent.com/SlG6uhmXrHSk28mbs9dGDFlbHsZcr9EDp3MPjSXEGxErm4h2kaGWnwiU9WMnpBy-g-1a5UyltQ_m4z4EGfOPJjEIdHSva2_rMPVeB7q8s5RbhHqmDRDtqhxIAE-WJ1nZnpDUnQmn7YADuu51QUSFtfc)**
3) Confirm that a yellow outlined  around the breakpoint & a highlighted line appeared
**![](https://lh4.googleusercontent.com/aLIAPVW6THdkw7hvKROG2aPaQPrPUWupAHo8i_q8vGtCXFiZ5DzBZTENnSZYocADEvA51TlwtZZHiKRY4s0vDudtx-Asc8lgWapiQMliGO6-JljywlfoIil2uH1D2y4V1cCyIcvRpl4shptfP9uXG0I)**

### How to use the debugger in vsCode
* When debugger is paused, the state of variables appear on the left panel
**![](https://lh5.googleusercontent.com/BRhi1JNuPkag1PMq0ZhghxZrrBVahBwcHOiKIzo7P9j4tUThyX_9zXm6wEWMaYPCJYYnjXP5QRQsy0uVI7cJdLcYvLlnijgbBD1mrqopuQAByD3Q7BP4dglN8XhIrQ_KA3KmTXHqIf__h45s_XtWnAM)**
* Expressions can be evaluated by entering them into into the debug console (at the bottom) and pressing enter
**![](https://lh3.googleusercontent.com/wA27UGDT9AVK8H7MfNMVlTAjutwFHHZNxqNsxWlelEsdN3N1yvf93J4o3WlHbUERtLdlO6KnZojSl3nqt-fi4W5Jyf85iv8IUe2jWbHXGl7NA8Q45k_rOQHnTtVFwszwztkVicZuet2PTH5XjBldR6Y)**

### Commands for Moving in the code - Debug Mode
**![](https://lh3.googleusercontent.com/h1NN70KXdj9B5IXWknONibDs0Pi_JF4612Rn1zZ7CS6YkSQv9EzKBhZJq4pKJOizeA0g60LvoogPtMOL6C_HTzKpVCOuA9bRy4lyUjTx2ipcxFKigDx3fIg6tUESFcEQQyYeRhRmkcTx20GtAc0BjJA)**

