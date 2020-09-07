# KotlinCoroutinesDemo
Kotlin协程Flow

#### Flow创建
flow 创建一个Flow流 类似RxJava的Observable
emit函数 向下游发送数据
```
flow{
    emit(1)
}
```
快捷方法 flowOf 类似RxJava的 just操作符
自动向下游发送数据 内部封装的还是原先的emit函数
     
```
public fun <T> flowOf(vararg elements: T): Flow<T> = flow {
    for (element in elements) {
        emit(element)
        
    }
}
```
数组集合提供了拓展函数 asFlow
```
arrayOf(1,2,3).asFlow()
listOf(1,2,3).asFlow()
```
     
collect 对应 RxJava的subscribe订阅方法 也就是下游 用于消费数据
     
线程切换 flowOn 数据上游的线程
     
下游线程切换 默认就是 launch时的调度器
     
异常处理 catch
     
完成回调 onCompletion
     
#### Flow 特性
1. 冷流 (懒加载) 只有collect的时候 数据才会进行发射 创建时不会进行数据操作
2. 有序 自上而下顺序传递
3. 可取消
     
#### 操作符

- map 数据类型转换操作
- take
- filter 数据过滤操作符

     
- buffer 数据发射并发
- collect 不并发
- conflate 数据发射太快,只处理最新发射的
- collectLatest 接收处理太慢,只处理最新接收的

     
- zip 组合两个流 双方都有新数据是才会发射处理
- combine 组合两个流 在经过第一次发射后,任意方有新数据来的时候就可以发射,另一方有可能是已经发射过的数据

     
- flatMapConcat 串行处理数据
- flatMapMerge 并发collect数据
- flatMapLatest 每次emit新数据后会取消前面的collect


- collect
- toList 转List集合
- toSet 转Set集合
- first 取第一个值
- single 确保流发射单个值
- reduce 如果发射的是int 最终会得到一个int 可以累加操作
- fold reduce拓展 可以自定义返回类型
