## 双向链表
```javascript
  function Node(element) {
    this.element = element;
    this.prev = null; //比单向链表多一个prev
    this.next = null;
  }
  function DoubleLinkedList() {
    this.init()
  }
  DoubleLinkedList.prototype = {
    constructor: DoubleLinkedList,
    init: ()=> { //初始化
      this.length = 0;
      this.head = null;
      this.tail = null; //比单向链表多一个tail
    },
    append: (element)=> { //添加
      let node = new Node(element),
          current = this.tail

      if(this.head === null) { //链表为空
        this.head = node;
        this.tail = node;
      } else { //基于tail来添加
        node.prev = current;
        current.next = node;
        this.tail = node;
      }

      this.length++; //更新链表长度
    },
    remove: (position)=> { //删除特定位置的元素
      if(position < -1 && position > this.length) { //越界
        return null;
      } else {
        let current = this.head,
            previous,
            index = 0;

        if(position === 0) { //若删除head
          this.head = current.next;
          if(this.length === 1) { //链表长度为1
            this.tail = null;
          } else {
            this.head.prev = null;
          }
        } else if(position === this.length - 1) { //最后一个元素
          current = this.tail;
          this.tail = current.prev;
          this.tail.next = null;
        } else {
          while(index++ < position) { //查找到需要删除的元素
            previous = current;
            current = current.next;
          }

          previous.next = current.next;
          current.next.prev = previous;
        }

        this.length--;

        return current.element //返回删除的元素
      }
    },
    insert: (position, element)=> { //在特定位置插入一个元素
      if(position < 0 && position > this.length) { //越界
        return false
      } else {
        let node = new Node(element),
            current = this.head,
            previous,
            index = 0;

        if(position === 0) { //添加在head
          if(!this.head) { //链表为空
            this.head = node;
            this.tail = node;
          } else {
            node.next = current;
            current.prev = node;
            this.head = node;
          }
        } else if(position === this.length) { //最后一个元素之后插入
          current = this.tail;
          node.prev = current;
          current.next = node;
          this.tail = node;
        } else {
          while(index++ < position) {
            previous = current;
            current = current.next;
          }

          node.next = current;
          previous.next = node;

          current.prev = node;
          node.prev = previous;
        }

        this.length++;

        return true
      }
    },
    indexOf: (element)=> { //查找在表中位置
      let current = this.head,
          index = 0;

      while(current) {
        if(element === current.element) {
          return index;
        }
        index++;
        current = current.next
      }

      return -1; //没找到返回-1
    },
    isEmpty: ()=> { //判空
      return this.length === 0
    },
    size: ()=> { //链表长度
      return this.length
    },
    clear: ()=> { //清空
      this.head = null;
      this.tail = null;
    }
  }
```
