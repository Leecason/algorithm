## 集合
```javascript
  function Set() {
    let items = {}; //集合没有重复项，使用对象来作为集合的容器

    this.has = (value)=> {
      return items.hasOwnProperty(value)
    }

    this.add = (value)=> {
      if(!this.has(value)) { //元素不存在
        items[value] = value;
        return true;
      } else {
        return false;
      }
    }

    this.remove = (value)=> {
      if(this.has(value)) { //元素存在
        delete items[value];
        return true;
      } else {
        return false;
      }
    }

    this.values = ()=> {
      return Object.keys(items);
    }

    this.clear = ()=> {
      items = {};
    }

    this.size = ()=> {
      return Object.keys(items).length;
    }

    this.union = (otherSet)=> { //并集
      let unionSet = new Set();
      let values = this.values();

      for(let i = 0; i < values.length; i++) { //添加当前集合
        unionSet.add(values[i]);
      }

      values = otherSet.values();
      for(let i = 0; i < values.length; i++) { //添加其他集合
        unionSet.add(values[i]);
      }

      return unionSet;
    }

    this.intersection = (otherSet)=> { //交集
      let intersectionSet = new Set();
      let values = this.values();

      for(let i = 0; i < values.length; i++) {
        if(otherSet.has(values[i])) {
          intersectionSet.add(values[i])
        }
      }

      return intersectionSet;
    }

    this.difference = (otherSet)=> { //差集, 与交集相反
      let differenceSet = new Set();
      let values = this.values();

      for(let i = 0; i < values.length; i++) {
        if(!other.has(values[i])) {
          differenceSet.add(values[i])
        }
      }

      return differenceSet;
    }

    this.subSet = (otherSet)=> { //子集
      if (this.size() > otherSet.size()) {
        return false
      } else {
        let values = this.values();

        for(let i = 0; i < values.length; i++) {
          if(!otherSet.has(values[i])) {
            return false
          }
        }

        return true
      }
    }
  }
```
