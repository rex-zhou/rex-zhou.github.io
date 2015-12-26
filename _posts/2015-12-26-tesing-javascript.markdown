---
layout: post
title: "Front-end javascript testing with Mocha and Chai"
date: 2015-12-26 22:30:00
---

As the [interpreter](https://github.com/rex-zhou/Schemescript) becomes more and more complex, testing the program in the textarea turns into an impossible mission. To test the javascript in HTML, better to separate the javascript file from the HTML file. But the javascript file could not be tested as the [Node](https://nodejs.org) file, you need to do a little small change to export the function you want to test.

Your javascript file:
{% highlight javascript %}
(function (exports) {
  "use strict";

  function myFunction(a, b) {
    return a + b;
  }

  exports.myFunction = myFunction;
})(this);
{% endhighlight %}

Then you can import you function in your test class as blow:
{% highlight javascript %}
"use strict";

var assert = require('assert');
var myFunction = require('script.js').myFunction; //The script.js is the file contains your function

//Then you can test as a nodejs test case
assert.equal(myFunction(1, 2), 3);
{% endhighlight %}

Congratulations, you now can test your front-end javascript in your unit test case. To make it more effective I recommend  Mocha and Chai as your testing framework.
You can find those two framework in below website.

- [Mocha](https://mochajs.org/)
- [Chai](http://chaijs.com/)

Both of the framework are available on npm.
{% highlight bash %}
$ npm install mocha
$ npm install chai
{% endhighlight %}

Recommend adding them to `package.json` file using a `*` as the version tag. This will ensure that you always have the most recent version.

#Tesing javascript with Mocha
All the Mocha test case file should located in the `test` folder. Then we could enhance the above test case with Mocha.
{% highlight javascript %}
"use strict";

var assert = require('assert');
var myFunction = require('script.js').myFunction; //The script.js is the file contains your function

//We can easily add some description to it
describe('myFunction(param1, param2)', function () {
  it('should return 3 if param1 = 1, param2 = 2', function (){
    assert.equal(myFunction(1, 2), 3);
  });
});
{% endhighlight %}

Run the `mocha` command in your terminal, also you can add as a test command to your `package.json` file. The result will print as below:
{% highlight bash %}
myFunction(param1, param2)
      ✓ should return 3 if param1 = 1, param2 = 2
1 passing (1ms)
{% endhighlight %}

If you want to assert an exception thrown by your function, you need to improve chai to your test cases.
Ok lets make the `myFunction` throw an exception.
{% highlight javascript %}
function myFunction(param1, param2) {
  if (isNaN(param1) || isNaN(param2)) {
    throw 'Param error';
  }

  return param1 + param2;
}
{% endhighlight %}

Then we add a test case for detect the exception:
{% highlight javascript %}
describe('myFunction(param1, param2)', function () {
    it('should return 3 if param1 = 1, param2 = 2', function () {
      assert.equal(myFunction(1, 2), 3);
    });
    it('should throw an exception when param and param are not number', function (){
      //here we use chai to assert the exception
      expect(function () {
        assert.equal(myFunction('jack', 'rose'), 3);
      }).to.Throw('Param error');
    });
  });
{% endhighlight %}

Run again the `mocha` command in your terminal, as you see, the exception has been tested.
{% highlight bash %}
myFunction(param1, param2)
      ✓ should return 3 if param1 = 1, param2 = 2
      ✓ should throw an exception when param and param are not number

2 passing (1ms)
{% endhighlight %}

To find more useful test function you can refer to the official document of Mocha and Chai, this should helpful to test your frond-end javascript:)
