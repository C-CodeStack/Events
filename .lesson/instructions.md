# Events

#### *** If you are having trouble with your code some computers will allow you to inspect elements. Pop your website out into a full tab and then right click on an html element. Then select inspect. If you look at the tabs `elements` and `console` it will give you hints to fix any issues

An `event` is things that happens to an HTML element. JS and/or CSS can respond to them. When you hit run and observe your webview you can see that table 1 and 5 have responses happening. As you mouse over those tables the cells change colors. This event is happening in the CSS due to the code on line 17, 92 and 103

```css
.one td:hover, .one th:hover {
  background-color:aqua;
}
```

As you can see it is the `hover`event that is creating the background color response. You can do the same thing in JS

```javascript
const tableDatas = document.getElementsByTagName("td")
tableDatas[0].onmouseover = () => {// when the mouse passes over the first td this anonomous function runs
  tableDatas[0].style.backgroundColor = "red"
}
```

The DOM has many events. All of which you can find here https://www.w3schools.com/jsref/dom_obj_event.asp. Some of the most popular ones are:

1. change
2. click
3. mouseover
4. mouseout
5. keydown
6. load

There is no exact hover like css has but the closest you have is `mouseover` and `mouseout`. You may have noticed that the example code did not use `mouseover` but `onmouseover`. That is because the event that happens(`fires an event`) when a user puts their mouse over the td, is the mouseover event. 

You need to have something listening for the `event firing`. That is what onmouseover is for. `onmouseover` is considered an event listener. It is attached to the td and it listens for mouseover events to be fired and when it detects that, it will run a function. In the case above it runs an `anonomous function` or a function that has no name.

## Task 1
1. Add the above code to you `script.js` file.
2. If you run your code and it does nothing then you probably never connected your js to your html. Do that now if you need to.
3. Your code successfully changes the td to `red` but it never goes back to `lightgrey`. Attach a onmouseout listener to the same td and have it change the `background color` back to `lightgrey`
#

Now you have one td that changes from red to light grey. It took a lot more work than CSS. Sometimes it is easier to just use CSS for this type of job. However, JS does have its advantages.

```javascript
const clickHandler = () => {
  tableDatas[1].innerText = "CHANGED"
  tableDatas[2].style.backgroundColor = "green"
  alert("CSS can't do this!")
}

tableDatas[1].onclick = clickHandler //not anonomous function
```

The code above attaches an onclick listener to the second td element. This time it runs a named function `clickHandler`. Both ways work just fine but it is common practice to use the `anonomous function` style from the first example. CSS would not be able to do all the things that this js onclick is doing.

## Task 2
1. Copy the above example into your code
2. Use a `dblclick` listener to return the table to its origional form when the second td is double clicked. You may use a named function or anonomous function style
3. You will have to remove or comment out the alert from clickHandler or it won't work
#

Sometimes you will have to attach the same function to many different event listeners. You could use the techniques from above but that would envolve a lot of DOM traversal or putting in a bunch of ID's in the index.html file. You might want to try this instead.

```javascript
let count = 1
const countHandler = (element) => {//notice the parameter
  element.innerText = count
  count++
}
```

## Task 3
Add the above to your `JS` and change line 16 in your `HTML` to:
```html
<th onmouseleave="countHandler(this)" colspan="4">Table one</th>
```
#

Notice how the listener is `onmouseleave`. If you don't know what that does check out this link https://www.w3schools.com/jsref/event_onmouseleave.asp.

To summarize, the event fires and is listened to by `onmouseleave` that is attached to the HTML directly. Last time we attached it in the JS. The listener calls `countHandler` to run and passes the argument `this`. The `this` just means that it is passing itself for the function to manipulate. It would be the same as using `getElementById`. It would give us the element we are looking to change. In this case it is the one that called it or `this`. 

Now we are inside the JS function `countHandler`. This function changes the innerText and increments the counter by 1.

## Task 4
Change HTML line 200 to:
```html
<td onmouseenter="countHandler(this)">Table data</td>
```

HTML line 173 to:
```html
<td onclick="countHandler(this)">Table data</td>
```
#

You are able to add this function to any number of elements simply by adding a `listener` attribute to the element and calling `countHandler(this)`. Since we don't have to rewrite the countHandler code everywhere this makes your code `DRY` and thats a good thing.

## Task 5 
1. In JS create a function called `rowColorOn`
2. Give this function a `parameter` called `element`
3. Set the border style to be `10px solid red`
4. In HTML For table 2 and 4 apply onmouseenter attribute to each `tr` and make it call `rowColorOn`
#

## Task 6
1. In JS create a function called `rowColorOff`
2. Give this function a `parameter` called `element`
3. Set the border style to be `initial`
4. In HTML For table 2 and 4 apply onmouseenter attribute to each `tr` and make it call `rowColorOff`
#

Your table 2 and 4 should now color the border for the row red when the mouse is on it and back to normal when it is not.