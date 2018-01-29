# Set在ES6中新增的数据结构，类似于数组，成员的值都是唯一的。
看到上面的话首先想到的竟然是唯一的，那么久可以进行筛选数组的重复值，可以直接去重。
> * 但是我在今天用Vue做QQ-music的时候想去点击全部播放，进而去筛选其重复值的时候，发现他也有缺陷。他不能去重引用类型的值，所以说只适合常规的进行筛选。

![tool-editor](https://github.com/liu33286821/ES6/blob/master/Set_Object.png)

上面这个例子我按照项目格式编写的对象。 发现数组是四个对象，使用Set()还是4个对象。 所以说引用类型不能使用Set来进行筛选。

## 用法：

```javascript
    const arr = [1,2,2,2,2,3,4,5]
    const set = new Set(arr)
    console.log(set)
    console.log(...new Set(arr))
```

![tool-editor](https://github.com/liu33286821/ES6/blob/master/set.png)


## Set实例的属性和方法
Set结构属性：
    > * Set.prototype.constrcutor ： 构造函数，默认就是```Set```函数。
    > * Set.prototype.size: 返回Set的成员个数。

Set的方法：
    > * ```add(value)``` 添加值  返回Set结构的本身
    > * ```delete(value)``` 删除某个值，返回一个布尔值，表示删除成功与否。
    > * ```has(value)``` 返回一个布尔值，表示该值是否为Set的成员。
    > * ```clear()``` 清除所有成员，没有返回值。


//ES6数组去除重复操作
```javascript
    function unique (arr) {
        return Array.from(new Set(arr))
    }
    unique(arr)
```


## 遍历操作。
Set结构的实例有四个遍历方法可以遍历成员。
    - ```keys()``` 返回键名的遍历器
    — ```values()``` 返回键值得遍历器
    - ```entries()``` 返回键值对的遍历器
    - ```forEach()``` 使用回调函数遍历每个成员
在这里需要提醒的是**Set没有键名只有键值,常规来说的意思就是它俩都是指向 同一个值** 那么```keys()```和```values()```都会得到同一个值，使用方法也完全相同。

### values() keys() entries()
```javascript
    let set = new Set([1,2,3,2,2,3])
    for(let i of set) {console.log(i)}
    for(let i of set.keys()){console.log(i)}
    for(let i of set.values()){console.log(i)}
    //以上三个个方法返回的都是同样的值
    //第一种方法是因为当Set结构实例默认可遍历，生成器函数就是他的values

    for(let i of set.entries()) {console.log(i)}
    //而entries()返回的是键值对。
```

### forEach()
```javascript
    set = new Set([1,4,9])
    set.forEach((key,val,arr) => console.log(`${key}:${val}`))
    //1：1
    //4：4
    //9：9
```
看到上面的代码，其实也是**键值键名**都是同一个值


## 在原来的ES6之前我们经常会遇见一些面试题目，考查其**交集**、**并集**、**差集**。当然在使用Set()的时候就比较简单了。
```javascript
    let a = new Set([1,2,3])
    let b = new Set([2,3,4])
    //在这里不懂 ...的话，可以去看看阮一峰的ES6教程。
   //并集
   console.log(new Set([...a,...b]))
   //1,2,3,4

   //交集
   let intersect = new Set([...a].filter(x => b.has(x)))
   //2,3
   //这里使用了filter  上面已经提到过Set的遍历操作。has()去查询有没有这个值，返回true或false
   //看到这里可能我需要去试验下我在上面留下的第一张图片了

   //差集
   let difference = new Set([...a].filter(x => !b.has(x)))
   // 1
```

## 在看ES6的软文中，在其介绍Set最下面的时候出现了 **想在遍历操作同步改变原来的Set结构，没有直接的方法，只能通过映射。或者from**。
```javascript
    //方法一
    let set = new Set([1,2,3])
    set = new Set([...set].map(val => val*2))
    //2,4,6

    set = new Set(Array.form(set,val => val*2))
```

