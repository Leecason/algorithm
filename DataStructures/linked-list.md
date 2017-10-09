## 链表
```javascript
  function Node(element) {
    this.element = element;
    this.next = null;
  }
  function LinkedList() {
    this.init()
  }
  LinkedList.prototype = {
    constructor: LinkedList,
    init: ()=> { //初始化
      this.length = 0;
      this.head = null;
    },
    append: (element)=> { //添加
      let node = new Node(element),
          current;

      if(this.head === null) { //链表为空
        this.head = node;
      } else {
        current = this.head;

        while(current.next) { //迭代链表，找到最后一项
          current = current.next;
        }

        current.next = node;
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
          this.head = current.next
        } else {
          while(index++ < position) { //查找到需要删除的元素
            previous = current;
            current = current.next;
          }

          previous.next = current.next //将previous的next指向current的next, 跳过current, 实现删除
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
          node.next = current;
          this.head = node;
        } else {
          while(index++ < position) {
            previous = current;
            current = current.next;
          }

          node.next = current;
          previous.next = node;
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
      this.head = null
    }
  }
```
