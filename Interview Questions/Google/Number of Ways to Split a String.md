

Given a binary string `s` (a string consisting only of '0's and '1's), we can split `s` into 3 **non-empty** strings s1, s2, s3 (s1+ s2+ s3 = s).

Return the number of ways `s` can be split such that the number of characters '1' is the same in s1, s2, and s3.

Since the answer may be too large, return it modulo 10^9 + 7.

 

**Example 1:**

```
Input: s = "10101"
Output: 4
Explanation: There are four ways to split s in 3 parts where each part contain the same number of letters '1'.
"1|010|1"
"1|01|01"
"10|10|1"
"10|1|01"
```

**Example 2:**

```
Input: s = "1001"
Output: 0
```

**Example 3:**

```
Input: s = "0000"
Output: 3
Explanation: There are three ways to split s in 3 parts.
"0|0|00"
"0|00|0"
"00|0|0"
```

**Example 4:**

```
Input: s = "100100010100110"
Output: 12
```

 

**Constraints:**

- `3 <= s.length <= 10^5`
- `s[i]` is `'0'` or `'1'`.



**Thuật toán**

Số cách split một string thành 3 string s1, s2, s3 mà số chữ số 1 trong mỗi sub string là như nhau.

Tìm tổng tất cả các số 1.

Ta sẽ có 3 kịch bản cho bài toán này

**TH1.**

Nếu ko chia hết cho 3 thì là trả về 0(Có nghĩa là có 0 cách)

**TH1**:

Nếu tất cả là số 0 thì việc bạn chia chuỗi như thế nào ko quan trọng miễn là bạn chia thành 3 chuỗi s1, s2, s3. Khi đó số cách chia sẽ bằng = (n - 2) + (n - 1) + .. + 1 = (n - 2) (n - 1) / 2

**TH3**

Đây cũng là trường hợp mà ta cần phải giải quyết đó chính là tổng số chữ số 1 chia hết cho 3. 

Khi đó chiến thuật của ta là tính mỗi chữ số 1 trong các chuỗi s1, s2, s3.

Gọi k là số chữ số 1 trong s1, s2, s3 thì chúng ta sẽ duyệt số cách tìm s1 cho đến khi thấy số chữ số 1 < k + 1

Ta sẽ lấy ví dụ trong trường hợp ví dụ 4 ở trên để giải thích thuật toán này:

```
100100010100110
```

Ở đây ta thấy là có 6 số 1 vì vậy ta có thể chia thành 3 chuỗi s1, s2, s3 mà mỗi chuỗi sẽ bao gồm hai số 1. 

Ta sẽ bắt đầu chia với chuỗi s1 trước. Ta thấy s1 sẽ có các trường hợp thoả mãn như sau

```
1001 00010100110
10010 0010100110
100100 010100110
1001000 10100110
```

Như vậy theo ta thấy s1 sẽ có 4 trường hợp thoả mãn. Cách tính số trường hợp thoã mãn đó là ta sẽ chạy từ đầu cho đến khi đếm đủ số lượng chữ số 1 bằng với k. Sau đó ta tiếp tục đếm cho đến khi gặp chứ số 1 tiếp theo. 

Khi đó số các chia s1 cũng chính là số lượng chữ số 0 + 1

Tương tự ta làm như thế với s3. Tuy nhiên ở đây t sẽ duyệt ngược mảng.

Sau khi tìm được số các chia s1 và s3 thì số cách ở đây sẽ là s1 * s3 % 1000000007

Tại sao lại có sự tồn tại của `1000000007` ở đây. Đó chính là để tránh tràn bộ nhớ, về con số này thì các bạn có thể tìm hiểu sau



```swift
class Solution {
    func numWays(_ s: String) -> Int {
        let chars = Array(s)
        let mod = 1000000007
        var numberOneNumber = 0
        for char in chars {
            let int = Int(String(char))!
            if int == 1 {
                numberOneNumber += 1
            }
        }
        if numberOneNumber == 0 {
            var result = 0
            for item in 0...s.count - 2 {
                result += item
            }
            return ((s.count - 2)*(s.count - 1) / 2) % mod
        }
        if numberOneNumber % 3 != 0 {
            return 0
        }
        // So cach split s1
        var numberS1 = 0

        var index = 0
        var numberWayS1 = 0
        while numberS1 < numberOneNumber / 3 + 1 {
            let number = Int(String(chars[index]))
            if number == 1 {
                numberS1 += 1
            }
            if numberS1 == numberOneNumber / 3 {
                numberWayS1 += 1
            }
            index += 1
        }


        var numberWayS2 = 0 
        index = s.count - 1
        numberS1 = 0
        while numberS1 < numberOneNumber / 3 + 1 {
            let number = Int(String(chars[index]))
            if number == 1 {
                numberS1 += 1
            }
            if numberS1 == numberOneNumber / 3 {
                numberWayS2 += 1
            }
            index -= 1
        }
        return numberWayS1 * numberWayS2 % mod
    }
}
```

