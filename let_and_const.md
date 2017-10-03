## let

let聲明的變量只在它所在的代碼塊有效。

```javascript
var a = [];

for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}

a[6](); // 10
```

上面代碼中，變量i是var命令聲明的，在全局範圍內都有效，所以全局只有一個變量i。<br />
每一次循環，變量i的值都會發生改變，而循環內被賦給數組a的函數內部的console.log(i)，裡面的i指向的就是全局的i。<br />
也就是說，所有數組a的成員裡面的i，指向的都是同一個i，導致運行時輸出的是最後一輪的i的值，也就是10。

如果使用let，聲明的變量僅在塊級作用域內有效，最後輸出的是6。

```javascript
var a = [];

for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}

a[6](); // 6
```

上面代碼中，變量i是let聲明的，當前的i只在本輪循環有效，所以每一次循環的i其實都是一個新的變量，所以最後輸出的是6。<br />
你可能會問，如果每一輪循環的變量i都是重新聲明的，那它怎麼知道上一輪循環的值，從而計算出本輪循環的值？這是因為 JavaScript 引擎內部會記住上一輪循環的值，初始化本輪的變量i時，就在上一輪循環的基礎上進行計算。

另外，for循環還有一個特別之處，就是設置循環變量的那部分是一個父作用域，而循環體內部是一個單獨的子作用域。

```javascript
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}

// abc
// abc
// abc
```

上面代碼正確運行，輸出了3次abc。這表明函數內部的變量i與循環變量i不在同一個作用域，有各自單獨的作用域。


### 不存在變量提升

```javascript
// var 的情况
console.log(foo); // 輸出undefined
var foo = 2;

// let 的情况
console.log(bar); // 報錯ReferenceError
let bar = 2;
```