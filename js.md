```markdown
# diff. between function statement and function expression

```javascript
function abc() {} // statement
var a = function() {} // function expression

```

If you set any object's reference as a key of an map or add it in set it won't be garbage collected. But if you use WeakSet or WeakMap that object will be garbage collected if not used any where elese in the code.

The main difference between function statement and function expression is function statements are hoisted , you can call function statement before declaration(defincation). But in case of function expression the variable is hoisted but value is not assigned so you can't call that function using variable until the assignment happens.

## This Keyword

* => In all functions statement and function expression this keyword points to global object.
* => for arrow function this points to it's enclosing execution context
* => for methods of object this key word point to that object's reference

we can declare class property as a private by using `#` like `#propName`.
chrome devtools can read private members of class.
one instance can read private members of other instances.