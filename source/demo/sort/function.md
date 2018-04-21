

# Global 常用的检测方法

```js
false                                       // 0,'',null,undefined,false,NaN
null                                        // 空对象指针
undefined                                   // 未初始化的变量，由null派生而来
eval('console.log("evel")')                 // 完整强大的 ECMAScript 解析器
typeof []                                   // 输出 object，检测变量的数据类型
Object.prototype.toString.call([])          // 输出 [object Array]，检测引用类型的原型
isNaN()                                     // 非数值型数据检测，自身不相等(null != null)
isFinite()                                  // 检测某个数值是否在最大值（Number.MAX_VALUE）和最小（Number.MIN_VALUE）之间
parseInt()                                  // 强制转换为整数，第二个参数可以指定进制格式
parseFloat()                                // 强制转换为小数类型。
encodeURI('http://baidu.com')               // 输出 'http://baidu.com'，适用于编码 domain
decodeURI('http://baidu.com')               // 输出 'http://baidu.com'，适用于解码 domain
encodeURIComponent('/api?name=baidu')       // 输出 '%2Fapi%3Fname%3Dbaidu' ，适用于编码 API参数
decodeURIComponent('%2Fapi%3Fname%3Dbaidu') // 输出 '/api?name=baidu',适用于解码 API参数
Array.isArray([]);                          // 返回 true
```
