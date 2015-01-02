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
var Obj = {
    a: "a",
    b: 2,
    func: function(x) {
        return x;
    }
};
```
Members and methods can also be added using the *this* keyword.

```javascript
var Obj = {
    this.a = "a";
    this.b = 2;
    this.func = function(x) {
        return x;
    };
};
```

This code snippet works exactly like the one above.

More properties can be added to an object after it's creation like so `Obj.c = true`, however it may get confusing what properties the objects has at any given time if added afterwards. A property can be removed with *delete* keyword, ex: `delete Obj.b`.

Objects with constructors do not use the *var* keyword, but are instead declared as a function.

```javascript
function Obj(a, b) = {
    this.a = a;
    var b = b;
    var c = function() {
        return a + b;
    };
};
```

Members and properties can be made private by using the *var* keyword instead of *this*. In the above example only the variable *a* can be called directly from the object.

One can add a method to all objects of a type that have been created with the prototype keyword. E.g. if two objects have already been created of a certain type and method needs to be added, it can be done like so: `Obj.prototype.func = function() { return 0; };`. The two objects of type *Obj* will now both have the *func* function.

The prototype keyword can also be used to make a class inherit from another. E.g. `Obj2.prototype = new Obj();`. Now *Obj2* has all the methods and properties of *Obj*, except if any of them were overwritten in *Obj2's* constructor.

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

#### For-in
To loop through all members of an object the for-in statement can be used.
```javascript
for(var x in obj) {
    console.log(x);
}
```

This code would loop through all the properties of obj and print out their name. **Note:** in this case, the name of the variables will be printed, **not** their values. To print their values, all you need to do is change the second line to `console.log(obj[x]);`, since this will access each property using the brackets notation.
