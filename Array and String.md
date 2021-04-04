# Array And String
#google/data_structures

### Introduction

`Array` là một trong những kiểu dữ liệu cơ bản trong data structure. Về cơ bản thì `String` bao gồm mọt array các character nên nó cũng chỉ là 1 mảng.  Hầu hết các cuộc phỏng vấn về lập trình hỏi về cấu trúc dữ liệu này.
Trong phần này chúng ta sẽ cùng tìm hiểu về `array` và `string`. Sau khi hoàn thành xong bài này bạn có thể:

1. Hiểu được sự khác nhau giữa `array` và `dynamic array`
2. Làm quen với các thao tác trên `array` và `dynamic array`
3. Hiểu đc mảng đa chiều và sử dụng mảng 2 chiều
4. Hiểu khái niệm về chuỗi và các tính năng khác nhau mà chuỗi có;
5. Sử dụng kỹ thuật `two-pointer ` để giải quyết một số bài toán

Trong array các phần tử có thể được truy cập ngẫu nhiên vì mỗi phần tử trong mảng có thể được xác định bằng một chỉ số mảng.
Mảng có thể có một hoặc nhiều kích thước. Ở đây chúng ta bắt đầu với mảng một chiều, còn được gọi là mảng tuyến tính.

<img width="562" alt="screen-shot-2018-03-20-at-191856" src="https://user-images.githubusercontent.com/14192303/113501067-bff60280-955d-11eb-98c5-71ea49b2192a.png">

 Trong ví dụ trên, có 6 phần tử trong mảng A. Tức là độ dài của A là 6. Chúng ta có thể sử dụng A [0] để biểu diễn phần tử đầu tiên trong mảng. Tương tự, A [1] = 3, A [2] = 8, v.v.
 
 ### Introduction to Dynamic Array
 
 Như chúng ta đã nói ở trên, một mảng có kích thước được xác định và chúng ta phải biết trước được kích thước của mảng trước khi khởi tạo. Điều này gây ra  khó khăn và lãng phí. Do đó, hầu hết các ngôn ngữ lập trình đều cung cấp mảng động tích hợp sẵn vẫn là cấu trúc dữ liệu danh sách truy cập ngẫu nhiên nhưng với kích thước thay đổi. Ví dụ, chúng ta có vector trong C ++ và ArrayList trong Java.
 
 ###  Two-pointer Technique - Scenario I
 
 Trong chương trước chúng ta đã giải quyết một số vấn đề bằng cách lặp lại mảng. Thông thường chúng ta chỉ sử dụng 1 con trỏ chạy từ chỉ mục đầu tiên của mảng đến phần tử cuối cùng của mảng. Tuy nhiên, đôi lúc chúng ta cần sử dụng 2 con trỏ để thực hiện việc lặp này.
 
**Ví dụ**
Chúng ta hãy bắt đầu với ví dụ cơ bản sau. 
`Đảo ngược tất cả các phần tử trong mảng.`

Ý tưởng là hoán đổi phần tử đầu tiên với phần cuối, tiến tới phần tử tiếp theo và hoán đổi nhiều lần cho đến khi nó đạt đến vị trí giữa. 
Chúng ta có thể sử dụng cùng lúc hai con trỏ để thực hiện lặp: một con bắt đầu từ phần tử đầu tiên và con trỏ khác bắt đầu từ phần tử cuối cùng. Tiếp tục hoán đổi các phần tử cho đến khi hai con trỏ gặp nhau

 ###  Two-pointer Technique - Scenario II
 
 Đôi khi chúng ta có thể sử dụng hai con trỏ với bước nhảy khác nhau để giải quyết bài toán.
 Chúng ta sẽ cùng xem xét qua ví dụ dưới đây để hiểu rõ hơn
 
 `Cho một mảng arr và một số K hãy xoá tất cả phần tử có giá trị bằng K và trả về độ dài của mảng sau khi xoá. Sử dụng kĩ thuật in-place có nghĩa là thay đổi ngay trên mảng đầu vào , không sử dụng mảng mới`
 
Nếu chúng ta không gặp phải giới hạn về độ phức tạp của không gian, thì mọi việc sẽ dễ dàng hơn. Lặp lại mảng ban đầu và thêm phần tử vào mảng mới nếu phần tử không bằng giá trị K đã cho.

Trên thực tế thì việc trên cũng tương đương với sử dụng 2 con trỏ, một con để lặp mảng ban đầu và một con để trỏ vào vị trí cuối cùng của mảng mới. 

Bây giờ chúng ta hãy xem xét lại giới hạn không gian.

Chúng ta có thể sử dụng một chiến lược tương tự. Chúng tôi vẫn sử dụng hai con trỏ: một con vẫn được sử dụng để lặp lại trong khi con trỏ thứ hai luôn trỏ vào vị trí mà chúng ta vừa mới thay đổi giá trị. 

Đây là mã để bạn tham khảo:

```java 
public int removeElement(int[] nums, int val) {
    int k = 0;
    for (int i = 0; i < nums.length; ++i) {
        if (nums[i] != val) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}
```

Chúng ta sử dụng 2 con trỏ i và k. Con trỏ i thì chạy nhanh hơn duyệt qua các phần tử của mảng từ đầu tới cuối, trong khi con trỏ k chỉ được tăng giá trị khi mà gia trị trong phần tử index khác với K. Bằng cách này chúng ta có thể xoá tất cả các phần từ có giá trị bằng `val` mà không cần phải sử dụng thêm mảng mới. Do đó space complexcity ở đây là O(1)


### Array-related Techniques

Có nhiều cấu trúc hoặc kỹ thuật dữ liệu liên quan đến mảng mà bạn có thể muốn biết. Chúng ta sẽ đi sâu về chúng trong những bài tiếp theo

1. Có một số cấu trúc dữ liệu khác tương tự như mảng như dưới đây:

- String (đã được giới thiệu trong thẻ này
- Hash table
- Linked List
- Queue
- Stack

2. Như chúng ta đã đề cập, chúng ta có thể sử dụng ` built-in function` ( Là những thuật toán đã được thiết kế sẵn) để sắp xếp một mảng. Nhưng sẽ rất hữu ích nếu hiểu nguyên tắc của một số thuật toán sắp xếp được sử dụng rộng rãi và độ phức tạp của chúng.

3. Tìm kiếm nhị phân cũng là một kỹ thuật quan trọng được sử dụng để tìm kiếm một phần tử cụ thể trong một mảng đã được sắp xếp.

4. Chúng tôi đã giới thiệu kỹ thuật hai con trỏ trong chương này. Không dễ để sử dụng linh hoạt kỹ thuật này. Kỹ thuật này cũng có thể được sử dụng để giải quyết:

- Slow-pointer and fast-pointer problem in Linked List
- Sliding Window Problem

5. Kỹ thuật hai con trỏ đôi khi sẽ liên quan đến Thuật toán tham lam giúp chúng ta thiết kế chiến lược di chuyển của con trỏ.

Các kĩ thuật về về sử dụng two pointer chúng ta sẽ tìm hiểu ở những bài tiếp theo.
