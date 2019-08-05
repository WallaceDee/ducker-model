<h1 align="center">Welcome to ducker 👋</h1>
<p>
  <img src="https://img.shields.io/badge/version-0.0.1-blue.svg?cacheSeconds=2592000" />
  <img src="https://badgen.net/badgesize/normal/https://raw.githubusercontent.com/simplefeel/ducker-model/master/dist/ducker.es5.js">
</p>

> Data converter, decoupling front and rear development, improving development efficiency 数据转换器，解耦前后端开发，提升开发效率

## Motivation
❓why we need ducker-model ? see the [article](https://mp.weixin.qq.com/s/q6xybux0fhrUz5HE5TY0aA) 

## Install
[![NPM](https://nodei.co/npm/ducker-model.png)](https://nodei.co/npm/ducker-model/)

## Usage

```js
// 1.初始一个model实例，传入数据结构属性定义
let userModel = new Model({
  id: {
    type: Number,
    property: "uuid",
    value: 0
  },
  name: {
    type: String,
    property: "buyer.shopinfo.nickname",
    value: ""
  },
  items: {
    type: String,
    property: "items"
  },
  age: {
    type: Number,
    property: "age"
  },
  lastLoginTime: {
    type: Date,
    property: "lastLoginTime"
  },
  price: {
    type: Number,
    unit: "B",
    property: "price"
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
// userState--> {"id":123,"name":"张三","items":"","age":0,"lastLoginTime":"2019-07-24","price":10}

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

## Author

👤 **skinner**

- Github: [@simplefeel](https://github.com/simplefeel)

## Show your support

Give a ⭐️ if this project helped you!

---

_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_
