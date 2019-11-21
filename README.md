## chameleon分包加载

**首先更新 chameleon-tool@1.0.4-alpha.1**

### 0 理解微信小程序分包策略

比如生成的 app.json 中配置如下:

```javascript
{
  "pages":[
    "pages/index",
    "pages/logs"
  ],
  "subpackages": [
    {
      "root": "packageA",
      "pages": [
        "pages/cat",
        "pages/dog"
      ]
    }, {
      "root": "packageB",
      "name": "pack2",
      "pages": [
        "pages/apple",
        "pages/banana"
      ]
    }
  ]
}

```
* 小程序主包体积和分包体积的计算方式：
  - 所有在不在 packageA packageB 中的体积才不会被计算到主包里；
  - packageA packageB 文件夹下的体积为对应的分包的体积
* 同时需要注意：
  - 主包不能引用分包的组件 
  - 分包可以引用主包的组件 
  - 分包不能引用分包的组件

了解了以上基本信息，我们来看下 chameleon 中的分包配置

### 1 app.cml中分包配置 

```javascript
"subPackages":[{
  "root":"pages/subpage",
  "pages":[
      "page1/page1"
    ]
  },
  {
    "root":"subpage2",
    "pages":[
      "page2/page2"
    ]
  }
]
```

**建议如果不是公用组件，那么久将其放到分包文件夹下面，而不是全部都将组件声明在src/components中，具体参考subpackdemo**



### 2 