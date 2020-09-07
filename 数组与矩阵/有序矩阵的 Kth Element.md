给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第 k 小的元素。
请注意，它是排序后的第 k 小元素，而不是第 k 个不同的元素。

 

示例：

matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

返回 13。


// 有序矩阵的Kth  
const countInMatrix = (matrix, midVal) => {
  const n = matrix.length; // 方阵n行n列
  let count = 0;
  let row = 0; // 第一行
  let col = n - 1; // 最后一列
  while (row < n && col >= 0) {
    if (midVal >= matrix[row][col]) { // 如果中间值大于等于当前行最后则把改行所有元素计数，并向下一行移动
      count += col + 1; // 不大于它的数增加col+1
      row++; // 比较下一行
    } else { // 比当前行最后元素小
      col--; // 留在当前行并向左比较
    }
  }
  return count;
}

const kthSmallest = (matrix, k) => {
  const n = matrix.length;
  let low = matrix[0][0];
  let high = matrix[n-1][n-1];
  while(low <= high) {
    // 无符号右移运算符>>>（防止溢出）为什么使用low + (high - low) / 2而不使用(high + low) / 2呢？目的是防止溢出！
    let midVal = low + ((high - low) >>> 1); //获取中间值
    let count = countInMatrix(matrix, midVal); // 矩阵中小于等于它的个数
    if (count < k) { //中间值小了，二分查找向右
      low = midVal + 1;
    } else {
      high = midVal - 1;
    }
  }
  return low;
}
 let matrix = [
  [ 1,  5,  9],
  [10, 11, 13],
  [12, 13, 15]
],
k = 8;
console.log(kthSmallest(matrix, k)); // 13