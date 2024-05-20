* An HTML format that JavaScript can understand
* Created by the DOM (see [[JS - What is the DOM Tree?]])
# How to access the DOM tree
* The DOM tree can be accessed by opening up the “Elements” tab in the developer tools of the browser

# Understanding the DOM Tree
* Each DOM tree branch ends in a node. There are four types of nodes (see [[JS - The DOM Behind the Scenes]])
	* Element Nodes
	* Text Nodes
	* Comment Nodes
	* Document Nodes
- All elements are nodes, but not all nodes are elements.
- The Document, Element, Comment and Text Nodes can be accessed and manipulated using specific methods (see [[JS - DOM Methods & Properties]])

**![A DOM tree with all of its nodes.](https://lh3.googleusercontent.com/8uvbdHhIOmQR6p-FLhhJhvm18OjIVE0CgCjOTVQ_Y3PEGhJ8783TOIbjQhl840drVOi1jL6OgV9QrF1AtT1TgiuIFn6iUxfliWAt9TuwKKPEIWS5y_xKDtoPbahHuI8X8UBhAVjWB1_IiaPnFq-MHZ4)**

**![](https://lh5.googleusercontent.com/MbZuOrrogE2cGoxWGSRJY2ImHgjuGQzK3HvkjhWKpB1nW-TektWSWWirdg8NfU3GZunZQnzxnZEU-yePGfnxhxuJ4Hcguiin-LcQ3nmoM6ndfW_fJ1k0yS-kuThDDmbmCzFf-74m5tIhBX6z3Il2B34)**

**![A DOM tree with all the text nodes (such as link to body, link to footer, heading, etc.) highlighted in blue.](https://lh4.googleusercontent.com/WR8V172CJ_Wng-P4slQH9KYBUpm0zA0opY5s0Bs1IPIEAyFGueeoy9MjpZt75pTdG_e2OTpc10LV2bCK_VFEoIZuFinKlXdobyD1QB3yt5qh48zyr3TB0vG4xTjxY4FPq2JtGezkMoKKY0AqyJiJu_M)**

**![A DOM tree with a comment node that reads "< - - - link to practicum - - - >" highlighted yellow.](https://lh6.googleusercontent.com/kzohYQmGvt6MAIBT__LjiKi6VYBdxsxNDVHWP0-YDaewbnIZNi3e1Duf6v_4XVDjTMfxii3Qb7rF1Nnev1aoj3ya-MC2ccJoBW1Ez0cndn5b0Bs94-rg0e-hE6gCGu29ROfXMbOp5h0ZtvmgRJlLXGY)**

### How the DOM looks in the browser
*****Using the Example above!

```html
<html>
  <head>
  </head>
  <body>
    <nav>
      <a>link to body</a>
      <a>link to footer</a>
    </nav>
    <main>
      <div></div>
      <h1>heading</h1>
      <div>
        <h2>subheading</h2>
        <p>text</p>
        <p></p>
        <p>paragraph text</p>
      </div>
      <p>paragraph text</p>
    </main>
    <footer>
      copyright
      <a>
        practicum.com
        <!-- link to practicum -->
      </a>
      <a>linkedin.com</a>
    </footer>
  </body>
</html>
```