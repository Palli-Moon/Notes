JavaScript
----------

#### map()
```javascript
var arr = [1, 2, 3]
var result = arr.map(function(cell) {
    return cell * 2;
});
```
Map applies a given function to every element in an array.

#### Objects
Objects in JavaScript have a slightly different syntax when declaring variables.

```javascript
var obj = {
    a: "a",
    b: 2,
    func: function(x) {
        return x;
    }
};
```

Note: the var keyword is not used when creating an object. More properties can be added to an object after it's creation like so `obj.c = true`, however it may get confusing what properties the objects has at any given time if added afterwards. A property can be removed with *delete* keyword, ex: `delete obj.b`.

#### Semicolons
In JavaScript, semicolons should be used similar to C++. They are generally not needed at all, but they are best used at the end of any statement. They are only used after curly brackets if a variable is being assigned. Consider:
```javascript
var func = function() {
    // do something
};

function func (true) {
    // do something else
}
```

The first example has a semicolon at the end because a function is being declared and assigned to a variable, a semicolon is unnecceasary in the second example since there is no assignment going on. Loops and if statments should never have semicolons at the end.
