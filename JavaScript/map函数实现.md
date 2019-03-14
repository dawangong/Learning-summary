写成这样主要为了减少多余的中间变量,尽可能遵循函数式编程的思想.(好吧,我承认可能看起来有些奇怪...)

```javascript
Array.prototype._map = function (fn, arg, result = []) {

    for(let i = 0; i < this.length; i++) {
        result.push(fn.apply(arg, [this[i], i, this]));
    }

    return result;
};

const res = [1, 2, 3]._map(item => item * 2);

console.log(res);
```

