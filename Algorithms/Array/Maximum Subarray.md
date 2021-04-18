**Difficulty**: Easy

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

Cho một mảng gồm các số nguyên, tìm mảng con(các phần tử liền nhau) sao cho tổng các phần tử trong mảng con đó là lớn nhất. Trả về tổng các các phần tử trong mảng con đó.

**Example 1:**

```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Example 2:**

```
Input: nums = [1]
Output: 1
```

**Example 3:**

```
Input: nums = [5,4,-1,7,8]
Output: 23
```

 

**Constraints:**

- `1 <= nums.length <= 3 * 104`
- `-105 <= nums[i] <= 105`

 

**Follow up:** If you have figured out the `O(n)` solution, try coding another solution using the **divide and conquer** approach, which is more subtle.



**Thuật toán:** (Hãy thử giải quyết bài này với độ phức tạp O(n))

- Cách đơn giải nhất của bài toán này đó chính là tính tổng tất cả của các sub array có thể xảy ra sau đó tìm max của chúng. Tuy nhiên chỉ riêng việc tính tổng của các sub array với 1 phần tử đã là 0(n) . Hơn nữa ta sẽ phải tính các sub array chứa 1 đến n phần tử. Như vậy thì độ phức tạp của thuật toán này sẽ tăng lên rất nhiều lần. Đây không phải là 1 cách hay để giải quyết bài toán này.



Thuật toán chúng ta sử dụng ở bài này chính là thuật toán Kandane ( `Kadane’s algorithm `)  sử dụng để giải quyết bài toán tìm mảng con lớn nhất trong 1 mảng các số nguyên cho trước. Thuật toán ban đầu được sử dụng để tìm mảng con lớn nhất cho mảng 1 chiều. Tuy nhiên chúng ta có thể mở rộng ra với sử dụng cho mảng đa chiều.

Thuật toán Kadane quét qua các phần tử của mảng, tính tại từng vị trí tổng lớn nhất có thể của các mảng con kết thúc tại vị trí đó. Mảng con này có thể rỗng khi tổng của các phần tử bằng 0 hoặc có thể chứa nhiều hơn một phần tử so với mảng con lớn nhất tại vị trí trước đó. Thuật toán của chương trình được viết bằng ngôn ngữ Python như sau:

```python
def max_subarray(A):
    max_so_far = max_ending_here = A[0]
    for x in A[1:]:
        max_ending_here = max(x, max_ending_here + x)
        max_so_far = max(max_so_far, max_ending_here)
    return max_so_far
```



Ta sẽ triển khai thuật toán sau bằng ngôn ngữ Swift 

```swift 
func maxSubArray(_ nums: [Int]) -> Int {
       guard nums.count > 1 else { return nums[0] }
        var maxSoFar = nums[0]
        var maxEndingHere = nums[0]
        for index in stride(from: 1, through: nums.count - 1, by: 1) {
            if maxEndingHere < 0 {
                // Nếu tổng các phần tử từ 0 đên index < 0

                if maxEndingHere < nums[index] {
                    // Tổng tất cả các phần tử phía trước nhỏ hơn phần tử vị trí
                  //index thì max sum = phần tử ở vị trí index
                    maxEndingHere = nums[index]
                }
            } else {
                maxEndingHere += nums[index]
            }
						
            maxSoFar = max(maxEndingHere, maxSoFar)
        }

        return maxSoFar
    }
```



Thuật toán này tính toán dựa trên cấu trúc con tối ưu (mảng con lớn nhật tại một vị trí được tính toán đơn giản từ các bài toán con nhỏ hơn là mảng con lớn nhất tại vị trí trước đó) nên thuật toán này thuộc dạng Quy hoạch động mà chúng ta sẽ cùng tìm hiểu ở phần sau.







