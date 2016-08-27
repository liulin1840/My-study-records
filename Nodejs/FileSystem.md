##FileSystem简介

文件系统模块是一个简单包装的标准 **POSIX** 文件 **I/O** 操作方法集。您可以通过调用`require('fs')`来获取该模块。文件系统模块中的所有方法均有异步和同步版本。

##fs.open(path, flags, [mode], callback)

fs.open(path, flags, [mode], callback)
*   path : 要打开的文件的路径
*   flags : 打开文件的方式 读/写
*   mode : 设置文件的模式 读/写/执行  4/2/1
*   callback : 回调
    * err : 文件打开失败的错误保存在err里面，如果成功err为null
    * fd : 被打开文件的标识，和定时器

```js
fs.open('1.txt', 'r', function(err, fd) {

    //console.log(err);
    //console.log(fd);

    if (err) {
        console.log( '文件打开失败' );
    } else {
        console.log( '文件打开成功' );
        console.log( fd );
    }

});
```

##fs.read(fd, buffer, offset, length, position, callback)

*   fd : 通过open方法成功打开一个文件返回的编号
*   buffer : buffer对象
*   offset : 新的内容添加到buffer中的起始位置
*   length ： 添加到buffer中内容的长度
*   position ：读取的文件中的起始位置
*   callback : 回调
    * err
    * uffer的长度
    * buffer对象

```js
fs.open('1.txt', 'r', function(err, fd) {
    if (err) {
        console.log('文件打开失败');
        console.log(err);
    } else {
        var bf1 = new Buffer('123456789');
        fs.read( fd, bf1, 0, 4, null, function( err, len, newBf ) {
            console.log( newBf );
        } );
    }
});

```
##fs.write(fd, buffer, offset, length[, position], callback)

 * fs.write(fd, buffer, offset, length[, position], callback)
 *   fd : 打开的文件
 *   buffer : 要写入的数据
 *   offset : buffer对象中要写入的数据的起始位置
 *   length : 要写入的buffer数据的长度
 *   position : fd中的起始位置
 *   callback : 回调
     * err:错误信息，没有就显示`null`
     * written:表明传入的`string`需要写入的字符串的字节长度
     * string:表明传入的字符串

```js
fs.write( fd, bf, 0, 3, 5, function() {
            console.log(arguments);
        } )
```

另一种写法：

**fs.write(fd, data[, position[, encoding]], callback)**

```js
fs.write(fd, '1234aqws你好', 0, 'utf-8', function(err, written, string) {
            console.log("ok");
            console.log(err);
            console.log(written);
            console.log(string);
});
```

操作结束后，要关闭打开的文件。

```js
fs.close(fd, function() {

});
```