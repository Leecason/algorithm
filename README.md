# js-algorithm

## 冒泡排序 Bubblesort
冒泡排序算法的运作如下：

 1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个
 2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数
 3. 针对所有的元素重复以上的步骤，除了最后一个
 4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较

```
  const bubbleSort = (arr)=> {

    // 获取数组个数
    const length = arr.length

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
    return arr
  }

  let arr
  bubbleSort(arr)
```

## 双向冒泡排序 Shakersort
双向冒泡排序是冒泡排序的一个简易升级版, 又称鸡尾酒排序. 冒泡排序是从低到高(或者从高到低)单向排序, 双向冒泡排序顾名思义就是从两个方向分别排序(通常, 先从低到高, 然后从高到低). 因此它比冒泡排序性能稍好一些.

```
  const shakerSort = (arr)=> {

    const length = arr.length

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

    return arr
  }

  let arr
  bubbleSort(arr)
```

## 快速排序 Quicksort
***快速排序（Quicksort）是对冒泡排序的一种改进。***

它的基本思想是：
通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

```
  const quickSort = (arr)=> {

    // 检查数组的元素个数，如果小于等于1，就返回。
　　if (arr.length <= 1) { return arr; }
　　
　　// 选择"基准"（pivot），并将其与原数组分离，再定义两个空数组，用来存放一左一右的两个子集。
　　let pivotIndex = Math.floor(arr.length / 2);
　　let pivot = arr.splice(pivotIndex, 1)[0];
　　let left = [];
　　let right = [];
　　
　　// 小于"基准"的元素放入左边的子集，大于基准的元素放入右边的子集。
　　for (let i = 0; i < arr.length; i++){
　　　　if (arr[i] < pivot) {
　　　　　　left.push(arr[i]);
　　　　} else {
　　　　　　right.push(arr[i]);
　　　　}
　　}
　　
　　// 最后，使用递归不断重复这个过程，就可以得到排序后的数组。
　　return quickSort(left).concat([pivot], quickSort(right));
  };

  let arr
  quickSort(arr)
```
