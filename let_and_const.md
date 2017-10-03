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