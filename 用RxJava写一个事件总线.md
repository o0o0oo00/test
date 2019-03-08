用RxJava写一个事件总线

有时候我们会想在两个界面之间互相通信，怎么说，就是后一个界面的行为会导致前一个界面的改变。

比如说，B页面的一个操作，会导致A页面的未读小红点消失。A怎么才能接收到B这个动作，进而把小红点消去呢？

通常的做法是：

onActivityResult、

或者本地记录一个变量，在onRestar()等生命周期中进行判断、

再或者就是EventBus来**通知**前一个页面做一些操作等等



现在我们用RxJava来**优雅的**实现这种需求，RxJava我们都知道，观察者模式！

那么我们到底观察的是什么呢？我们可不可以观察一个变量 ，当这个变量的值发生改变的时候，我们就去通知各个观察者，做出响应。



首先写一个用于观察的ObservableMap

就相当于是滴滴打车，有很多的订单，而这些订单与人绑定，

我们Map的key作为订单，来确定谁是乘车人，然后司机只需要接单，就可以去接乘客出发去目的地啦。

```kotlin
class ObservableMap<T, K> : HashMap<T, K>() {

    private var onChange: ((T) -> Unit)? = null

    override fun put(key: T, value: K): K? {
        val put = super.put(key, value)
        onChange?.invoke(key)
        return put
    }

    fun registerOnChange(change: (T) -> Unit) {
        this.onChange = change
    }

    fun unregisterOnChange() {
        this.onChange = null
    }
}
```



1、继承自HashMap<T,K> 然后重写它的put方法，每当有put操作发生的时候，也就是下单的时候，我们就去通知我们的滴滴平台，

用一个高阶函数，来将这个key传给Observable，让Observable来发射给观察者。

2、我们写一个滴滴平台用来分发专车订单：

每次发生put操作也就会生成一个订单，

定义一个Observable好让观察者来观察我，就是一个订单池，司机可以通过订单id来找到我，别管司机和乘客为什么知道订单 The KEY ，因为写代码的人让他俩同时知道的。

```kotlin
private val onBooleanChange = Observable.create<String> { emitter ->
        val onChange: (String) -> Unit = {
            emitter.onNext(it)
        }
        emitter.setCancellable {
            map.unregisterOnChange()
        }
        map.registerOnChange(onChange)
    }.share()
```



我们都知道当Observable在发生订阅关系的时候才会发射数据，所以我们写一个发生订阅的方法

```kotlin
fun observeBoolean(key: String): Observable<Boolean> = onBooleanChange
        .filter { it == key }
        .map { map[key] }
```

根据传进来的key作为唯一标识，也就是司机要知道是你打的专车，然后将对应的value发送给Observer观察者。司机拿着这个订单Key来匹配滴滴平台中的诸多订单**filter { it == key }**，当发现有匹配订单的时候，司机可以根据这订单来拿到乘客**.map { map[key] }**



我们看下面，这里为map进行了一次put操作，前面说到map进行操作put，然后高阶函数将key发射给Observable，由Observable来发射给各个观察者(司机)

 **map[key] = value**    就是   **map.put(key,value)**

```kotlin
fun setBoolean(key: String,  value: Boolean) {
        map[key] = value
    }
```

现在我要下单啦，一个订单**The KEY**，一个我，先别管我为什么是一个true，我也只是一个数据信息而已。

```kotlin
ObserverBooleanStatus.setBoolean(The KEY, true)
```

已经发送滴滴平台啦。静候司机大哥



既然已经将Observable写好了，那么理所当然我们马上就要去**subscribe**发生订阅关系了啦！

司机拿到了真正的订单**The KEY**，油门已经踩得嗡嗡响了，一旦乘客下单 订单号为The KEY，那么司机马上就可以接到乘客出发啦，最终目的地是sout。岂不美哉

```
 ObserverBooleanStatus.observeBoolean(The KEY)
            .subscribe { boolean -> 
               sout(boolean = $boolean)
            }
```





