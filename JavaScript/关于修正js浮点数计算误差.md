> js浮点数乘法是有误差的，这个问题是在很久以前一次项目计算中发现的，那么接下来就说一下如何修正这个误差。

下面直接上代码吧，简单来说就是以小数点为基准进行切割，将是浮点数的转为整数进行计算，最后再放大小数点后N倍还原正确计算结果。

```javascript
=========> 比如计算 0.14*10

// 直接答案 1.4000000000000001 这显然不是我们想要的结果

function accMul(arg1, arg2) {

	let m = 0;
	const s1 = arg1.toString();
	const s2 = arg2.toString();

	if (s1.includes('.')) {
		m += s1.split('.')[1].length;
	}

	if (s2.includes('.')) {
		m += s2.split('.')[1].length;
	}

	return Number(s1.replace('.', '')) * Number(s2.replace('.', '')) / Math.pow(10, m);
}

//调用accMul accMul(0.14, 10) 得到 1.4 这才是我们想要的
```

