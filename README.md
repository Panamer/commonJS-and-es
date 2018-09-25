# commonJS-and-es
exports、module.exports和export、export default到底是咋回事
```
https://segmentfault.com/a/1190000010426778
https://www.cnblogs.com/fayin/p/6831071.html

举个例子：

我新建一个fuck.test.js，Nodejs 中我引入（require）了一个 es6 写的类库用来测试。但这个类都是使用 export default { ... } 的方式导出的。

前面说过，Nodejs 是不支持 export 的。所以会报错。不仅如此，如果该es6类库还使用了 import 语法引入了其他库。更加会报错。因为nodejs不支持import。

解决方案是什么呢？有没有想过，为什么其他第三方库可以正常引入无论是es6还是nodejs？这需要套路！

套路：  先不考虑其他第三方是如何做到的。我们先自己约束和规范好。

譬如说，引入文件的方式使用双方通用的require！

但导出怎么办？双方似乎没有协同点？没关系。我们可以从 es6 + webpack + babel 入手： http://npm.taobao.org/package/babel-plugin-transform-es2015-modules-commonjs

下载并且使用这个babel插件：在,babelrc的plugins中加入代码： "plugins": ["transform-es2015-modules-commonjs"]

然后，我们的es6代码就支持 module.exports 了。这样一来，我们的导出统一使用 module.exports （需要babel插件支持）即可！

总而言之一句话：导入用require, 导出用module.exports 


```
# ps: 不知从什么时候开始，es6居然已经支持module.exports了
