### Minimum Difference Between Largest and Smallest Value in Three Moves

Given an array `nums`, you are allowed to choose one element of `nums` and change it by any value in one move.

Return the minimum difference between the largest and smallest value of `nums` after perfoming at most 3 moves.

 

**Example 1:**

```
Input: nums = [5,3,2,4]
Output: 0
Explanation: Change the array [5,3,2,4] to [2,2,2,2].
The difference between the maximum and minimum is 2-2 = 0.
```

**Example 2:**

```
Input: nums = [1,5,0,10,14]
Output: 1
Explanation: Change the array [1,5,0,10,14] to [1,1,0,1,1]. 
The difference between the maximum and minimum is 1-0 = 1.
```

**Example 3:**

```
Input: nums = [6,6,0,1,1,4,6]
Output: 2
```

**Example 4:**

```
Input: nums = [1,5,6,14,15]
Output: 1
```

 

**Constraints:**

- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`



**Thuật toán:**

// Thay tối đa 3 số bằng 1 số nào đó trong mảng, sau đó tìm min của max - min 

 Ta nhận thấy nếu mà mảng có ít hơn 4 phần tử thì lúc nào giá trị trả về cũng sẽ = 0 ( bởi vì thay 3 số ở phía sau bằng phần tử đầu tiên -> min = max →  max - min = 0)

Trong trường hợp có 5 phần tử trở lên.  Ta sẽ xắp xếp phần tử theo thứ tự tăng dần. Việc này tốn O(nlogn) time. Sau khi sắp xếp xong mảng của chúng ta sẽ trở nên như sau.

`[min1, min2, min3,...., max3, max2, max1] `  với max1 là số lớn nhất trong mảng, min2 là số bé nhất trong mảng. Từ đây ta có thể nhận thấy bài toán dễ dàng được giải quyết bằng cách thay một phần tử bất kì nằm giữa min3 -> max3 vào 6 số ở trên. 

Ta có 4 cách để thay 3 số vào 6 vị trí để thoả mãn đề bài đó là

1. Xoá 3 vị trí max ( thay các số bất kỳ trong min3 -> max3 vào 3 vị trí cuối cùng)
2. Xoá min1, và xoá max2, max1
3. Xoá min1, min2 và max1
4. Xoá min1, min2, min3

Trong 4 cách trên thì tìm giá trị nhỏ nhất trong 4 cách đó là được.

```swift
class Solution {
    func minDifference(_ nums: [Int]) -> Int {
 			  guard nums.count > 4 else { return 0}
        var sortedArr = nums.sorted(by: <)
        var result = [Int]()
        var index = 0
      	// Cách sử dụng vòng lặp while này cũng sẽ phù hợp với bài toán thay k số trong mảng cũng sẽ sử dụng đc. 
        while index < 4 {
            result.append(sortedArr[nums.count - 1 - 3 + index] - sortedArr[index])
            index += 1
        }
        return result.min()!
    }
}
```

Bài toán trên được giải quyết với độ phức tạp là O(nlogn) và space complexity O(n)

