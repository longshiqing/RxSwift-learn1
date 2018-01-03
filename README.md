RxSwift入门：
======

创建序列 Observable：
-----
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
         
什么是 `Subject`
-----
* `PublishSubject`：可以不需要初始来进行初始化（也就是可以为空），并且它只会向订阅者发送在订阅之后才接收到的元素。
* `BehaviorSubject`：需要一个初始值来进行初始化，因为比起PublishSubject，它会为订阅者发送订阅前接收到的最后一个元素，当然，新事件也会发送。
* `ReplaySubject`：初始化的时候要指定一个缓冲区的大小，而它会维持一个指定大小的数组来保存最近的元素，当有订阅者订阅了，它会首先向订阅者发送该缓冲区内的元素。然后当有新的元素加入，也会发送给订阅者。
* `Variable`：这是一个不太一样的Subject，它实际上等同于包了一层BehaviorSubject，它里面有一个value属性等同于最近接收的一个元素，但是它本身不继承自Observable。需要调用它自带的asObservable()方法进行转化后才能被订阅。

序列变化
-----      
* `map` 就是用你指定的方法去变换每一个值，这里非常类似 Swift 中的 map ，特别是对 SequenceType 的操作，几乎就是一个道理。一个一个的改变里面的值，并返回一个新的 functor 
* `mapWithIndex` 操作符与takeWhile很相似, takeWhile是返回了true或false, 而mapWithIndex 在返回真假的同时还能进行传进来的值得操作
* `flatmap` map、flatMap用于把流内容映射成新的内容，但flatMap用于其内容还是流事件
* `scan` 应用一个 accumulator (累加) 的方法遍历一个序列,最终发射多个最终累加值
* `reduce` 会在序列结束时才发射最终的累加值。最终只发射一个最终累加值
* `filter` 根据自身需求过滤掉一些不用的值
* `distinctUntilChanged` 用于当下一个事件与前一个事件是不同事件的事件才进行处理操作
* `elementAt` 处理在指定位置的事件 索引从0开始
* `take` 只处理前几个信号
* `takeLast` 只处理前几个信号,这里要注意，使用 takeLast 时，序列一定是有序序列，takeLast 需要序列结束时才能知道最后几个是哪几个值。所以 takeLast 会等序列结束才向后发射值。如果你需要舍弃前面的某些值，你需要的是 skip 。
* `takeWhile` 满足条件才处理 一旦不满足即使后面出现满足的条件也不会发出事件了
* `takeuntil` 接收事件消息，直到另一个sequence发出事件消息的时候才终止
* `skip` 忽略前面几次事件
* `skipWhile` 忽略开始满足条件的,如果碰到不满足条件的，后面的全部输出
* `skipWhileWithIndex` 满足条件的都被取消，传入的闭包同skipWhile有点区别而已,如果碰到不满足条件的，后面的全部输出
* `skipUntil` 直到某个sequence发出了事件消息，才开始接收当前sequence发出的事件消息
* `toArray` 将sequence转换成一个array，并转换成单一事件信号，然后结束
* `concat` concat会把多个sequence和并为一个sequence，并且当前面一个sequence发出了completed事件，才会开始下一个sequence的事件。
* `buffer` 在特定的线程，定期定量收集序列发射的值，然后发射这些的值的集合。
* `window` window 和 buffer 非常类似。唯一的不同就是 window 发射的是序列， buffer 发射一系列值
* `debounce` debounce 和 throttle 是同一个东西,仅在过了一段指定的时间还没发射数据时才发射一个数据，换句话说就是 debounce 会抑制发射过快的值。注意这一操作需要指定一个线程。
* `single` 就是抽样操作，按照 sample 中传入的序列发射情况进行抽样
* `startWith` 在一个序列前插入一个值
* `combineLatest` 当两个序列中的任何一个发射了数据时，combineLatest 会结合并整理每个序列发射的最近数据项。
* `zip` zip 和 combineLatest 相似，不同的是每当所有序列都发射一个值时， zip 才会发送一个值。它会等待每一个序列发射值，发射次数由最短序列决定。结合的值都是一一对应的。
* `merge` 会将多个序列合并成一个序列，序列发射的值按先后顺序合并。要注意的是 merge 操作的是序列，也就是说序列发射序列才可以使用 merge 。
* `switchLatest` switchLatest 和 merge 有一点相似，都是用来合并序列的。然而这个合并并非真的是合并序列。事实是每当发射一个新的序列时，丢弃上一个发射的序列。
* `amb` 用来处理发射序列的操作，不同的是， amb 选择先发射值的序列，自此以后都只关注这个先发射序列，抛弃其他所有序列。


可连接的观察者序列：
-----
  可连接的观察者序列（Connectable observables）是观察者序列中特殊的一个类。不管订阅者的数量多少，他们并不会发送任何的元素，一直到你调用观察者序列的connect()方法。记住：对于一些操作符，如果返回 ConnectableObservable<E>而不是Observable<E>，那么就需要执行调用connect()方法
可连接的序列和一般的序列基本是一样的，不同的就是你可以用可连接序列调整序列发射的实际。只有当你调用 connect 方法时，序列才会发射。比如我们可以在所有订阅者订阅了序列后开始发射。下面的几个例子都是无限执行的，你可以自行调用每个函数感受不同的操作的结果。
* `replay(_:)` 创建了一个新的观察者序列，根据缓存值的大小，用来记录由源观察者序列最后发送的几个元素。每一次新的观察者进行订阅，它将立马接受到缓冲中的元素（如果缓冲中有内容），而且保持接受最新的元素。就像一个正常的订阅者一样。返回的是可连接的观察者序列（connectable observable）。shareReplay 就相当于将 replay 中的参数设置为无限大，可以解决多个订购者多次发送序列问题
* `replayAll()` 一旦有新的订阅者将立马发送缓冲中的元素.这个操作符使用需要注意：使用的情景是你需要知道全部的缓冲元素的个数并且将保持合理化。使用replayAll()在序列中，可能不会终止而且产生许多的数据将迅速的阻塞你的内存。
* `multicast(_:)` 将一个正常的sequence转换成一个connectable sequence，并且通过具体的subject发送出去，比如PublishSubject，或者replaySubject，behaviorSubject等，不同的Subject会有不同的结果(Converts the source Observable sequence into a connectable sequence, and broadcasts its emissions via the specified subject.)
* `publish()` 将一个普通序列转换成Connectable Observable序列，订阅观察者序列之后并没有发送事件，一直到调用connect()方法，connect()方法将激活可连接的观察者序列（connectable observable），并且连接的观察者序列发送事件给所有的订阅者。所以得到以上结果
         
            **订阅观察者序列之后并没有发送事件，一直到调用connect()方法，connect()方法将激活可连接的观察者序列（connectable observable），并且连接的观察者序列发送事件给所有的订阅者。所以得到以上结果，当序列发送元素之后，你将经常需要确保将来的新的订阅者接受一些或者所有过去的元素。这时候我们就需要replay(_:)和replayAll()这两个操作符。确保所有的订阅者都能够获得相同的观察者序列发送的元素，即使是在观察者序列已经开发发送元素之后开始订阅的。**



Refcount : 这个是一个可连接序列的操作符。它可以将一个可连接序列变成普通的序列。

感激
感谢以下的大牛,排名不分先后

* [靛青K](http://t.swift.gg/d/2-rxswift) 
* [王巍](https://onevcat.com)

关于作者

```javascript
  var ihubo = {
    nickName  : "冷冻残阳",
    site : "http://blog.csdn.net/longshiqing14/"
  }
 ```
 
 
