## 字典
```javascript
  function Dictionary() {
    let items = {}

    this.has = (key)=> {
      return items.hasOwnProperty(key)
    }

    this.set = (key, value)=> { //赋值
      items[key] = value
    }

    this.remove = (key)=> { //删除
      if(this.has(key)) {
        delete items[key]
        return true
      } else {
        return false
      }
    }

    this.values = ()=> {
      let values = []
      for (let key in items) {
        values.push(items[key])
      }

      return values
    }

    this.keys = ()=> {
      return Object.keys(items)
    }

    this.size = ()=> {
      return Object.keys(items).length
    }

    this.clear = ()=> {
      items = {}
    }

    this.get = (key)=> {
      return this.has(key) ? items[key] : undefined
    }
  }

```
