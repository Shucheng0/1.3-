## 链表（上）

#### [链表]([https://zh.wikipedia.org/wiki/%E9%93%BE%E8%A1%A8](https://zh.wikipedia.org/wiki/链表))：一种线性数据结构，通过“指针”将一组零散的内存串联起来，来存储数据。



组成链表各部分的称谓：

>* **节点**：每一个内存块称为链表的节点
>* **后继指针 next**：记录下一个节点地址的指针
>* **头节点**：习惯把第一个节点叫做头节点
>* **尾节点**：习惯把最后一个节点叫做尾节点。一个特殊的地方，指针不是指向下一个节点，而是指向一个**空地址 NULL**，表示这是链表上最后一个节点。



那问题来了，什么是线性表的数据结构呢？使用“指针”串联一组零散内存的意义在那里？为何能支持存储不同类型的数据呢？

| 问题                             | 回答                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| 什么是线性表的数据结构？         | 就是每个线表上的数据最多只有前、后两个方向                   |
| 什么是非线性表的数据结构呢？     | 不是简单的前后关系                                           |
| 使用“指针”串联一组零散内存的意义 | 插入、删除操作迅速                                           |
| 为何能支持存储不同类型的数据？   | 可能是，保存“指针”的内存可以单独“识别”出来。所以，不同节点之间跳转直接遍历节点的内存就好 |



线性表和非线性表差别，可以通过下图直观的看出：
<img src="https://static001.geekbang.org/resource/image/b6/77/b6b71ec46935130dff5c4b62cf273477.jpg" alt="线性表" style="zoom:33%;" />
<img src="https://static001.geekbang.org/resource/image/6e/69/6ebf42641b5f98f912d36f6bf86f6569.jpg" alt="非线性表" style="zoom:33%;" />



单链表的具体形式可以看下图：

​	<img src="https://static001.geekbang.org/resource/image/b9/eb/b93e7ade9bb927baad1348d9a806ddeb.jpg" alt="单链表" style="zoom:40%;" />



单链表的插入、删除、随机访问操作及程序：

<img src="https://static001.geekbang.org/resource/image/45/17/452e943788bdeea462d364389bd08a17.jpg" alt="单链表的插入、删除" style="zoom:33%;" />

```javascript
/**
 * 1）单链表的插入、删除、查找操作；
 * 2）链表中存储的是int类型的数据；
 */
class Node {
  constructor (element) {
    this.element = element
    this.next = null
  }
}
class LinkedList {
  constructor () {
    this.head = new Node('head')
  }
  // 根据value查找节点
  findByValue (item) {
    let currentNode = this.head.next
    while (currentNode !== null && currentNode.element !== item) {
      currentNode = currentNode.next
    }
    console.log(currentNode)
    return currentNode === null ? -1 : currentNode
  }
        
  // 指定元素向后插入
  insert (newElement, element) {
    const currentNode = this.findByValue(element)
    if (currentNode === -1) {
      console.log('未找到插入位置')
      return
    }
    const newNode = new Node(newElement)
    newNode.next = currentNode.next
    currentNode.next = newNode
  }
    
  // 根据值删除
  remove (item) {
    const prevNode = this.findPrev(item)
    if (prevNode === -1) {
      console.log('未找到元素')
      return
    }
    prevNode.next = prevNode.next.next
  }
}
```



#### 三种最常见的链表结构：

* 循环链表
  * 循环链表的尾节点指针指向链表的头节点
    * <img src="https://static001.geekbang.org/resource/image/86/55/86cb7dc331ea958b0a108b911f38d155.jpg" alt="循环链表内存示意图" style="zoom:33%;" />
  * 优点：从链尾到链头比较方便
* 双向链表
  * 每一个节点支持两个方向：前驱指针prev指向前面的节点，后继指针指向next指针。
    * <img src="https://static001.geekbang.org/resource/image/cb/0b/cbc8ab20276e2f9312030c313a9ef70b.jpg" alt="双向链表内存示意图" style="zoom:33%;" />
  * 缺点：占用更多空间
  * 优点：可以访问前一个节点。相较于单链表，除去耗内存之外，更加的高效。实际的开发中，使用的更加的广泛。（用空间换时间）
* 双向循环链表
  * <img src="https://static001.geekbang.org/resource/image/d1/91/d1665043b283ecdf79b157cfc9e5ed91.jpg" alt="双向循环链表内存分布图" style="zoom:33%;" />



#### 数组基本功能实现程序

```javascript
/**
 * 1）单链表的插入、删除、查找操作；
 * 2）链表中存储的是int类型的数据；
 */
class Node {
  constructor (element) {
    this.element = element
    this.next = null
  }
}

class LinkedList {
  constructor () {
    this.head = new Node('head')
  }
  // 根据value查找节点
  findByValue (item) {
    let currentNode = this.head.next
    while (currentNode !== null && currentNode.element !== item) {
      currentNode = currentNode.next
    }
    console.log(currentNode)
    return currentNode === null ? -1 : currentNode
  } 
  
  // 根据index查找节点，下标从0开始
  findByIndex (index) {
    let currentNode = this.head.next
    let pos = 0
    while (currentNode !== null && pos !== index) {
      currentNode = currentNode.next
      pos++
    }
    console.log(currentNode)
    return currentNode === null ? -1 : currentNode
  }

  // 向链表末尾追加节点
  append(newElement) {
    const newNode = new Node(newElement)
    let currentNode = this.head
    while(currentNode.next) {
      currentNode = currentNode.next
    }
    currentNode.next = newNode
  }
  
  // 指定元素向后插入
  insert (newElement, element) {
    const currentNode = this.findByValue(element)
    if (currentNode === -1) {
      console.log('未找到插入位置')
      return
    }
    const newNode = new Node(newElement)
    newNode.next = currentNode.next
    currentNode.next = newNode
  } 
  
  // 查找前一个
  findPrev (item) {
    let currentNode = this.head
    while (currentNode.next !== null && currentNode.next.element !== item) {
      currentNode = currentNode.next
    }
    if (currentNode.next === null) {
      return -1
    }
    return currentNode
  } 
  
  // 根据值删除
  remove (item) {
    const prevNode = this.findPrev(item)
    if (prevNode === -1) {
      console.log('未找到元素')
      return
    }
    prevNode.next = prevNode.next.next
  }
  
  // 遍历显示所有节点
  display () {
    let currentNode = this.head.next // 忽略头指针的值
    while (currentNode !== null) {
      console.log(currentNode.element)
      currentNode = currentNode.next
    }
  }
}
// Test
const LList = new LinkedList()
LList.append('chen')
LList.append('curry')
LList.append('sang')
LList.append('zhao') // chen -> curry -> sang -> zhao
console.log('-------------insert item------------')
LList.insert('qian', 'chen') // 首元素后插入
LList.insert('zhou', 'zhao') // 尾元素后插入
LList.display() // chen -> qian -> curry -> sang -> zhao -> zhou
console.log('-------------remove item------------')
LList.remove('curry')
LList.display() // chen -> qian -> sang -> zhao -> zhou
console.log('-------------find by item------------')
LList.findByValue('chen')
console.log('-------------find by index------------')
LList.findByIndex(2)
console.log('-------------与头结点同值元素测试------------')
LList.insert('head', 'sang')
LList.display() // chen -> qian -> sang -> head -> zhao -> zhou
LList.findPrev('head') // sang
LList.remove('head')
LList.display() // chen -> qian -> sang -> zhao -> zhou
```



相关章节：[链接](https://time.geekbang.org/column/article/41013)

相关程序：[链接](https://github.com/wangzheng0822/algo/blob/master/javascript/06_linkedlist/SinglyLinkedList.js)