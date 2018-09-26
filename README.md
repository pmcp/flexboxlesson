# Experiment: Flexbox

## Introduction

Use of CSS frameworks like Bootstrap and Foundation is easy and quick, but sometimes there are reasons to not use a framework. You might have a very simple website, and a framework might overdue it, or you have a very specific layout in mind, that would need a lot of tweaking of the base code of the framework.

In a world full of different devices, it’s important to create a responsive design. In the beginning, html was not handy to create really nice layouts. When i started building websites, we heavily used the frame tag and the table tag. Both have it's merits, but there are some new modules that will help us create a bit more of a flexible layout.

The two most promising layout modules are [**Grid**](https://caniuse.com/#feat=css-grid) and [**Flexbox**](https://caniuse.com/#feat=flexbox).

The difference between grid and flexbox can be a bit confusing. Some feel that Grid is the successor to Flexbox, but this is not true. Although you can pretty much end up with the same layouts using one or the other, they each have their use cases where they shine the most.

Generally speaking the easiest rule to follow is:

- If you are building a layout that has two dimensions, columns and rows, go for Grid.
- If you are building a layout that has one dimension, go for Flexbox, this will give you a bit more flexibility.

You can also combine Grid and Flexbox. You can for example create a full layout with Grid, and inside create some elements with Flexbox. Such an element is for example a menu bar.

## Exercise: creating a responsive menu component with css Flexbox

### Step 1: The base code
We will start with a basic html page. For the convenience of this experiment, we'll keep the css in the same file.

As you can see, we have a div, that has three child divs. These are the main buttons of our menu. As they have no specific css mark up, they will just appear beneath each other.

```
<html>

<head>
  <style>
  </style>
</head>

<body>

  <div>
		<div>Home</div>
		<div>The Team</div>
		<div>Contact</div>
		<div>Search</div>
  </div>
  
</body>

</html>
```

To really see what we are doing, we'll add some colours, so once we start to play around with flex box, we'll see what exactly happens with what element. You can also check the lay out out in Web Inspector, but this is just a bit more visual.

Go ahead and add a border width and border colour to the divs and background colours to the children divs. You can do it inline or in the CSS in the head tag.

    div {
      border: 1px solid #6638F0;
    }
    
    div > div {
      background-color: #5CC9F5;
    }

### Step 2: Making it flex

Now, we are going to make these divs behave in a more flexible way by adding Flex Box markup.

To keep the overview, let's give the parent div a class, called "container". And we'll add the markup ```display: flex;```. So now we end up with:

```
<html>

<head>
  <style>
   
    div {
      border: 1px solid #6638F0;
    }
    
    div > div {
      background-color: #5CC9F5;
    }

    .container {
      display: flex;
    }
    
  </style>
</head>

<body>

  <div>
		<div>Home</div>
		<div>Team</div>
		<div>Contact</div>
		<div>Search</div>
  </div>
  
</body>

</html>
```

We know see that the div's get lined up.

### step 3: playing around with the Flexbox properties

Flexbox has some fun properties, and they are mainly divided in to two categories:
1. Properties for the parent
2. Properties for the children

At CSS-Tricks you can find a nice overview of the [different properties](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

#### 1. Properties for the parent
-   **flex-direction:** row | row-reverse | column | column-reverse
-   **flex-wrap:** nowrap | wrap | wrap-reverse
-   **justify-content:** flex-start | flex-end | center | space-between | space-around | space-evenly
-   **align-items:** flex-start | flex-end | center | baseline | stretch
-   **align-content:** flex-start | flex-end | center | space-between | space-around | stretch

#### 2. Properties for the child
-   **order:** integer (default is 0)
-   **align-self:** auto | flex-start | flex-end | center | baseline | stretch
-   **flex-grow:**: number (default is 0)
-   **flex-shrink:** number (default is 0)
-   **flex-basis:** length | auto (default is auto)

Let's play around with the parent properties! Here are some small exercises:

- Make the row into a column again, using flex box
- Reverse the row
- Distribute the child divs so that the first one is all the way to the left, the last child div is all the way to the right, and the other divs are equally distributed along the x-axis.

Ok, now let's play around with the child properties. You can do this inline or in the style tag.
- Let's make "Home" the third word, without replacing divs.
- Let's put "Search" all the way right, and the other buttons left (Hint: margin-left: auto;). It's best to do this with a class, this will help you out in the next step.


Just to finish it off, let's add a min-width to the buttons, and  let's align the text of each button to the center.

```
.container > div {
      background-color: #5CC9F5;
      min-width: 80px;
      text-align: center;
    }
```

### Step 3: Adding Responsiveness

Ok, now we have a menubar, that works well on desktop, but we want i to be responsive and work nicely on mobile.

There are multiple UX ways to do this. The quickest way is by adding a "wrap" property to the flex parent.

```
.container {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap-reverse;
}
```
    
But thanks to media queries, we can have a bit more fun: we'll make the menu switch to a vertical stacked menu if the screen is smaller than 400px in width.

```
    @media all and (max-width: 400px) {
      .container {
        display: flex;
        flex-direction: column;
      }

      .search {
        margin-left: 0;
      }
  }
```

Now let's give the parent div a height, for example 200px, and evenly distribute the children.

Now we can center the div's, using the align-self property:

```
      .container > div {
          align-self: center;
      }
```

Now try to swap the order, and make Search the first item on mobile view.

This is the end result. Of course, as there is no one truth in coding, you can end up with some differences.

```
<html>

<head>
  <style>
    div {
      border: 1px solid #6638F0;
    }

   .container > div {
      background-color: #5CC9F5;
      min-width: 80px;
      text-align: center;
    }

    .container {
      display: flex;
      justify-content: space-between;
    }

    .search {
      margin-left: auto;
    }

    @media all and (max-width: 400px) {
      .container {
        height: 200px;
        display: flex;
        flex-direction: column;
      }
      
      .container > div {
          align-self: center;
      }
      .search {
        margin-left: 0;
        order: -1;
      }

    }
  </style>
</head>

<body>

  <div class="container">
    <div>Home</div>
    <div>Team</div>
    <div>Contact</div>
    <div class="search">Search</div>
  </div>

</html>
```

### Step 4: Make it semantic

Now we have our CSS the way we want it, we should make our html a bit more semantic. HTML Semantics are often overlooked, and really not super easy, as the specs sometimes leave a lot of decisions up to the developer. But, in this case there is a simple and clear way to go.

- A menu or navigation should be contained in the <nav> tag.
- Menu items should be written as a list with ordered or unordered children.

So we end up with this:

```
<html>

<head>
  <style>
    ul.container {
      border: 1px solid #6638F0;
      display: flex;
      justify-content: space-between;
      list-style: none;
	    margin: 0;
      padding: 0;

    }
    
   ul.container > li {
      background-color: #5CC9F5;
      min-width: 80px;
      text-align: center;
    }
    
    .search {
      margin-left: auto;
    }

    @media all and (max-width: 400px) {
      ul.container {
        height: 200px;
        display: flex;
        flex-direction: column;
      }
      
      ul.container > li {
          align-self: center;
      }
      .search {
        margin-left: 0;
        order: -1;
      }

    }
  </style>
</head>

<body>
  <nav>
    <ul class="container">
      <li>Home</li>
      <li>Team</li>
      <li>Contact</li>
      <li class="search">Search</li>
    </ul>
  </nav>

</html>
```

Notice the margin and padding added in the <ul> element. The <ul> element has browser inherent padding & margin by default. This way we get rid of it.

### 5: Extra: a simple stacked bar chart

We haven't looked at "flex-grow" and "flex-shrink" yet. These properties have a lot of value, and, together with "max-width" and "min-width", you can get really creative.

A simple example with "flex-grow" is a stacked bar chart:

```
<html>

<head>
  <style>
    
    .container {
      display: flex;
      margin: 0;
      padding: 0;
      height: 20px;
    }

    .container > div:nth-child(1) {
      background-color: #F78AE0;
      flex-grow: 2;
    }
    
    .container > div:nth-child(2) {
      background-color: #6638F0;
      flex-grow: 2.2;
    }
    
    .container > div:nth-child(3) {
      background-color: #4AF2A1;
      flex-grow: 1;
    }

  </style>
</head>

<body>
  <div class="container">
    <div></div>
    <div></div>
    <div></div>
  </div>
</html>
```

And of course, you can quickly change this bar chart to a vertical chart, using media queries.

#### Extra note about prefixes

Some browsers use prefixes to correctly show flex-box.
