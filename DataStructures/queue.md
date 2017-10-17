## 队列 FIFO
```javascript
  function Queue(arr = []) {
    let items = arr;

    this.append = (element)=> { //入队
      items.push(element)
    }

    this.server = ()=> { //出队
      return items.shift()
    }

    this.isEmpty = ()=> { //判空
      return items.length === 0
    }

    this.size = ()=> {
      return items.length
    }

    this.clear = ()=> { //清空
      items = []
    }
  }
```

### 应用: 击鼓传花
```javascript
  function hotPotato(nameList, num) {
    let queue = new Queue(),
        eliminated = '';

    //入队
    for (var i = 0; i < nameList.length; i++) {
      queue.append(nameList[i])
    }

    while (queue.size() > 1) {
      // 按设定的击鼓次数，每个人都从队列头部出队转到队列尾部入队
      for (var i = 0; i < num; i++) {
        queue.append(queue.server())
      }
      // 到了规定次数后，在队列头部的人被淘汰
      eliminated = queue.server()
      console.log(eliminated + '被淘汰')
    }

    return eliminated;
  }
```
