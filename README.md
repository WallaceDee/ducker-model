<h1 align="center">Welcome to ducker 👋</h1>
<p>
  <img src="https://img.shields.io/badge/version-0.0.1-blue.svg?cacheSeconds=2592000" />
  <img src="https://badgen.net/badgesize/normal/https://raw.githubusercontent.com/simplefeel/ducker-model/master/dist/ducker.es5.js">
</p>

> 数据转换器，解耦前后端开发，提升开发效率

## Motivation

✅ why we need ducker-model ? see the [article](https://mp.weixin.qq.com/s/q6xybux0fhrUz5HE5TY0aA)

## Install

[![NPM](https://nodei.co/npm/ducker-model.png)](https://nodei.co/npm/ducker-model/)

## Usage

```js
// 1.初始一个model实例，传入数据结构属性定义
let userModel = new Model({
  id: {
    type: Number,
    property: "uuid",
    value: 0,
    computed: function(value) {
      return value * 10;
    }
  },
  name: {
    type: String,
    property: "buyer.shopinfo.nickname",
    value: ""
  },
  lastLoginTime: {
    type: Date,
    property: "lastLoginTime",
    format: "kk"
  },
  price: {
    type: Number,
    unit: "B",
    property: "price"
  },
  flag: {
    type: Number,
    property: ["uuid", "price"],
    computed: function(args) {
      let result = 0;
      for (let i = 0; i < args.length; i++) {
        result += args[i];
      }
      return result;
    }
  }
});

// 2.实例调用parse()方法解析数据
let userState = userModel.parse({
  uuid: 123,
  buyer: {
    shopinfo: {
      nickname: "张三"
    }
  },
  price: 1000,
  lastLoginTime: "1563897600000"
});
// userState--> {"id":1230,"name":"张三","lastLoginTime":"2019年07月24日 00点00分","price":"10.00","flag":1123}

// --------或者----------

// 3.实例调用traverse()方法反向映射数据
let userParams = userModel.traverse({
  id: 234,
  name: "李四",
  age: null,
  lastLoginTime: "2019-07-24",
  price: 24
});
// userParams--> {"uuid":234,"buyer":{"shopinfo":{"nickname":"李四"}},"lastLoginTime":1563897600000,"price":2400}
```

## API 说明

1. **type**为**Date**的属性，增加**format**字段，支持多种内置数据格式，默认为"l",可以选择的格式如下：

   - "l": "YYYY-MM-DD",
   - "ll": "YYYY 年 MM 月 DD 日",
   - "k": "YYYY-MM-DD hh:mm",
   - "kk": "YYYY 年 MM 月 DD 日 hh 点 mm 分",
   - "kkk": "YYYY 年 MM 月 DD 日 hh 点 mm 分 q",
   - "f": "YYYY-MM-DD hh:mm:ss",
   - "ff": "YYYY 年 MM 月 DD 日 hh 点 mm 分 ss 秒",
   - "fff": "YYYY 年 MM 月 DD 日 hh 点 mm 分 ss 秒 星期 w",
   - "n": "MM-DD",
   - "nn": "MM 月 DD 日"
   
2. 添加了**unit**字段的，代表该属性值表示一个价格，模型内置**十、百、千、万**单位，可以快捷的将价格字段进行转换，例如1000 -> 100

3. 属性定义增加**computed**，值为函数，可以用来自定义数据格式化处理

4. **property**，值可以为一个数组，传入多个路径，此时可以通过定义 **computed** 方法来组合计算值

## Author

👤 **skinner**

- Github: [@simplefeel](https://github.com/simplefeel)

## Show your support

Give a ⭐️ if this project helped you!

