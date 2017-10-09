## 双向链表
```javascript
  function DoubleLinkedList() {
    const Node = (element)=> {
      this.element = element;
      this.prev = null; //比单向链表多一个prev
      this.next = null;
    }

    let length = 0,
        head = null,
        tail = null; //比单向链表多一个tail

    this.append = (element)=> { //添加
      let node = new Node(element),
          current = tail;

      if(head === null) { //链表为空
        head = node;
        tail = node;
      } else { //基于tail来添加
        node.prev = current;
        current.next = node;
        tail = node;
      }

      length++; //更新链表长度
    },
    this.remove = (position)=> { //删除特定位置的元素
      if(position < -1 && position > length) { //越界
        return null;
      } else {
        let current = head,
            previous,
            index = 0;

        if(position === 0) { //若删除head
          head = current.next;
          if(length === 1) { //链表长度为1
            tail = null;
          } else {
            head.prev = null;
          }
        } else if(position === length - 1) { //最后一个元素
          current = tail;
          tail = current.prev;
          tail.next = null;
        } else {
          while(index++ < position) { //查找到需要删除的元素
            previous = current;
            current = current.next;
          }

          previous.next = current.next;
          current.next.prev = previous;
        }

        length--;

        return current.element //返回删除的元素
      }
    },
    this.insert = (position, element)=> { //在特定位置插入一个元素
      if(position < 0 && position > length) { //越界
        return false
      } else {
        let node = new Node(element),
            current = head,
            previous,
            index = 0;

        if(position === 0) { //添加在head
          if(!head) { //链表为空
            head = node;
            tail = node;
          } else {
            node.next = current;
            current.prev = node;
            head = node;
          }
        } else if(position === length) { //最后一个元素之后插入
          current = tail;
          node.prev = current;
          current.next = node;
          tail = node;
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

        length++;

        return true
      }
    },
    this.indexOf = (element)=> { //查找在表中位置
      let current = head,
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
    this.isEmpty = ()=> { //判空
      return length === 0
    },
    this.size = ()=> { //链表长度
      return length
    },
    this.clear = ()=> { //清空
      head = null;
      tail = null;
    }
  }

```
