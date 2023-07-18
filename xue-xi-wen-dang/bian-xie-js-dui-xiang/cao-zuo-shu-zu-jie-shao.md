# 操作数组介绍

本文档将介绍在PagePlug中常用的数组方法，下面提供一些简单的案例介绍



## 1、使用Lodash

PagePlug默认装载了 Lodash。Lodash 是一个一致性、模块化、高性能的 JavaScript 实用工具库。下面给出一些使用 Lodash 库的方法操作数组的示例，若您想要了解更多操作，请参阅 [Lodash 文档](https://www.lodashjs.com/)。

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

| 方法                        | 介绍                               | 示例                                              |
| ------------------------- | -------------------------------- | ----------------------------------------------- |
| \_.head(array)            | 返回数组的第一个元素                       | ![](<../../.gitbook/assets/image (16) (1).png>) |
| \_.last(array)            | 返回数组最后一个元素                       | ![](<../../.gitbook/assets/image (3) (2).png>)  |
| \_.nth(array, n)          | 获取第 n 个元素，n 可以为负数(例如取第三个)        | ![](<../../.gitbook/assets/image (7) (1).png>)  |
| \_.chunk(array, size)     | 将数组拆分成多个长度为 `size` 的小数组，小数组构成新数组 | ![](<../../.gitbook/assets/image (4) (1).png>)  |
| \_.uniq(array)            | 去重数组                             | ![](<../../.gitbook/assets/image (13) (1).png>) |
| \_.initial(array)         | 删除数组最后一个元素                       | ![](<../../.gitbook/assets/image (2) (2).png>)  |
| \_.pull(array, \[values]) | 移除数组 `array`中所有和`[values]` 相等的元素 | ![](<../../.gitbook/assets/image (17).png>)     |
| \_.tail(array)            | 删除数组第一个元素                        | ![](<../../.gitbook/assets/image (5) (1).png>)  |



## 2、常用的数组操作方法

在PagePlug中可以编写JS表达式来操作数组

| 方法          | 介绍                              | 示例                                              |
| ----------- | ------------------------------- | ----------------------------------------------- |
| `.length`   | 返回数组的长度                         | ![](<../../.gitbook/assets/image (18).png>)     |
| `.join`     | 将数组中的元素组合成字符串，分隔符可以自定义(通常为空格)   | ![](<../../.gitbook/assets/image (16).png>)     |
| `.indexOf`  | 返回数组中指定值第一次出现的索引                | ![](<../../.gitbook/assets/image (8) (1).png>)  |
| `.map`      | 返回一个新数组，其中包含对原始数组的每个元素运行指定函数的结果 | ![](<../../.gitbook/assets/image (11) (1).png>) |
| `.filter`   | 返回一个新数组，其中包含原始数组中匹配指定条件的元素      | ![](<../../.gitbook/assets/image (12) (1).png>) |
| `.includes` | 如果数组包含传递给方法的值，则返回true或false     | ![](<../../.gitbook/assets/image (14) (1).png>) |
| `.reduce`   | 通过为数组的每个值（从左到右）运行函数，将数组缩减为单个数值  | ![](<../../.gitbook/assets/image (10) (1).png>) |
| `.concat`   | 合并 2 个或多个数组                     | ![](<../../.gitbook/assets/image (15) (1).png>) |
