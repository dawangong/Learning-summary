> 今天关于some和every又引发了我新的思考,还记得前面的判断优化吗?

1. 多或判断

```javascript
const a = '23333';

if (a === '23333' || a === '33333' || a === '43333' || a === '53333') {
    console.log(1);
}
```

之前说过关于这样的判断,可以通过includes来简化,如下:

```javascript
const a = '23333';
const compare = ['23333', '33333', '43333', '53333'];

if (compare.includes(a)) {
    console.log(1);
}
```

其实some方法也可以做到,如下:

```javascript
const a = '23333';
const compare = ['23333', '33333', '43333', '53333'];

if(compare.some(item => item === a)) {
    console.log(1);
}
```

由此也就引发出了every在多“且”条件下的用法,例如:

```javascript
const a = '23333';

if (a === '63333' && a === '33333' && a === '43333' && a === '53333') {
    console.log(1);
}
```

可以改写为:

```javascript
const a = '23333';
const compare = ['33333', '43333', '53333', '63333'];

if (compare.every(item => item === a)) {
    console.log(1);
}
```

