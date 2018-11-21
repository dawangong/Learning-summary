相信下面的代码很眼熟吧

```javascript
const a = '23333';

if (a === '23333' || a === '33333' || a === '43333' || a === '53333') {
    console.log(1);
}
```

如果a的值有更多可能呢？或许可以这样写：

```javascript
const a = '23333';
const compare = ['23333', '33333', '43333', '53333']

if (compare.includes(a)) {
    console.log(1);
}
```

有没有觉得好多了？实际上可能平常困扰更多的是大量的if-else的使用，其实这也是有办法简化的。

例如这样的判断：

```javascript
const state = 'a';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

if (state === 'a') {
    add('state1');
    go('state1')
} else if (state === 'b') {
    add('state2');
    go('state2')
} else if (state === 'c') {
    add('state3');
    go('state3')
} else if (state === 'd') {
    add('state4');
    go('state4')
} else if (state === 'e') {
    add('state5');
    go('state5')
}
```

可以使用switch替换如下：

```javascript
const state = 'a';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

switch (state) {
    case 'a':
        add('state1');
        go('state1');
        break;
    case 'b':
        add('state2');
        go('state2');
        break;
    case 'c':
        add('state3');
        go('state3');
        break;
    case 'd':
        add('state4');
        go('state4');
        break;
    case 'e':
        add('state5');
        go('state5');
        break;
}
```

好像没有太大的变化…别着急，其实像这样的一元条件判断可以通过object对象或者Map对象存储达到降低代码的冗杂度。具体怎么做呢？请看一下下面两种写法：

```javascript
const state = 'a';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

const handle = {
    'a': 'state1',
    'b': 'state2',
    'c': 'state3',
    'd': 'state4',
    'e': 'state5'
};

add(handle[state]);
go(handle[state]);
```

```javascript
const state = 'a';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

const map = new Map([
    ['a', 'state1'],
    ['b', 'state2'],
    ['c', 'state3'],
    ['d', 'state4'],
    ['e', 'state5']]);

add(map.get(state));
go(map.get(state));
```

这样代码是不是感觉简洁多了？如果是更复杂的判断情况呢？比如下面的：

```javascript
const state = 'a';
const author = 'me';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

if (author === 'me') {
    if (state === 'a') {
        add('state1');
        go('state1')
    } else if (state === 'b') {
        add('state2');
        go('state2')
    } else if (state === 'c') {
        add('state3');
        go('state3')
    } else if (state === 'd') {
        add('state4');
        go('state4')
    } else if (state === 'e') {
        add('state5');
        go('state5')
    }
} else if (author === 'you') {
    if (state === 'a') {
        add('state11');
        go('state11')
    } else if (state === 'b') {
        add('state22');
        go('state22')
    } else if (state === 'c') {
        add('state33');
        go('state33')
    } else if (state === 'd') {
        add('state44');
        go('state44')
    } else if (state === 'e') {
        add('state55');
        go('state55')
    }
}
```

上面的有两个判断条件，我们称为二元条件判断。这种情况又该怎么处理呢？请看下面的写法：

```javascript
const state = 'a';
const author = 'me';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

const handle = {
    'me_a': 'state1',
    'me_b': 'state2',
    'me_c': 'state3',
    'me_d': 'state4',
    'me_e': 'state5',
    'you_a': 'state11',
    'you_b': 'state22',
    'you_c': 'state33',
    'you_d': 'state44',
    'you_e': 'state55'
};

add(handle[`${author}_${state}`]);
go(handle[`${author}_${state}`]);
```

这次通过字符串拼接和对象存储，实现了二元条件的判断简化。当然也可以用Map对象来做容器，这里我就不演示了。

其实这个并不是最好的方法，或许对于二元条件判断来说可以接受，但是如果是三元判断甚至更多呢？总不能因为es6的模版字符串好用而无脑使用字符串拼接吧。

这个时候Map对象的优势就体现出来了，我们都知道Map对象的key可以是任何值。利用这个特性我们可以通过Map对象作为容器管理多元判断。具体怎么做呢？请看下面的代码：

```javascript
const state = 'a';
const author = 'me';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

const map = new Map([
    [{state: 'a', author: 'me'}, 'state1'],
    [{state: 'b', author: 'me'}, 'state2'],
    [{state: 'c', author: 'me'}, 'state3'],
    [{state: 'd', author: 'me'}, 'state4'],
    [{state: 'e', author: 'me'}, 'state5'],
    [{state: 'a', author: 'you'}, 'state11'],
    [{state: 'b', author: 'you'}, 'state22'],
    [{state: 'c', author: 'you'}, 'state33'],
    [{state: 'd', author: 'you'}, 'state44'],
    [{state: 'e', author: 'you'}, 'state55'],
]);

const item = [...map].filter(([key, value]) => key.state === state && key.author === author );
const [key, value] = item[0];

add(value);
go(value);
```

那么这样就够了吗？其实有了Map对象做容器后，我们可以实现更复杂的多元判断管理。

比如，某几个状态( state = b || c || d || e 同时 author = me)会执行相同的函数，此时引入正则即可实现这样的多元判断简化，如下：

```javascript
const state = 'c';
const author = 'me';

function add(param) {
    console.log(param);
}

function go(param) {
    console.warn(param);
}

const map = new Map([
    [/^a_me$/, 'state1'],
    [/^b|c|d|e_me$/, 'state2'],
    [/^a_you$/, 'state11'],
    [/^b_you$/, 'state22'],
    [/^c_you$/, 'state33'],
    [/^d_you$/, 'state44'],
    [/^e_you$/, 'state55'],
]);

const item = [...map].filter(([key, value]) => key.test(`${state}_${author}`) );
const [key, value] = item[0];

add(value);
go(value);
```

有没有一种再也不会被大量的if-else困扰的感觉？2333...