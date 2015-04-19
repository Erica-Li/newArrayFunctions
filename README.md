# ES5中新增的Array方法  

1. forEach
2. map  
3. filter  
4. some  
5. every
6. indexOf
7. lastIndexOf  
8. reduce  
9. reduceRight

--------------------------

* var arr = [0, 1, 2, 3, 4, 5, 6];*
-------------------------
-------------


## 1. forEach

### 循环，遍历 

`arr.forEach(function(value, index, array){});`  

######  value：数组内容； index：索引； array：数组本身   

    arr.forEach(function(a, index) {
        console.log(a);
    });

`arr.forEach(callback, [thisObject]);`

###### forEach除了接受一个必须的回调函数参数，还可以接受一个可选的上下文参数（改变回调函数里的`this`指向，this指向thisObject；若不指定，则为全局对象`window`）

------------

## 2. map

### 映射，将原数组映射成新的数组

`arr.map(function(value, index, array){}, [thisObject]);`

    var newArr = arr.map(function(a) {
        return a * a;
    });

*注：callback一定要有return，否则数组各项都为undefined*

---------------

## 3. filter

### 返回过滤之后的新数组

`arr.filter(function(value, index, array){}, [thisObject]);`

    var newArr = arr.filter(function(a) {
        if(a == 2) {
            return true;
        }
    });

*注：callback函数需要返回true/false。但是，返回值只需要弱等于`==true/false`就行，并非一定要返回`===true/false`*

    var newArr = arr.filter(function(a) {
        return a;
    });     //[1,2,3,4,5,6]

------------

## 4. some

### 是否某些项合乎条件

`arr.some(callback, [thisObject]);`

    arr.some(function(a) {
        if(a > 2) {
            console.log(a);    //3   ------只输出3
            return true;
        }
    });

*注： some只要有一个值让callback`return true`，就不再执行。很多时候，就不需要forEach进行遍历了。*

---------------

## 5. every

### 是否所有的项都合乎条件,区别于 `some`

`arr.every(callback, [thisObject]);`

    function test(value) {
        if(value > 3) return true;
    }
    if(arr.every(test)) {
        console.log('yes');
    } else {
        console.log('no');   //no
    }

-----------------

## 6. indexOf

### 类似于`string.indexOf(str, position)`

`arr.indexOf(elem, [fromIndex])`

###### 返回整数索引值，如果没有*严格匹配*，返回-1. `fromIndex`可选，便是从这个位置开始搜索，如果缺省或格式不符合要求，使用默认值0，字符串数值也是可以的。如3和'3'。

    arr.indexOf(2, 'a'); //2  'x'被忽略
    arr.indexOf(2, '3'); //-1 从第3个位置开始找，未找到2。
    arr.indexOf('2', 0);//-1  因为2 !== '2'

-------------------

## 7. lastIndexOf

`arr.lastIndexOf(elem, [fromIndex]);`

###### 从数组的末尾开始查找，而不是开头。`fromIndex`值默认为`array.length - 1` 而不是`0`

    [0,1,2,1,0].lastIndexOf(0);  //4
    [0,1,2,1,0].lastIndexOf(1, 3); //3

----------------

## 8. reduce

### 类似迭代、递归

`arr.reduce(function(previous, current, index, array){}, [initialValue]);`

######  `initialValue`为初始值，可选。若指定，则当作最初使用的`previous`值，如果缺省，则使用数组的第一个元素作为`previous`初始值，同时current值往后排一位，相比有`initialValue`少一次迭代。

    var sum = [1, 2, 3, 4].reduce(function(pre, curr, index, array) {
        return pre + curr;
    });
    console.log(sum);  //10

*注：有了`reduce`，我们可以实现二维数组的扁平化*

    var matrix = [[1, 2], [3, 4], [5, 6]];
    var flatArr = matrix.reduce(function(pre, curr){
        return pre.concat(curr);
    });
    console.log(flatArr); //[1, 2, 3, 4, 5, 6]


------------------


## 9. reduceRight

### 与`reduce`类似，差异在于`reduceRight`从末尾项开始实现

`arr.reduceRight(function(pre, curr, index, array){}, [initialValue]);`

    var value = [1, 2, 3, 4].reduceRight(function(pre, curr, index) {
        if(index == 0) {
            return pre - curr;
        } else {
            return pre + curr;    
        }
    });
    console.log(value);  
    // index = 3  pre = 4  curr = 3
    // index = 2  pre = 7  curr = 2
    // index = 1  pre = 9  curr = 1
    // index = 0  pre = 8  curr = undefined(退出)

-------------


*参考：[ES5中新增的Array方法详细说明](http://www.zhangxinxu.com/wordpress/2013/04/es5%E6%96%B0%E5%A2%9E%E6%95%B0%E7%BB%84%E6%96%B9%E6%B3%95/)*
