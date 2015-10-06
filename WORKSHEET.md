# JavaScript Hoisting Worksheet

## Instructions
1. Review each code snippet below.
2. Fill in what will be output to the console.
3. Run the code to see if you were correct.
4. Describe why the code behaved as it did.
5. Re-write the code snippet to maintain the same output, but to avoid hoisting.

```js
var myvar = 'my value'; 
  
(function() { 
	console.log(myvar);
	var myvar = 'local value'; 
})();
```

> output:
>-
>- undefined
>-
> why?
>-
>- because it moves the local variable to the top of the function, but not the definition. 
>-
>-
>-
>-
> rewrite without hoisting
>-
>-var myvar = 'my value'; 
  
>-(function() { 
	var myvar;
	console.log(myvar);
	myvar = 'local value'; 
>-})();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var flag = true; 
  
function test() {
	if(flag) {
		var flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
test();
```

> output:
>-'Switch flag from false to true'
>-
>-
> why?
>-
>-the flag variable is not locally defined, so it cannot be true so it immediality goes to else. 
>-
>-
>-
>-
> rewrite without hoisting
>-var flag = true; 
  
>-function test() {
	var flag;
	if(flag) {
		flag = false;
		console.log('Switch flag from true to false');
	}
	else {
		flag = true;
		console.log('Switch flag from false to true');
	}
}
test();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-


```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	var message = 'Foo bar';
}
saySomething();
```

> output:
>-undefined
>-
>-
> why?
>-becuase it hoists the var message to the top of the saySomething function as blank, then when it console logs, it has nothing in it.
>-
>-
>-
>-
>-
> rewrite without hoisting
>-
>-var message = 'Hello world'; 
  
function saySomething() {
	var message;
	console.log(message);
	message = 'Foo bar';
}
saySomething();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var message = 'Hello world'; 
  
function saySomething() {
	console.log(message);
	message = 'Foo bar';
}
saySomething();
```

> output:
>-'Hello World'
>-
>-
> why?
>-
>-No new variables were declared  in the function.
>-
>-
>-
>-


```js
function test() {
	console.log(a);
	console.log(foo());

	var a = 1;
	function foo() {
		return 2;
	}
}
 
test();
```

> output:
>-
>-undefined
>-2
> why?
>-
>-the function is available to return 2, but only the declartion of 'a' is available.
>-
>-
>-
>-
> rewrite without hoisting
>-
>-
>-function test() {
	var a;
	
	function foo() {
		return 2;
	}

	console.log(foo());
	console.log(a);

	a = 1;
	
}
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
(function() {
	console.log(bar);
	foo();

	function foo() {
		console.log('aloha');
	}

	var bar = 1;
	baz = 2;
})();
```

> output:
>-undefined
>-'aloha'
>-
> why?
>-
>-the function is available to console log 'aloha', but only the declartion of bar is available.
>-
>-
>-
>-
> rewrite without hoisting
>-
>-(function() {
	function foo() {
		console.log('aloha');
	}
	var bar;
	console.log(bar);
	foo();
	bar = 1;
	baz = 2;
})();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	function run() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-
>-'I can Run'
>-
> why?
>-
>-beucase the function run went to the top of the fancy function as a truthie value. So when the fancy function was run, it ran the if statement.
>-
>-
>-
>-
> rewrite without hoisting
>-var run = false;
>-function fancy(arg1, arg2) {
	function run() {
		console.log('Will I run?');
	}

	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	
}
fancy();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-

```js
var run = false;

function fancy(arg1, arg2) {
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	var run = function() {
		console.log('Will I run?');
	}
}
fancy();
```

> output:
>-'i can\'t run'
>-
>-
> why?
>-becuase it moves the variable run (not as a function) to the top as blank, which is a falsey value so it would go right to the else statement.
>-
>-
>-
>-
>-
> rewrite without hoisting
>-
>-var run = false;

function fancy(arg1, arg2) {
	var run;
	if(run) {
		console.log('I can run');
	}
	else {
		console.log('I can\'t run');
	}

	run = function() {
		console.log('Will I run?');
	}
}
fancy();
>-
>-
>-
>-
>-
>-
>-
>-
>-
>-