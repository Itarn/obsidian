### 一、基础概念

-   bit:

	-   计算机中的最小存储单元
	-   存储内容总是0或1

	-   所有二进制状态的实体都可以使用1bit表示
	-   8bits组成1byte

	-   不能够单独寻址

-   byte：

	-   1byte包含8bits
	-   可以存储所有ASCII所有字符（这是它包含8bits的初衷）

	-   十进制整数范围[-128,127]或[0, 255] 2的n次方-1
	-   最小的可寻址存储单元

  

### 二、js 操作二进制 API 介绍

-   **ArrayBuffer**

-   代表内存之中的一段二进制数据，可以通过“视图”进行操作。“视图”部署了数组接口，这意味着，可以用数组的方法操作内存。
```js
// 参数代表字节数量
// 构造函数，可以分配一段可以存放数据的连续内存区域
const buf = new ArrayBuffer(1);
```

-   **TypedArray**

-   共包括 9 种类型的视图，比如`Uint8Array`（无符号 8 位整数）数组视图, `Int16Array`（16 位整数）数组视图, `Float32Array`（32 位浮点数）数组视图等等。

```js
const buf = new ArrayBuffer(1);

// 举例，用为 TypedArray 类型的 Uint8Array 构造函数来读写
const x1 = new Uint8Array(buffer);
x1[0]=2;
x1[0] // 2
```

-   **DataView**

-   可以自定义复合格式的视图，比如第一个字节是 Uint8（无符号 8 位整数）、第二、三个字节是 Int16（16 位整数）、第四个字节开始是 Float32（32 位浮点数）等等，此外还可以自定义字节序。
-   制数据。

``` js
const buf = new ArrayBuffer(1);

// DataView
// DataView(ArrayBuffer, 字节起始位置?, 长度?);
const dv = new DataView(buffer);
```

简单说，`ArrayBuffer`对象代表原始的二进制数据，TypedArray 视图用来读写简单类型的二进制数据，`DataView`视图用来读写复杂类型的二进

[链接](https://www.bookstack.cn/read/es6/docs-arraybuffer.md)

  

### 三、protobuf 介绍

```js
message SearchRequest {
  // 字段规则 字段类型 字段名 = 分配标识符;
  required string query = 1;
  optional int32 page_number = 2;
  optional int32 result_per_page = 3;
}
```

1.从前端的角度理解 Protobuf

[https://zhuanlan.zhihu.com/p/138818472](https://zhuanlan.zhihu.com/p/138818472?utm_source=com.example.android.notepad)

2.[译]Protobuf 语法指南

[https://colobu.com/2015/01/07/Protobuf-language-guide/#%E5%AE%9A%E4%B9%89%E4%B8%80%E4%B8%AA%E6%B6%88%E6%81%AF%E7%B1%BB%E5%9E%8B](https://colobu.com/2015/01/07/Protobuf-language-guide/#%E5%AE%9A%E4%B9%89%E4%B8%80%E4%B8%AA%E6%B6%88%E6%81%AF%E7%B1%BB%E5%9E%8B)

3.protobufjs api

[https://github.com/protobufjs/protobuf.js](https://github.com/protobufjs/protobuf.js)

  

### 四、CRC 循环冗余校验

在数据传输过程中，无论传输系统的设计再怎么完美，差错总会存在，这种差错可能会导致在链路上传输的一个或者多个帧被破坏(出现比特差错，0变为1，或者1变为0)，从而接受方接收到错误的数据。为尽量提高接受方收到数据的正确率，在接收方接收数据之前需要对数据进行差错检测，当且仅当检测的结果为正确时接收方才真正收下数据。

实现原理文章

1.  [https://segmentfault.com/a/1190000018094567?utm_source=tag-newest](https://segmentfault.com/a/1190000018094567?utm_source=tag-newest)
2.  [https://baike.baidu.com/item/CRC/1453359](https://baike.baidu.com/item/CRC/1453359)