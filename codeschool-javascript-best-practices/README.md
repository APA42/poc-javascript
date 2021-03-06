
#Interesting links
https://www.codeschool.com/account/courses/javascript-best-practices

Code conventions for JS:
http://javascript.crockford.com/code.html

45 useful JS tips:
http://modernweb.com/2013/12/23/45-useful-javascript-tips-tricks-and-best-practices/

#Best Practices
* Do NOT use eval



#Level 3: The crystal of caution

##Careful comparisons
Not all equality comparisons are equal
The triple equals compares both type AND contents.
== (double equals operator) uses “type coercion”, which turns a number contained within a string into an actual number.
=== (triple equals operator) does NOT ignore the type of the value.
An object is an instance of all the prototypes from which it inherits properties.


##Exception handling

##Stuff that sometimes sucks
JavaScripts 'with' keyword is somewhat unreliable and often expensive, so it is generally avoided in practice.

with(drawbridge) {
	close = function() {
		alert('CLACK!');
	}	
}
The with keyword takes the entire encapsulated environment of the parameter object and use it to build a new “local” scope within its bracketed block … which is kind of processing-expensive. 
The close() function indeed is not created in the SAME scope of the object drawbridge, so it doesn't belong to the object...

"with" goal is to limit redundancy, since you can access the objects attributes withoug "this" or anything else, you get into its scope.
"with" makes it unclear which properties or variables are modified: global scope or object scope?

eval() affects legibility. Eval might be useful for dynamic code or uncontrollable data, but it's still treating the string as a program to expensively compile.
If what you want is to create dynamically an attribute name with a number (e.g. "attribute_1"), instead of eval(), use an array and access the value you need (attributes[i]).
Using eval() to parse JSON data is often regarded as vulnerable and unsafe, because eval evaluates any script >> use JSON.parse() instead.

##Number Nonsense
JavaScript uses binary floating point values to handle all of its decimal based operations.
toFixed()
parseFloat()
parseInt(): instead of looking for a floating point number, parseInt() seeks the first available integer at the front of a string.
parseInt("021", 10): to assure that you expect decimal system.

parseFloat(value.toFixed(1));

Using NaN to check if values are actually JS Numbers is not a good idea.
typeof NaN; >> number
NaN === NaN >> false
isNaN("42") >> false because it looks for the NaN value itself!!
Do a double check to know if it is a number!!: 
function isANumber(data) {
	return ( typeof data === "number" && !isNaN(data) );
}

#Level 4: The Mail of Modularity

##Namespacing basics
Conflicting global elements!!
variables with same name in different files get overwritten due to hoisting.
The key to creating a namespace is a single globlal Object, commonly called the "wrapper" for the space (name capitalized entirely).
The name of the namespace acts as a shield.
Nested namespacing is frequent in module pattern. Nesting namespaces provide further organization and protection, as well as help keep variable names intuitive.

##Anonymous closures
The thing with a namespace is that you have to "hope" that no one else ever uses its name.
We want to hide "private" properties, wrapping the whole file into an IIFE: Immediately Invoked Function Expression.
To make some properties public, return an object (see slides).

##Global imports
When non-local variables are referenced in a module, the entire length of the scope chain is checked (besides dangerous, it is slow).
For clearer, faster global variables in modules, use imports.
Pass all your globals into your IIFE using the calling parantheses: the function's parameter creates a modifiable value for use in the module, while the global value stays protected if necessary.

##Augmentation
How to augment the modules.
No var keyword. We pass in the IIFE as parameter.
Any new properties will have no access to the private data from the earlier closure. The earlier public properties however will retain the reference.
Best practice: group file contents around needed data.
So... you better do NOT augment your modules.


Bookmark:
http://campus.codeschool.com/courses/javascript-best-practices/level/4