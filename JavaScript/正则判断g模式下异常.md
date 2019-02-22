正则g模式下出现true和false交替
- 原因：正则表达式中的g模式, 使得搜索过程后, 如果匹配成功, 则记录上一次字符串的位置, 如果匹配不成功, 则会归零字符串位置.

- 解决：
  - reg.lastIndex = 0;	 归零搜索的位置
  - 去掉g模式
  - 直接调用正则

- 在chrome-console中尝试下下面几段代码

  ```javascript
  1
  const reg = /^a/g;
  reg.test('a');     //不断对此式进行取值
  2
  const reg = /^a/g;
  reg.lastIndex      // 此时console显示为1
  reg.lastIndex = 0; // 手动归0
  reg.test('a');     //不断对此式进行取值
  3.
  const reg = /^a/;
  reg.test('a');     //不断对此式进行取值
  4.
  /^a/g.test('a');   //不断对此式进行取值
  ```

  