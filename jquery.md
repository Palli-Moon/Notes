jQuery
----------

#### .next() and length
To prevent overflowing with the `.next()` built-in function, once can check the length of the next element. If it's length is 0, the element doesn't exist and can be reset using `.first()`.

```jquery
var nextElem = $('.class').next();
if (nextElem.length == 0) {
    nextElem = $('.class').first();
}
```
