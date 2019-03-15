# Best practices
Written by Larisa Bulacheva

**1/10 Place Scripts at the Bottom of Your Page**
The primary goal is to make the page load **as quickly as possible for the user**. When loading a script, the browser can't continue on until the entire file has been loaded. Thus, the user will have to wait longer before noticing any progress.
If we have JS files whose only purpose is to add functionality -- for example, after a button is clicked -- go ahead and place those files at the bottom, just before the closing body tag. 
Example:
```<p>And now you know my favorite kinds of corn. </p>```
```<script type="text/javascript" src="path/to/file.js"></script>```
```<script type="text/javascript" src="path/to/anotherFile.js"></script>```
```</body>```
```</html>```

**2/10 Declare Variables Outside of the For Statement**
When executing lengthy "for" statements, don't make the engine work any harder than it must. For example (bad):
```for(var i = 0; i < someArray.length; i++) {```
```   var container = document.getElementById('container');```
```   container.innerHtml += 'my number: ' + i;```
```   console.log(i);```
```}```

Notice how we must determine the length of the array for each iteration, and how we traverse the dom to find the "container" element each time -- highly inefficient!
For example (good):
```var container = document.getElementById('container');```
```for(var i = 0, len = someArray.length; i < len;  i++) {```
```   container.innerHtml += 'my number: ' + i;```
```   console.log(i);```
```}```

**3/10 Reduce Globals**
Minimize the use of global variables. This includes all data types, objects, and functions. Global variables and functions can be overwritten by other scripts. Use local variables instead, and learn how to use closures.
Discouraged:
```var name = 'Jeffrey';```
```var lastName = 'Way';```
``` function doSomething() {...}```
```console.log(name); // Jeffrey -- or window.name```
Better:
```var DudeNameSpace = {```
```   name : 'Jeffrey',```
```   lastName : 'Way',```
```   doSomething : function() {...}```
```}```
```console.log(DudeNameSpace.name); // Jeffrey```
Notice how we've "reduced our footprint" to just the ridiculously named "DudeNameSpace" object.

**4/10 Declarations on Top**
It is a good coding practice to put all declarations at the top of each script or function.
This will:
* Give cleaner code
* Provide a single place to look for local variables
* Make it easier to avoid unwanted (implied) global variables
* Reduce the possibility of unwanted re-declarations

Declare at the beginning:
```var firstName, lastName, price, discount, fullPrice;```
Use later:
```firstName = "John";```
```lastName = "Doe";```
```price = 19.90;```
```discount = 0.10;```
```fullPrice = price * 100 / discount;```
This also goes for loop variables (declare at the beginning):
```var i;```
Use later:
```for (i = 0; i < 5; i++) {```
By default, JavaScript moves all declarations to the top (JavaScript Hoisting).

**5/10 Initialize Variables**
It is a good coding practice to initialize variables when you declare them.
This will:
* Give cleaner code
* Provide a single place to initialize variables
* Avoid undefined values

Declare and initiate at the beginning:
```var firstName = "",```
```lastName = "",```
```price = 0,```
```discount = 0,```
```fullPrice = 0,```
```myArray = [],```
```myObject = {};```


**6/10 Don't Use new Object()**
* Use {} instead of new Object()
* Use "" instead of new String()
* Use 0 instead of new Number()
* Use false instead of new Boolean()
* Use [] instead of new Array()
* Use /()/ instead of new RegExp()
* Use function (){} instead of new Function()
Example:
```var x1 = {};           // new object```
```var x2 = "";           // new primitive string```
```var x3 = 0;            // new primitive number```
```var x4 = false;        // new primitive boolean```
```var x5 = [];           // new array object```
```var x6 = /()/;         // new regexp object```
```var x7 = function(){}; // new function object```


**7/10 Use === Comparison**
The == comparison operator always converts (to matching types) before comparison. The === operator forces comparison of values and type.
Example:
```0 == "";        // true```
```1 == "1";       // true```
```1 == true;      // true```
```0 === "";       // false```
```1 === "1";      // false```
```1 === true;     // false```

**8/10 Avoid Using eval()**
The eval() function is used to run text as code. In almost all cases, it should not be necessary to use it. Because it allows arbitrary code to be run, it also represents a security problem.

**9/10 Use Shortcut Notations**
Shortcut notations keep your code snappy and easier to read once you get used to it.
Illegal:
```if(v){```
```   var x = v;```
```} else {```
```   var x =10;```
```}```
Better:
```var x = v || 10;```


**10/10 Call things by their name — easy, short and readable variable and function names
**
Illegal: 
```x1, fe2, xbqne, incrementorForMainLoopWhichSpansFromTenToTwenty or createNewMemberIfAgeOverTwentyOneAndMoonIsFull;```
None of these make much sense — good variable and function names should be easy to understand and tell you what is going on — not more and not less. One trap to avoid is marrying values and functionality in names. A function called isLegalDrinkingAge() makes more sense than isOverEighteen() as the legal drinking age varies from country to country, and there are other things than drinking to consider that are limited by age.
Better: 
```isOverEighteen, familyName, isLegalDrinkingAge;```
Hungarian notation is a good variable naming scheme to adopt (there are other naming schemes to consider), the advantage being that you know what something is supposed to be and not just what it is.

For example, if you have a variable called familyName and it is supposed to be a string, you would write it as sFamilyName in “Hungarian”. An object called member would be oMember and a Boolean called isLegal would be bIsLegal. It is very informative for some, but seems like extra overhead to others — it is really up to you whether you use it or not.
Keeping to English is a good idea, too. Programming languages are in English, so why not keep this as a logical step for the rest of your code. Having spent some time debugging Korean and Slovenian code, I can assure you it is not much fun for a non-native speaker.
See your code as a narrative. If you can read line by line and understand what is going on, well done. 


15/03