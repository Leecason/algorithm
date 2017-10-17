## 二叉搜索树
知识点: [知乎问题-递归](https://www.zhihu.com/question/20507130)
```javascript
  function BinarySearchTree() {
    const node = (key)=> {
      this.key = key; //键值
      this.left = null; //左节点
      this.right = null; //右节点
    }

    let root = null; //根节点

    const insertNode = (node, newNode)=> { //插入节点
      // 在二叉搜索树中，比父节点小的值存在左侧节点，大于等于父节点的存在右侧节点
      // 若要插入一个节点（根节点已存在），首先与根节点比大小，若比根节点小则应插入根节点的左侧
      // 如果左侧已存在节点，则递归调用函数，将左侧节点传入递归函数作为当前节点
      // 如果插入的节点比当前节点大且当前节点右侧为空，则插入右侧
      // 如果插入节点比根节点小，原理同上

      if(newNode.key < node.key) {
        if(node.left === null) {
          node.left = newNode
        } else {
          insertNode(node.left, newNode)
        }
      } else {
        if(node.right === null) {
          node.right = new Node
        } else {
          insertNode(node.right, newNode)
        }
      }
    }

    this.insert = (key)=> { //向树中插入一个新的键
      let node = new Node(key)

      if(root === null) {
        root = node
      } else {
        insertNode(root, node)
      }
    }

    const searchNode = (node, key)=> { //搜索节点
      //比较输入的key与当前节点的key，当相等时（意味着找到了目标节点）就返回true
      //当查找完最末端的节点时，即传入的node为null时，就返回false，表示未找到。
      if (node === null) {
        return false
      }

      if(key < node.key) {
        return seachNode(node.left, key)
      } else if (key > node.key) {
        return searchNode(node.right, key)
      } else {
        return true
      }
    }

    this.search = (key)=> { //在树中查找一个键，如果节点存在返回tue，否则返回false
      return searchNode(root, key)
    }

    //遍历
    const inOrderTraverseNode = (node, callback)=> { //中序遍历，按顺序（从小到大）访问整棵树的所有节点，也就是常见的升序排序
      if(node !== null) { //停止递归的条件
        inOrderTraverseNode(node.left, callback)
        callback(node.key)
        inOrderTraverseNode(node.right, callback)
      }
    }

    this.inOrderTraverse = (callback)=> {
      inOrderTraverseNode(root, callback)
    }

    const preOrderTraverseNode = (node, callback)=> { //先序遍历
      if(node !== null) {
        callback(node.key)
        preOrderTraverseNode(node.left, callback)
        preOrderTraverseNode(node.right, callback)
      }
    }

    this.preOrderTraverse = (callback)=> {
      preOrderTraverseNode(root, callback)
    }

    const postOrderTraverseNode = (node, callback)=> { //后序遍历
      if(node !== null) {
        postOrderTraverseNode(node.left, callback)
        postOrderTraverseNode(node.right, callback)
        callback(node.key)
      }
    }

    this.postOrderTraverse = (callback)=> {
      postOrderTraverseNode(root, callback)
    }

    //min, max
    const minNode = (node)=> {
      if(node) { // 如果node存在，则开始搜索。能避免树的根节点为Null的情况
        // 只要树的左侧子节点不为null，则把左子节点赋值给当前节点。
        // 若左子节点为null，则该节点肯定为最小值。
        while(node && node.left !== null) {
          node = node.left
        }
        return node.key
      }
      return null
    }

    const maxNode = (node)=> {
      if(node) {
        while(node && node.right !== null) {
          node = node.right
        }
        return node.key
      }
      return null
    }

    this.min = ()=> {
      return minNode(root)
    }

    this.max = ()=> {
      return maxNode(root)
    }

    //remove(key) 从树中移除某个键
    const findMinNode = (node)=> {
      if(node) {
        while(node && node.left ! == null) {
          node = node.left
        }
        return node
      }
      return null
    }

    const removeNode = (node, key)=> {
      if(node === null) {
        return null
      }

      if(key < node.key) {
        node.left = removeNode(node.left, key)
        return node
      } else if (key > node.key) {
        node.right = removeNode(node.right, key)
        return node
      } else {
        // 删除节点为叶节点,直接删除该节点
        if(node.left === null && node.right === null) {
          node = null
          return node
        }
        // 删除节点一侧有子节点,将一侧的子节点替换为当前节点
        if(node.left === null) {
          node = node.right
          return node
        } else if (node.right === null) {
          node = node.left
          return node
        }
        // 删除节点两侧都有子节点,找到当前节点右侧子树中最小的那个节点,替换掉要删除的节点,然后再把右侧子树中最小的节点移除
        let aux = findMinNode(node.right)
        node.key = aux.key
        node.right = removeNode(node.right, aux.key)
        return node
      }
    }

    this.remove = (key)=> {
      return removeNode(root, key)
    }
  }

```
