`Độ khó: Dễ `

## Find Pivot Index

Cho dãy số có `n` phần tử (gồm cả số âm và dương). Tìm index của số thoả mãn điều kiện sau tổng các số từ [0.. index - 1] bằng tổng các số từ [index + 1 .. n] 

Nếu `index = 0` và tổng các phần tử bên phải index  bằng `0` thì trả về  -1

Nêú `index = n - 1` và tổng các phần tử bên trái của index bằng `0` thì cũng trả về  -1 

Example 1:

```
Input: nums = [1,7,3,6,5,6]
Output: 3
Explanation:
The pivot index is 3.
Left sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11
Right sum = nums[4] + nums[5] = 5 + 6 = 11
```

Example 2:

```
Input: nums = [1,2,3]
Output: -1
Explanation:
There is no index that satisfies the conditions in the problem statement.
```


Example 3:
```
Input: nums = [2,1,-1]
Output: 0
Explanation:
The pivot index is 0.
Left sum = 0 (no elements to the left of index 0)
Right sum = nums[1] + nums[2] = 1 + -1 = 0
 ```

Điều kiện:
```
1 <= nums.length <= 104
-1000 <= nums[i] <= 1000
```

----

Chắc hẳn đọc xong đề bài các bạn sẽ nghĩ đây là một bài toán khá là đơn giản. Chỉ cần dùng 2 vòng lặp là xong, một vòng lặp duyệt từ đầu đến cuối, một vòng lặp tính tổng từ chỉ số i đến cuối mảng. 

Nếu làm theo cách này thì đương nhiên độ phức tạp của thuật toán là O(n^2). Tuy nhiên bạn có nghĩ rằng bài toán này có thể thực hiện với độ phức tạp là O(n)

Chúng ta suy nghĩ một chút thì có thể tìm ra được cách tính tổng của dãy số bên trái index và bên phải index một cách rất đơn giản.
Gọi sum là tổng của dãy `nums` ta sẽ có : `nums = left_sum + nums[index] + right_sum` .  Do đó cách giải quyết của bài toán này đó chính là đầu tiên ta sẽ tính tổng tất cả các phần tử của dãy nums. Sau khi duyện đến đâu thì ta sẽ tính tổng của dãy bên trái phần tử index. Từ giá trị `left_sum` này chúng ta sẽ tính được tổng của dãy bên phải. Tiếp tục duyệt cho đến khi `left_sum = right_sum ` or duyệt hết mảng.

Dưới dây là code của thuật toán trên được viết bằng swift

```swift

class Solution {
    func pivotIndex(_ nums: [Int]) -> Int {
        let sum = nums.reduce(0, +)
    
        // Tổng các số sau index 0 == 0 thì trả về 0
        if sum - nums[0] == 0 {
            return 0
        }



        var leftSum = 0
        for (index, item) in nums.enumerated() {
            if leftSum == sum - item - leftSum {
                return index
            }

            leftSum += item
        }

        // Tổng các số phía trc phần tử cuối cùng == 0 thì trả về index = nums.count - 1
        if sum - nums[nums.count - 1] == 0 {
            return nums.count - 1
        }
        return -1
    }
}
```







