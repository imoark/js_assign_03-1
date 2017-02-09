Closure

In Javascript there are two ways that you can declare variables, the one that is declared outside a function which will be in the global scope, and the one that is declared within a function, which will be a local scope.


A global scope (variables) therefore, are available to the entire application (or the entire HTML document), while local scope(variables) mean that they are only accessible within that function or by functions inside that function.


This inner function that (has) access to the outer function’s variables is called a Closure. It chains up (or bind, or sequence) the scope through different level. (It is doing so, not by literally storing the value from the parent function's, but by storing a 'references' of the outer function's value.)


It has up to 3 chains: 
1. it has access to its own scope (variables defined between its curly brackets), 
2. it has access to the outer function’s variables
3. it has access to the global variables.

Usually, 

Here is an simple example of Closure:

function yourPet (firstPet, secondPet) {
	​var petIntro = "Your pets are ";
	​function makeSentenceFormat () {       
	 	return petIntro + firstPet + " and " + secondPet; 
	} // this inner function (function makeSentenceFormat) has access to the outer function's variables, including the parameter​
	​
	​return makeSentenceFormat ();
}
​
yourPet ("Cat", "Dog"); // Your pets are Cat and Dog


Here is the extended example of good usage of Closure:

function yourPet(firstPet) {
	​var petIntro = "Your pets are ";
	​function makeSentenceFormat(secondPet) {       
	 	return petIntro + firstPet + " and " + secondPet; 
	} // this inner function (function makeSentenceFormat) has access to the outer function's variables, including the parameter​
	​
	​return makeSentenceFormat;
}

var globalPet = yourPet("Cat"); // At this point, the yourPet outer function has returned.

// The closure makeSentenceFormat() is called here after the outer function has returned above​
​// Yet, the closure still has access to the outer function's variables and parameter​

globalPet("Dog"); // Your pets are Cat and Dog

How it works?

So what's interesting about this is that you call globalPet() after yourPet() has exited. globalPet()'s variable name should be gone from the world. But when you call globalPet(), you can see that name is still alive, from its perspective (i.e. its context).
It's the inner function, named makeSentenceFormat() inside globalPet() and assigned to the variable globalPet() when you call globalPet(), that's the closure. It's a closure because it's a function that's returned by another function, but it still retains--it's "closed over"--the context in which it was defined.


So why do we need to use Closure?

The main advantage is that any variables you have inside your code is not exposed to the Global namespace and thus you guard against colliding with other libraries or parts of your app.

For example lets say we have a code that is like this:

(function(){
    var count = 100;
    //do stuff with count
}());

Now lets say in a library or another js file that a coworker wrote he/she had this (and both get loaded into the same page)

(function(){
    var count = 10;
    //do stuff with count
}());

Because they are both in local scope, your variables and his/her are isolated and won't clash. If they were not in an local scope, it could override each other.


Reference:
Learning JavaScript, 3rd Edition, Ethan Brown, O'Reilly Media, Inc., 2016
HTML5, JavaScript, and jQuery 24-hour trainer / Dane Cameron
Cameron, Dane, 2015
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures
http://www.w3schools.com/js/js_function_closures.asp
