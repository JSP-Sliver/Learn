exports和module.exports

根据使用方法来说
通常exports的使用方法为：
exports [function name]=[function name]

module.exports使用方法为：
module.exports=[function name]

这样使用两者的根本区别是：
exports返回的是模块函数
module.exports返回的是模块对象本身，是一个类


使用上的区别：
export的方法可以直接调用
module.exports的方法需要new对象之后才能调用

深度好文，建议学习
https://www.cnblogs.com/cangqinglang/p/8336754.html