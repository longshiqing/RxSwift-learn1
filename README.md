##1.0 RxSwift-learn1
#创建序列 Observable：
* `asObservable` 返回一个序列
* `create` 使用 Swift 闭包的方式创建序列
* `deferred` 只有在有观察者订阅时，才去创建序列
* `empty` 创建一个空的序列，只发射一个 .Completed
* `error` 创建一个发射 error 终止的序列
* `toObservable` 使用 SequenceType 创建序列
* `interval` 创建一个每隔一段时间就发射的递增序列
* `never` 不创建序列，也不发送通知
* `just` 只创建包含一个元素的序列。换言之，只发送一个值和 .Completed
* `of` 通过一组元素创建一个序列
* `range` 创建一个有范围的递增序列
* `repeatElement` 创建一个发射重复值的序列
* `timer` 创建一个带延迟的序列
* `generate` 是创建一个可观察sequence，当初始化的条件为true的时候，他就会发出所对应的事件
* `do`    主要用于在subscribe中onNext，onError，onCompleted前调用
         
2、
#初学RxSwift的一些代码总结，持续更新
