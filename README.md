
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
         
#什么是 `Subject`
* `PublishSubject`：可以不需要初始来进行初始化（也就是可以为空），并且它只会向订阅者发送在订阅之后才接收到的元素。
* `BehaviorSubject`：需要一个初始值来进行初始化，因为比起PublishSubject，它会为订阅者发送订阅前接收到的最后一个元素，当然，新事件也会发送。
* `ReplaySubject`：初始化的时候要指定一个缓冲区的大小，而它会维持一个指定大小的数组来保存最近的元素，当有订阅者订阅了，它会首先向订阅者发送该缓冲区内的元素。然后当有新的元素加入，也会发送给订阅者。
* `Variable`：这是一个不太一样的Subject，它实际上等同于包了一层BehaviorSubject，它里面有一个value属性等同于最近接收的一个元素，但是它本身不继承自Observable。需要调用它自带的asObservable()方法进行转化后才能被订阅。
