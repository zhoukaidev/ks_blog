## 简介

多线程环境中，并发访问同一块内存是很常见的情况，有的线程想要修改内容，有的线程想读取内容， 此时对内存采用互斥访问策略就很重要。
比如当一个线程正在修改该内存中的内容的时候，其他线程应该等待该线程完成工作才可以去读取或者修改同一块内容。

举一个简单的例子，例如用户可以提交多个任务给后台程序处理，后台程序需要监控目前的任务数量，例如每个用户排队的任务数量不可以多余10个，此时任务计数器需要被用户修改，在任务被完成之后，也需要修改计数器，此时计数器会被多个线程同时访问，不正确的编码方式，会导致计数器的数量不对。

### 例程

先考虑以下没有临界区保护的例子

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

var jobCount = 0

func IncreaseCount() {
	jobCount = jobCount + 1
}

func DecreaseCount() {
	jobCount = jobCount - 1
}

func main() {
	//我们假设已经提交了100000个任务
	jobCount = 100000
	var wg sync.WaitGroup

	//启动100000个协程来处理任务
	for i := 0; i < 100000; i++ {
		threadId := i
		wg.Add(1)
		go func(id int) {
			fmt.Printf("%d: start process job\n", id)
			//模拟处理每个任务使用了一秒钟
			time.Sleep(1 * time.Second)
			DecreaseCount()
			wg.Done()
		}(threadId)
	}
	//确保所有协程都正常退出
	wg.Wait()
	fmt.Printf("剩余的job数量:%d", jobCount)
}
```
为了让以上代码的问题更容易暴漏出来，我们假设提交了100000个任务，其实这也是一个很常见的问题，在多线程环境中，代码存在潜在的内存竞争问题，但是这种问题在实际运行过程中并不是那么容易被暴露出来，如同`墨菲定律`说的一样，任何可能出错的事情最终一定会出错，这种临界区问题往往平常不会出现问题，在最关键的时刻会暴露出来，比如一个购物网站，平常访问的客户不过，产品运行一直不会出现问题，某天开始打折促销，大批量用户同一时刻突然去购买，这种最关键的节点，往往该问题就会暴露出来，影响销售活动。

我们提交了100000个任务，同时启动了100000个协程来处理，每个协程退出的时候会对jobCount减1，我们希望最终得到的剩余的job数量应该是0，但因为存在临界区访问的问题，我们可能会发现最终打印的剩余的job数量并不是0

### 互斥锁

早上上述问题的主要原因是多个线程在同时访问临界区，参考以下流程：

1. 比如当前jobCount的值是100
2. 1号线程读取jobCount的值是100
3. 2号线程读取了jobCount的值也是100
4. 1号线程对jobCount值减一，此时jobCount为99
5. 2号线程之前读取了jobCount的值是100， 所以也执行减一动作，jobCount也是99
6. 1，2号线程完成工作退出
7. 我们会发现1，2线程都退出之后，因为临界区问题，jobCount并没有变成预想的98，而是99

通过添加互斥锁，保证每次只能有一个线程访问理解去便可以解决这个问题，go提供了`Mutex`和`RWMutext`两种互斥锁，可以根据情况选择使用。


```go
package main

import (
	"fmt"
	"sync"
	"time"
)

var jobCount = 0
var mtx sync.Mutex

func IncreaseCount() {
	jobCount = jobCount + 1
}

func DecreaseCount() {
	//访问临界区之前先上锁
	mtx.Lock()
	//函数完成之后，释放锁
	defer mtx.Unlock()
	jobCount = jobCount - 1
}

func main() {
	//我们假设已经提交了100000个任务
	jobCount = 1000
	var wg sync.WaitGroup

	//启动100000个协程来处理任务
	for i := 0; i < 1000; i++ {
		threadId := i
		wg.Add(1)
		go func(id int) {
			fmt.Printf("%d: start process job\n", id)
			//模拟处理每个任务使用了一秒钟
			time.Sleep(1 * time.Second)
			DecreaseCount()
			wg.Done()
		}(threadId)
	}
	//确保所有协程都正常退出
	wg.Wait()
	fmt.Printf("剩余的job数量:%d", jobCount)
}

```

使用`Mutex`访问临界区之后，我们能够发现，所有线程退出之后，剩余的job数量一直是0