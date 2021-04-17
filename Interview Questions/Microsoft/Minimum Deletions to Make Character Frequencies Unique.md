A string `s` is called **good** if there are no two different characters in `s` that have the same **frequency**.

Given a string `s`, return *the **minimum** number of characters you need to delete to make* `s` **good**.

The **frequency** of a character in a string is the number of times it appears in the string. For example, in the string `"aab"`, the **frequency** of `'a'` is `2`, while the **frequency** of `'b'` is `1`.

 

**Example 1:**

```
Input: s = "aab"
Output: 0
Explanation: s is already good.　（Bởi vì số lần xuất hiện của a và b là khác nhau)
```

**Example 2:**

```
Input: s = "aaabbbcc" -> Tần số xuất hiện của a và b là như nhau. Vì vậy ta cần phải xoá n ký tự để cho tuần số các ký tự trong chuỗi là khác nhau. 
Output: 2
Explanation: You can delete two 'b's resulting in the good string "aaabcc".
Another way it to delete one 'b' and one 'c' resulting in the good string "aaabbc".
```

**Example 3:**

```
Input: s = "ceabaacb"
Output: 2
Explanation: You can delete both 'c's resulting in the good string "eabaab".
Note that we only care about characters that are still in the string at the end (i.e. frequency of 0 is ignored).
```

 

**Constraints:**

- `1 <= s.length <= 105`
- `s` contains only lowercase English letters.



**Thuật toán:**

Ở bài này ta sẽ học được cách giải quyết một bài toán dựa vào cấu trúc dữ liệu `Set` trong Swift.

Đầu tiên ta nhận thấy với input là `ceabaacb` thì sẽ rất khó thao tác ta sẽ chuyển về một dạng khác dễ thao tác hơn. Đó chính là kiểu dictionary với key chính là `character` còn value là tần số xuất hiện của nó

Với input như trên thì sau khi ta chuyển sẽ được một dict như sauu:

```
["c": 2, "b": 2, "a": 3, "e": 1] 
Tương đương [2, 2, 3, 1]
```

Sau khi chuyển về trên thì ta nhận thấy bài toán ban đầu trở thành 1 bài toán đơn giản hơn rất nhiều đó chính là các phần tử trong mảng trên phải giảm tối thiểu bao nhiêu đơn vị để mỗi phần tử trong mảng là duy nhất.

Từ đây ta sẽ chỉ cần duyệt mảng dùng set để lưu những phần tử đã duyệt. Khi gặp 1 phần tử đã có trong `set` thì ta bắt đầu trừ cho đến khi không còn phần tử nào trùng lặp ở `set` nữa.

Ta thấy thuật toán này sẽ có độ phức tạp trong trường hợp xấu nhất là O(n^2). Trường hợp này xấu nhất khi mỗi character sẽ xuất hiện 1 lần. Khi đó dict sẽ chứa s.count phần tử và phần check `while set.contain(val)` cũng sẽ chạy 0(n) time vs n chính là size của set. Tuy nhiên này trường hợp này sẽ rất ít khi xảy ra. Bởi vì trong hầu hết trường hợp thì chiều dài của `dict` nhỏ hơn rất nhiều so với chiều dài của `s` input.

```swift
class Solution {
    func minDeletions(_ s: String) -> Int {
        var dict = [Character: Int]()
      // O(n)
        for char in s { 
            dict[char, default: 0] += 1
        }
        var set: Set<Int> = []
        var result = 0
      
        for (key, value) in dict {
            var val = value
            while set.contains(val) {
                val -= 1
                result += 1
            }
            if val > 0 {
                set.insert(val)
            }
        }
        return result
    }
}
```



