学习笔记  
本周主要学习了深度、广度遍历、贪心算法及二分搜索。  
其中深度一般就是递归，广度需要维护一个队列，贪心算法每次都用最优方案，二分搜索每次都可以舍弃一般数据为log(n)复杂度。  
学习下来，对于二分搜索其实熟练度很欠缺，尤其是是思路好想，但是二分的细节太多了，比如while(是否要等于)，mid + 1 还是 -1。

下面总结  
使用二分查找，寻找一个半有序数组 [4, 5, 6, 7, 0, 1, 2] 中间无序的地方
```
 public int search(int[] nums) {

        public int findMin(int[] nums) {
        
                if (nums == null || nums.length == 0) {
                    return -1;
                }
                 int left = 0;
                 int right = nums.length -1;
                 while (left <= right) { //边界为[left,right] 闭区间
                     int mid = left + (right - left) / 2;
                     if (nums[left] < nums[mid]) { // mid > left 说明旋转点在右边界，把left位置转换为mid
                         left = mid;
                     }else { // mid <= left 说明旋转点在左边界，把left位置转换为所以 right = mid ,又因为=已经判断了，所以此处-1
                         right = mid - 1; 
                     }
                 }
                return left; // 最后输出元素 的下一个为旋转点
            }
    }
```