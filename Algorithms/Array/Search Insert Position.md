Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

- Cho một dãy số được sắp xếp, và 1 giá trị `target` . Bài toán yêu cầu tìm và trả về vị trí index của số đó trong mảng. Nếu số đó không tồn tại thì tìm vị trí của số đó nếu mà sắp xếp vào trong mảng.

**Example 1:**

```
Input: nums = [1,3,5,6], target = 5
Output: 2
```

**Example 2:**

```
Input: nums = [1,3,5,6], target = 2
Output: 1
```

**Example 3:**

```
Input: nums = [1,3,5,6], target = 7
Output: 4
```

**Example 4:**

```
Input: nums = [1,3,5,6], target = 0
Output: 0
```

**Example 5:**

```
Input: nums = [1], target = 0
Output: 0
```

 

**Constraints:**

- `1 <= nums.length <= 10^4`
- `-10^4 <= nums[i] <= 10^4`
- `nums` contains **distinct** values sorted in **ascending** order.
- `-10^4 <= target <= 10^4`



**Thuật toán**



Bởi vì ta thấy số lượng input đầu vào là rất lớn 10^4. Nếu giải quyết theo cách thông thường thì thời gian sẽ rất lâu. Bởi vì phải duyệt tất cả các phần tử nên độ phức tạp sẽ là O(n)

Ta nhận thấy input là mảng đã được sắp xếp, vì vậy ta sẽ dùng phương pháp tìm kiếm nhị phân (binary search) để giải quyết bài toán này.

```swift
func searchInsert(_ nums: [Int], _ target: Int) -> Int {
    var result = 0
    if let index = binarySearch(nums, target: target) {
        return index
    } else {
        if target >= nums[nums.count - 1] {
            return nums.count
        } else if target <= nums[0] {
            return 0
        } else {
            var lowIndex = 0
            var upIndex = nums.count - 1
          	// Duyệt cho đến khi lowInde = upIndex thì khi đó giá trị của index chính là giá trị mà ta cần insert vào mảng
            while lowIndex <= upIndex {
                let middle = (lowIndex + upIndex) / 2
                let middleValue = nums[middle]
                if middleValue > target {
                    // Insert vao ben trai
                    upIndex = middle - 1
                } else {
                    // insert vao ben phai
                    lowIndex = middle + 1
                }
            }
            return lowIndex
        }
    }
    
    
    return result
}

func binarySearch(_ nums: [Int], target: Int) -> Int? {
    var lowwerIndex = 0
    var upperIndex = nums.count - 1
    while lowwerIndex <= upperIndex {
        let middle = (lowwerIndex + upperIndex) / 2
        if nums[middle] == target {
            return middle
        } else if lowwerIndex > upperIndex {
            return nil
        } else {
            if nums[middle] < target {
                lowwerIndex = middle + 1
            } else if nums[middle] > target {
                upperIndex = middle - 1
            }
        }
    }
    return nil
}

```





