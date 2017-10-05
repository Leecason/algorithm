# algorithm

## 冒泡排序 bubbleSort
冒泡排序算法的运作如下：（从后往前）

 1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个
 2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对。在这一点，最后的元素应该会是最大的数
 3. 针对所有的元素重复以上的步骤，除了最后一个
 4. 持续每次对越来越少的元素重复上面的步骤，直到没有任何一对数字需要比较

```
// 确定数组
  const arr

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

  bubbleSort(arr)
```
