# 手写代码
> 通过手写JavaScript代码打牢JavaScript的基本功

## 数组扁平化

**概念** ：将一个多维数组变为一个一维数组

```javascript
const arr = [1, [2, [3, [4, 5]]], 6];
// => [1, 2, 3, 4, 5, 6]
```

1. 使用Array.prototype.flat()

   > flat()会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素合并为一个新的数组返回

   使用flat可以根据传进来的depth，将数据扁平化。如果数组中包含方法，也不会产生数据丢失。

   ```js
   arr.flat(Infinity);
   ```

   

2. 利用正则

   > 将数组转换成JSON字符串，然后使用replace()将[]替换为""

   将数组通过JSON.stringify()转为字符串，然后利用replace()函数将数组中的[]替换为“”，最后使用split(",")，将字符串还原为数组。但是，如果数组中包含方法，则该方法会全部丢失

   ```js
   JSON.stringify(arr).replace(/(\[+)|(\]+)/g, "").split(",");
   ```

   

3. 使用Array.prototype.reduce()

   > reduce : 对数组中的每一个元素依次执行reduce回调函数，将结果汇总为单个返回值

```js
function fn(arr) {
    return arr.reduce((a, b) => {
       return a.concat(Array.isArray(b) ? fn(b) : b) 
    }, [])
}
fn(arr);
```



## 数组去重

```js
const arr = [1, 1, '1', 17, true, true, false, false, 'true', 'a', {}, []];
// => [1, '1', 17, true, false, 'true', 'a', {}, []]
```

1. 利用Set对象

   > Set对象允许存储任何类型的唯一值，无论是原始类型或者是对象引用

   ```js
   Array.from(new Set(arr));
   ```

   

2. 两层for循环+Array.prototype.splice()

   > splice方法通过删除或者替换现有元素或者原地添加新的元素来修改数组，并以数组形式返回被修改的内容。此方法会改变原数组。

   ```js
   (function(arr) {
   	let len = arr.length;
   	for (let i = 0; i < len; i++) {
   		for (let j = len; j > i; j--) {
               if (arr[i] === arr[j]) {
                   arr.splice(j, 1);
                   len--;
               }
           }
   	}
   })(arr);
   ```

3. 利用Array.prototype.indexOf()

   > ​	indexOf方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1

   ```js
   (function(arr) {
       const newArr = [];
       for (let i = 0; i < arr.length; i++) {
           if (newArr.indexOf(arr[i]) === -1) {
               newArr.push(arr[i]);
           }
       }
   })(arr);
   ```

   

4. 利用Array.prototype.include()

   > include方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回true，否则返回false

   ```js
   (function(arr) {
       const newArr = [];
       arr.forEach(item => {
           newArr.includes(item) || newArr.push(item)
       })
   })(arr);
   ```

   

5. 利用Array.prototype.filter()

   > filter方法创建一个新的数组，其包含通过所提供函数实现的测试的所有元素

   ```js
   (function(arr) {
       return arr.filter((item, index, a) => {
          return a.lastIndexOf(item) === index;
       })
   })(arr);
   ```

   

## 类数组转化为数组

>类数组 ：具有length属性，但是不具有数据原型上的方法
>
>常见的类数组 ：arguments，DOM操作方法返回的结果

1.  Array.from()
2.  Array.prototype.slice.call()
3.  扩展运算符
4.  利用concat

## Array.prototype.filter()

## Array.prototype.map()

## Array.prototype.forEach()

## Array.prototype.reduce()

## Function.prototype.apply()

## Function.prototype.call()

## Function.prototype.bind()

## debounce(防抖)

> 防抖：

## throttle(节流)

> 节流：

## 函数柯里化

> 函数柯里化 ：将一个接受多个参数的函数变为接受一个参数返回一个函数的固定形式。

```js
// 经典面试题
// 实现 add(1)(2)(3)(4) = 10; add(1)(2, 3, 4)(2) = 9;
```

## 模拟new操作

## instanceof

> instanceof : 

## 原型继承

## Object.is

## Object.assign

## 深拷贝

## Promise

## Promise.all

## Promise.race

## Promise并行限制

> 实现有并行限制的Promise调度器问题

## JSONP

## AJAX

## event模块

> 实现node中回调函数的机制，node中回调函数其实是内部使用了观察者模式

## 图像的懒加载

## 滚动加载

> 滚动的页面底部，进行后续操作

## 渲染几万条数据不卡住页面

> 渲染大数据时，合理使用createDocumentFragment和requestAnimationFrame，将操作切分为一小段一小段执行

## 打印出当前网页使用了多少种HTLML元素

## 将虚拟DOM转化为真实DOM结构

> 放在vue模块，该部分分为模块编译和Diff算法

## 模板字符串解析问题

