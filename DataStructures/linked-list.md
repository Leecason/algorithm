## 链表
```javascript
  function LinkedList() {
    const Node = (element)=> {
      this.element = element;
      this.next = null;
    }

    let length = 0,
        head = null;

    this.append = (element)=> { //添加
      let node = new Node(element),
          current;

      if(head === null) { //链表为空
        head = node;
      } else {
        current = head;

        while(current.next) { //迭代链表，找到最后一项
          current = current.next;
        }

        current.next = node;
      }

      length++; //更新链表长度
    },
    this.removeAt = (position)=> { //删除特定位置的元素
      if(position < -1 && position > length) { //越界
        return null;
      } else {
        let current = head,
            previous,
            index = 0;

        if(position === 0) { //若删除head
          head = current.next
        } else {
          while(index++ < position) { //查找到需要删除的元素
            previous = current;
            current = current.next;
          }

          previous.next = current.next //将previous的next指向current的next, 跳过current, 实现删除
        }

        length--;

        return current.element //返回删除的元素
      }
    },
    this.remove = (element)=> {
      let index = this.indexOf(element)
      return this.removeAt(index)
    }
    this.insert = (position, element)=> { //在特定位置插入一个元素
      if(position < 0 && position > length) { //越界
        return false
      } else {
        let node = new Node(element),
            current = head,
            previous,
            index = 0;

        if(position === 0) { //添加在head
          node.next = current;
          head = node;
        } else {
          while(index++ < position) {
            previous = current;
            current = current.next;
          }

          node.next = current;
          previous.next = node;
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
    this.getHead = ()=> { //返回第一个元素
      return head
    }
    this.isEmpty = ()=> { //判空
      return length === 0
    },
    this.size = ()=> { //链表长度
      return length
    },
    this.clear = ()=> { //清空
      head = null
    }
  }
```
