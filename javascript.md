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
Objects in javascript have a slightly different syntax when declaring variables.

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
