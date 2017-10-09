## 栈 LIFO
```javascript
  function Stack(arr = []) {
    this.init(arr)
  }
  Stack.prototype = {
    constructor: Stack,
    init: (arr)=> { //初始化
      this.items = arr
    },
    push: (element)=> { //入栈
      this.items.push(element)
    },
    pop: ()=> { //出栈
      return this.items.pop()
    },
    top: ()=> { //取栈顶元素
      return this.items[this.items.length - 1]
    },
    isEmpty: ()=> { //判空
      return this.items.length === 0
    },
    clear: ()=> { //清空
      this.items = []
    }
  }
```

### 应用: 十进制转换为其他进制
```javascript
  function BaseConverter(decNumber, base) {
    let remStack = new Stack(),
        rem,
        binaryString = '',
        digits = '0123456789ABCDEF';

    // 判断十进制数是否为0，把余数推入栈中
    while(decNumber > 0) {
      rem = Math.floor(decNumber % base);
      remStack.push(rem);
      decNumber = Math.floor(decNumber / base);
    }

    // 把栈中的元素拼接打印出来
    while(!remStack.isEmpty()) {
      binaryString += digits[remStack.pop()]
    }

    return binaryString;
  }
```
