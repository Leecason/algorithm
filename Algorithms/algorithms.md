## 冒泡排序 Bubblesort
冒泡排序算法的运作如下：

 1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个
 2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数
 3. 针对所有的元素重复以上的步骤，除了最后一个
 4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较

```javascript
  const bubbleSort = (arr)=> {

    // 获取数组个数
    const length = arr.length;

    // 一共执行 i = length - 1 次排序
    for (let i = 0; i < length; i++) {

      // 扣除掉每轮不需要比较的数组（第一轮倒数第一个，第二轮倒数第二个，第三轮...）
      for (let n = 0; n < length - 1 - i; n++) {

        // 如果前面比后面大，调换位置，es6 解构赋值语法。
        if (arr[n] > arr[n+1]) {
          [arr[n], arr[n + 1]] = [arr[n + 1], arr[n]]
        }
      }
    }
    return arr;
  }

  let arr;
  bubbleSort(arr);
```

## 双向冒泡排序 Shakersort
双向冒泡排序是冒泡排序的一个简易升级版, 又称鸡尾酒排序. 冒泡排序是从低到高(或者从高到低)单向排序, 双向冒泡排序顾名思义就是从两个方向分别排序(通常, 先从低到高, 然后从高到低). 因此它比冒泡排序性能稍好一些.

```javascript
  const shakerSort = (arr)=> {

    const length = arr.length;

    for (let i = 0; i < length; i++) {

      //第一轮，将最小的数冒泡到前面
      for(let j = i; j < length; j++) {
        if (arr[j] > arr[j+1]) {
          [arr[j], arr[j+1]] = [arr[j+1], arr[j]]
        }
      }

      //第二轮，将最大的数冒泡到后面
      for (let j = length; j > i; j--) {
        if (arr[j-1] > arr[j]) {
          [arr[j-1], arr[j]] = [arr[j], arr[j-1]]
        }
      }
    }

    return arr;
  }

  let arr;
  shakerSort(arr);
```

## 快速排序 Quicksort
***快速排序（Quicksort）是对冒泡排序的一种改进。***

它的基本思想是：
通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

```javascript
  const quickSort = (arr)=> {

    const length = arr.length;

    // 检查数组的元素个数，如果小于等于1，就返回。
　　if (length <= 1) { return arr; }
　　
　　// 选择"基准"（pivot），并将其与原数组分离，再定义两个空数组，用来存放一左一右的两个子集。
　　let pivotIndex = Math.floor(length / 2),
　　    pivot = arr.splice(pivotIndex, 1)[0],
       left = [],
       right = [];
　　
　　// 小于"基准"的元素放入左边的子集，大于基准的元素放入右边的子集。
　　for (let i = 0; i < length; i++){
　　　　if (arr[i] < pivot) {
　　　　　　left.push(arr[i]);
　　　　} else {
　　　　　　right.push(arr[i]);
　　　　}
　　}
　　
　　// 最后，使用递归不断重复这个过程，就可以得到排序后的数组。
　　return quickSort(left).concat([pivot], quickSort(right));
  };

  let arr;
  quickSort(arr);
```

## 直接插入排序 DirectInsertsort
它的基本思想是：
每步将一个待排序的纪录，按其关键码值的大小插入前面已经排序的文件中适当位置上，直到全部插入完为止。

```javascript
  const directInsertSort = (arr)=> {

    const length = arr.length;

    for(let i = 1; i < length; i++) {
      let current = arr[i], //当前元素
          j = i - 1; //待比较元素index

      while(j >= 0 && arr[j] > current) { //待比较元素比当前元素大
        arr[j+1] = arr[j]; //待比较元素后移一位
        j--; //游标前移一位
      }
      if(j+1 != i) { //避免同一个元素赋值给自身
        arr[j+1] = current; //将当前元素插入预留空位
      }
    }

　　return arr;
  };

  let arr;
  directInsertSort(arr);
```

## 二分插入排序 BinaryInsertsort
它的基本思想是：
1. 从第一个元素开始，该元素可以认为已经被排序；
2. 取出下一个元素，在已经排序的元素序列中二分查找到第一个比它大的数的位置；
3. 将新元素插入到该位置后；
4. 重复上述两步

```javascript
  const binaryInsertSort = (arr)=> {

    const length = arr.length

    for(let i = 1; i < length; i++) {
      let current = arr[i],
          low = 0,
          high = i - 1;

      while(low <= high) { //折半查找
        let mid = parseInt((low + high) / 2);
        if(current < arr[mid]) { //插入点在低半区
          high = mid - 1;
        } else { //插入点在高半区
          low = mid + 1;
        }
      }

      for (let j = i - 1; j >= low; j--) { //插入位置之后的元素全部往后移一位
        arr[j+1] = arr[j]
      }

      arr[low] = current; //插入元素
    }

　　return arr;
  };

  let arr;
  binaryInsertSort(arr);
```

## 希尔排序 Shellsort
***希尔排序的实质是分组直接插入排序，该方法又称缩小增量排序。***
该方法的基本思想是：
1. 将数组拆分为若干个子分组, 每个分组由相距一定”增量”的元素组成
2. 然后对每个子分组应用直接插入排序
3. 逐步减小”增量”, 重复步骤1,2
4. 直至”增量”为1, 这是最后一个排序, 此时的排序, 也就是对全数组进行直接插入排序

```javascript
  const shellSort = (arr)=> {

    const length = arr.length;

    let gap = Math.floor(length / 2); //步长

    while(gap != 0) {
      for(let i = gap; i < length; i++) { //按步长分组
        let current = arr[i], //当前元素

            j = i - gap; //待比较元素index

        while(j >= 0 && arr[j] > current) { //待比较元素比当前元素大
          arr[j + gap] = arr[j]; //将待比较元素后移gap位

          j -= gap; //游标前移gap位
        }
        arr[j+gap] = current; //将当前元素插入预留空位
      }
      gap = Math.floor(gap / 2)
    }

　　return arr;
  };

  let arr;
  shellSort(arr);
```

## 选择排序 Selectionsort
它的工作原理是每一次从待排序的数据元素中选出最小（或最大）的一个元素，存放在序列的起始位置，直到全部待排序的数据元素排完。

***选择排序是不稳定的排序方法***

选择排序每次交换的元素都有可能不是相邻的, 因此它有可能打破原来值为相同的元素之间的顺序. 比如数组[2,2,1,3], 正向排序时, 第一个数字2将与数字1交换, 那么两个数字2之间的顺序将和原来的顺序不一致, 虽然它们的值相同, 但它们相对的顺序却发生了变化. 我们将这种现象称作**不稳定性**.

```javascript
  const selectionSort = (arr)=> {

    const length = arr.length;

    for(let i = 0; i < length; i++) {
      for(let j = i; j < length; j++) {
        if (arr[i] > arr [j]) {
          [arr[i], arr[j]] = [arr[j], arr[i]]
        }
      }
    }

　　return arr;
  };

  let arr;
  selectionSort(arr);
```

## 堆排序 Heapsort
堆排序是指利用堆积树（堆）这种数据结构所设计的一种排序算法，它是选择排序的一种。可以利用数组的特点快速定位指定索引的元素。堆分为大根堆和小根堆，是完全二叉树。大根堆的要求是每个节点的值都不大于其父节点的值，即A[PARENT[i]] >= A[i]。

> 并非所有的序列都是堆, 对于序列k1, k2,…kn, 需要满足如下条件才行:<br>
ki <= k(2i) 且 ki<=k(2i+1)(1≤i≤ n/2), 即为小根堆, 将<=换成>=, 那么则是大根堆. 我们可以将这里的堆看作完全二叉树, k(i) 相当于是二叉树的非叶子节点, k(2i) 则是左子节点, k(2i+1)是右子节点.

算法的基本思想(以大根堆为例):
1. 先将初始序列K[1..n]建成一个大根堆, 此堆为初始的无序区
2. 再将关键字最大的记录K1 (即堆顶)和无序区的最后一个记录K[n]交换, 由此得到新的无序区K[1..n-1]和有序区K[n], 且满足K[1..n-1].keys≤K[n].key
3. 交换K1 和 K[n] 后, 堆顶可能违反堆性质, 因此需将K[1..n-1]调整为堆. 然后重复步骤2, 直到无序区只有一个元素时停止

```javascript
  const heapify = (arr, i, length)=> { //堆调整
    let left = i * 2 + 1,
        right = i * 2 + 2,
        largest = i;

    if(left < length && arr[largest] < arr[left]) {
      largest = left;
    }
    if(right < length && arr[largest] < arr[right]) {
      largest = right;
    }
    if(largest != i) { //最大索引不是初始索引
      [arr[i], arr[largest]] = [arr[largest], arr[i]];

      //继续解决交换过来的节点对堆造成的影响
      heapify(arr, largest, length);
    }
  }

  const heapSort = (arr)=> {
    //建立大顶堆
    let length = arr.length;

    for(let i = parseInt(length / 2) - 1; i >= 0; i--) {
      heapify(arr, i, length)
    }

    for(let i = length - 1; i > 0; i--) {
      [arr[0], arr[i]] = [arr[i], arr[0]];
      heapify(arr, 0, --length);
    }

    return arr;
  }

  let arr;
  heapSort(arr);
```
