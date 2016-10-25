# getin协议

# v0.1.0

## Overview

* 将复杂object序列化为url的通用协议。便于书写表达丰富的http-get请求。
* 协议名getin寓意从get方法中也可以取出丰富内容。

## Reference


## Documents

1. 协议核心描述。7条基本规则。
    1. xxx[_obj](#_obj)=... 表示xxx是一个对象
    2. xxx[_lis](#_lis)=... 表示xxx是一个数组
    3. xxx[_flt](#_flo)=... 表示xxx是一个浮点数
    4. xxx[_int](#_int)=... 表示xxx是一个整数
    5. 不能用[=](#=)号的地方用[~](#~)代替
    6. 不能用[&](#&)号的地方用[+](#+)代替
    7. 同级别的[键](#键)按从左到右的顺序读

## Examples
* 实例1:
```javascript
var sample = {
  limit: 10,
  skip: 20,
  sort: ["active", "create"],
  plat: "china",
  rate: 10.5
};

var sampleUrl = "?limit_int=10&skip_int=20&plat=china&sort_lis=active&sort_lis=create&rate_flt=10.5";
```

* 实例2:
```javascript
var sample = {
  plat: "china",
  key: {
    cate: "person",
    group: "social"
  }
};

var sampleUrl = "?plat=china&key_obj=cate~person&key_obj=group~social";
```

* 实例3，两个结果等价，但推荐长度较短的前者:
```javascript
var sample = {
  plat: "china",
  key: {
    class: ["music", "drawing"]
  }
};

var sampleUrl = "?plat=china&key_obj=class_lis~music+class_lis~drawing";
var sampleUrlAlias = "?plat=china&key_obj=class_lis~music&key_obj=class_lis~drawing";
```

* 实例4:
```javascript
var sample = {
  key: {
    magic: {
      name: "jack",
      method: {
        want: "jump"
      }
    }
  }
};

var sampleUrl = "?key_obj=magic_obj~name~jack+magic_obj~method_obj~jump";
```
