---
css: javascript-error
layout: post
title: Javascript Error Throwing
header-img: ""
---

As a junior web developer I usually don't employ explicit exception handling strategies. When writing code, I don't consider all edge cases and often aim for successful flow of the program. This approach results in dealing with bugs and errors after they happen and it often leads to over-reliance on default error messages which tend to be vague and make debugging more time consuming.

Before continuing a distinction between error and exception needs to be made. _Exceptions are events which can be handled at the run time whereas errors cannot be handled._ An exception happens when the natural flow of the program is interrupted by an unexpected event. In other words, while writing code, exceptions arise when something unexpected happens, this affects the flow of the program and thus the user experience. 

As programmers, to better deal with these events we can take advantage of a practice known as _exception handling._

Exception handling is the process of anticipating, detecting and resolving anomalies or exceptional conditions during computation. This approach requires special processing and often changes the normal flow of the program.

### Types of Errors
----

During software development phase programmers come across various types of programming errors. Programming languages contain rules that, when deviated from, result in errors being displayed in order to provide information. Locating and fixing mistakes and bugs would be terribly difficult if errors weren't reported back to the user.

The major types of errors in programming are:

* _Parsing errors_ aka syntax errors occur at compile time or at interpret time (e.g. Javascript) and are usually typographical mistakes or improper use of special characters. These errors are usually handled by proofreading.

* _Runtime errors_ aka exceptions occur during execution and usually are the result of adverse system parameters or invalid input data and are usually handled by careful debugging.

* _Logical errors_ aka bugs occur when executed code does not produce the expected result and often is the result of human mistake. Handled by debugging tools and error handling approaches.

### Errors in Javascript
----

Dealing with errors can be a challenging process due to the nature of when and where they happen and how they tend to be described in the message. _Javascript error messages are known to be uninformative and ambiguous._ 

If error messages described exactly what happened and where, debugging would be easier to deal with. Javascript like many other programming languages provides developers with ways to do just that, handle exceptions and throw errors which provide more descriptive messages.

Before going into examples of how that can be accomplished it is important to review the base error types in Javascript.

### Base Error Types
----

Javascript contains seven base error types.

* **Error**: A generic error that is not tied to a specific scenario.

* **TypeError**: A TypeError is thrown when a variable is not of the expected type. (_e.g. A boolean is passed in when expecting a string._)

* **RangeError**: These occur when a numeric value is invalid, such as trying to access an index in an array that doesn't exist. (_e.g. Limiting range of allowed dates._)

* **SyntaxError**: A SyntaxError occurs when something is not coded properly. (_e.g. Improper structure of an object literal._)

* **ReferenceError**: If there is a problem with a referenced variable, a ReferenceError is thrown. (_e.g. Expecting an object to have a specific property but that property is not defined._)

* **EvalError**: If JavaScript has a problem parsing an eval() statement, it will throw an EvalError. (_e.g. Misusing the eval() function which provides access to the Javascript compiler._)

NOTE: This exception is not thrown by JavaScript anymore, however the EvalError object remains for compatibility.

* **URIError**: Occurs natively when encodeURI() and decodeURI() cannot parse their content. (_e.g. Throwing a URIError if there are problems with URLs and URIs._)

Being aware of the different types of errors makes it easier to handle them. All error types inherit from _Error.prototype_ object and instances of those objects are thrown when runtime errors occur. The Error object can also be used as a base object for user-defined exceptions. As with all constructors, you can use the prototype of the constructor to augment instances created with that constructor.

### Throwing Your Own Errors

The benefits of throwing your own errors are numerous. Expecting and preparing for failure at _specific locations_ in the code base is more effective than purely relying on default errors or planning to cover every point in code.

> Cars are built with crumple zones, areas of the frame that are designed to collapse in a predictable way when impacted. Knowing how the frame will react in a crash, which parts will fail, allow the manufacturers to ensure passenger safety. Your code can be constructed in the same way. [Source](https://www.nczonline.net/blog/2009/03/03/the-art-of-throwing-javascript-errors/)

Throwing your own errors is a tool in a programmers tool belt. Like other tools it should be used where and when appropriate.

#### Throw operator

You can throw an error by using the `throw` operator and by providing an object to throw, most often an Error object. When not using the `try-catch` statement, the browser will display the error in the typical way.

```javascript
throw new Error("Exception message!!")
```

When using `throw` in this manner browsers treat the error the same way as an error you didn't throw, it includes default message, column and line numbers. The main difference is that you can add a more descriptive message which may help you in debugging the problem.

```javascript
function getAttribute(element, attribute) {
    return element.getAttribute(attribute)
}
```

The above example is a function that returns the value of a specified attribute on the element. When the provided element is null, browsers return a default exception.

Chrome returns error that says:

```
Uncaught TypeError: Cannot read property 'getAttribute' of null(…)
```

Firefox Developer Edition returns an error that looks like this:

```
TypeError: element is null
```

Safari return this error message:

```
TypeError: null is not an object (evaluating 'element.getAttribute')
```

Choosing to throw a custom error we can make debugging easier by providing a message that contains more meaningful information to the developer and looks exactly the same on all three browsers.

```javascript
function getAttribute(element, attribute) {
    if (element !== null && typeof element.className == "string") {
        return element.getAttribute(attribute);
    } else {
        throw new TypeError("getAttribute(): First parameter must be a valid element.");
    }
}
```
The error:

```
TypeError: getAttribute(): First parameter must be a valid element.
```

#### Try-Catch Construct

Javascript provides a `try-catch` statement that allows the developer to capture thrown errors before they are handled by the browser. This provides an opportunity to handle the error and prevent it from breaking your application flow.

```javascript
    function multiply(x, y) {
       if (typeof x !== 'number') {
          throw new TypeError(x + ' is not a number.');
       }
       if (typeof y !== 'number') {
          throw new TypeError(y + ' is not a number.');
       }
       return x * y;
    }

    try {  
       multiply(2, 'a string type');
    } catch (exception) {
       alert(exception.message);
    }
```

In the above example we check that both arguments are numbers and if one of them is not, a TypeError is thrown. The catch block is then run if an error was thrown, passing the error object as an argument. The result of that is an alert box with a message that says _'a string type is not a number'_.

According to Nicholas C. Zakas, a Javascript developer, some developers have trouble discerning whether it's appropriate to throw an error or catch one using `try-catch`.

> Errors should only be thrown in the deepest part of the application stack which typically means JavaScript libraries. Any code that handles application-specific logic should have error handling capabilities and should therefore be catching errors thrown from the lower-level components. Application logic always knows why it was calling a particular function and so is best suited for handling the error. [Source](https://www.nczonline.net/blog/2009/03/03/the-art-of-throwing-javascript-errors/)

He adds that a `try-catch` statement should never have an empty `catch` clause and that the developer should always handle errors in some way.

#### A Note on Error Instance Type

Being familiar with differences in errors and knowing the type of error that was thrown can make it easier to handle them. Because all errors inherit from Error object we can check the types of error instances using the `instanceof` statement.

Using the previous example, we could add a conditional like so:

```javascript
try {
  multiply(2, 'a string type');
} catch (exception) {
  if (exception instanceof TypeError) {
    alert(exception.message);
  } else {
    // report error to server
  }
}
```

The alert will only fire if a `TypeError` is detected notifying the user to fix input. Any other type of error will be logged internally.

### Final Words

Getting to know the types of errors and why they happen is immensely useful when dealing with debugging. Errors help us navigate towards a solution and locate problems in our code. Taking the time to learn where it is best to throw errors and how to handle errors appropriately may result in time savings when debugging and increase the quality of our code.

P.S.

1. Assume your code will fail
2. Log errors to the server
3. You, not the browser, handle errors
4. Identify where errors might occur
5. Throw your own errors
6. Distinguish fatal versus non-fatal errors
7. Provide a debug mode


### Sources

* [Wikipedia Exception handling](https://en.wikipedia.org/wiki/Exception_handling)
* [Tech Target Error-handling](http://searchsoftwarequality.techtarget.com/definition/error-handling)
* [Throwing Custom Errors](http://www.mikemurry.com/throwing-custom-errors-in-javascript/)
* [The Art of Throwing Javascript Errors](https://www.nczonline.net/blog/2009/03/03/the-art-of-throwing-javascript-errors/)
* [The Art of Throwing Javascript Errors, Part 2](https://www.nczonline.net/blog/2009/03/10/the-art-of-throwing-javascript-errors-part-2/)
* [MDN Error Ref](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
* [Enterprise JavaScript Error Handling](http://www.devhands.com/2008/10/javascript-error-handling-and-general-best-practices/)
