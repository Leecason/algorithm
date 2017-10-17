## 散列表
```javascript
  function HashTable() {
    let table = []

    let djb2HashCode = (key)=> { //散列函数 大致原理:相加所得的hash数要够大，且尽量为质数，用hash与另一个大于散列表大小的质数做求余，这样得到的地址也能尽量不重复。
      let hash = 5381;
      for(let i = 0; i < key.length; i++) {
        hash = hash * 33 + key.charCodeAt(i);
      }
      return hash % 1013
    }

    let ValuePair = (key, value)=> {
      this.key = key;
      this.value = value;
    }

    this.put = (key, value)=> { //向列表添加一个新的项
      let position = djb2HashCode(key)
      if(table[position] === undefined) { //生成一个链表
        table[position] = new LinkedList()
      }
      table[position].append(new Value(key, value))
    }

    this.get = (key)=> { //返回根据键值检索到的特定的值
      let position = djb2HashCode(key)

      if(table[position] !== undefined) {
        let current = table[position].getHead()

        while(current.next) { //遍历链表查找值
          if(current.element.key === key) {
            return current.element.value
          }

          current = current.next
        }

        if(current.element.key === key) { //查看最后一个元素
          return current.element.value
        }
      }

      return undefined
    }

    this.remove = (key) { //根据键值从散列表中移除值
      let position = djb2HashCode(key)

      if(table[position] !== undifined) {
        let current = table[position].getHead()

        while(current.next) {
          if(current.element.key === key) {
            table[position].remove(current.element)
            if(table[position].isEmpty()) { //链表空了，把该位置设为undefined
              table[position] = undifined
            }
            return true
          }
          current = current.next
        }

        if(current.element.key === key) {
          table[position].remove(current.element)
          if(table[position].isEmpty()) {
            table[position] = undefined
          }
          return true
        }
      }

      return false
    }
  }

```
