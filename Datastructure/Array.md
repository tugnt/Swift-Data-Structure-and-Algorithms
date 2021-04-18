### Array

Có lẽ khi nói về mảng thì mọi người đã quá quen thuộc với cấu trúc dữ liệu này rồi. Đây là một trong những cấu trúc dữ liệu mà chúng ta sẽ thường xuyên làm việc rất là nhiều. Bởi vậy trong bài này mình sẽ không nói chi tiết về mảng là gì , cách thêm các phần tử vào mảng ra sao vv. Mà chúng ta sẽ cùng đi tìm hiểu những kiến thức nâng cao hơn về cấu trúc dữ liệu này.



### Searching

Một bài toán quan trọng nhất của cấu trúc dữ liệu mảng đó là bài toàn tìm kiếm một phần tử ở trong mảng cho trước. Thông thường, nó phụ thuộc vào tốc độ tìm kiếm một phần tử trong cấu trúc dữ liệu giúp lập trình viên đưa ra các lựa chọn thiết kế phù hợp với bài toán.

Có nhiều cách để tìm kiếm trong mảng nhưng hiện tại chúng ta sẽ tập trung vào những cách căn bản nhất. Tìm kiếm ở đây có nghĩa là xác nhận sự tồn tại, xuất hiện của 1 phần tử trong mảng đó hay không và trả về vị trí của nó.



Có 2 thuật toán tìm kiếm căn bản cho kiểu dữ liệu mảng đó là

- Linear Search (Tìm kiếm tuyến tính)
- Binary Search (Tìm kiếm nhị phân)

### Linear Search (Tìm kiếm tuyến tính)

Đúng như tên gọi của nó, tìm kiếm tuyến tính có nghĩa là chúng ta sẽ duyệt mảng từ phần tử đầu tiên cho đến khi tìm thấy phần tử cần tìm or đến khi kết thúc mảng. Kỹ thuật này sử dụng cách kiểm tra từng phần tử trong mang theo một thứ tự nhất định nên gọi nó là tìm kiếm tuyến tính. Phương thức này dễ cài đặt và hay được sử dụng tuy nhiên thời gian chạy trong trường hợp xấu nhất là `O(n)`. Bởi vậy, với những bài toán cần tối ưu hoá phương thức tìm kiếm thì cách này không phải là tốt nhất.



### Binary Search (Tìm kiếm nhị phân)

Có một cách khác để tìm kiếm một mảng. Nếu các phần tử trong mảng đã được sắp xếp theo một thứ tự (tăng dần, or giảm dần) thì chúng ta có thể sử dụng tìm kiếm nhị phân. Tìm kiếm nhị phân là cách chúng ta liên tục chia mảng thành 2 phần `left`  và `right` và sau đó là xác định phần tử cần tìm kiếm nằm ở mảng bên trái `left` hay là `right` (mảng bên phải). Mỗi lần chúng ta chia đôi mảng ra như vậy chúng ta có thể giảm thời gian tìm kiếm đi 1/2, việc này làm cho tìm kiếm nhị phân nhanh hơn rất nhiều so với tìm kiếm tuyến tính.

Tuy nhiên, nhược điểm của tìm kiếm nhị phân đó chính là nó chỉ thực hiện được trên input đã sắp xếp. Nếu chúng ta tìm kiếm với một bộ dữ liệu input không được sắp xếp thì tìm kiếm tuyến tính sẽ là đơn giản hơn và nhanh hơn. Bởi vì nếu chúng ta sắp xếp sau đó lại tìm kiếm thêm 1 lần nữa thì nó sẽ lâu hơn rất nhiều lần(Thuật toán sắp xếp nhanh nhất có độ phức tạp là O(nlogn)).



### In-place Array Operations (Xử lý mảng tại chỗ)

Trong các cuộc phỏng vấn lập trình về thuật toán, người phỏng vấn thường luôn mong bạn tối ưu thời gian chạy **(time complexity)** và không gian **(space complexity)** trong việc thực hiện thuật toán. Các phép toán mảng tại chỗ (in-place array operation) giúp giảm bớt sự phức tạp về không gian và do đó là một loại kỹ thuật mà hầu hết mọi người đều gặp phải thường xuyên trong các cuộc phỏng vấn.

**Vậy, các phép toán mảng tại chỗ là gì?**

Cách tốt nhất để trả lời câu hỏi này là xem một ví dụ dưới đây

`Cho một mảng và trả về 1 mảng bình phương giá trị ở những phần tử có chỉ mục index chẵn.`

```
Input: array = [9, -2, -9, 11, 56, -12, -3]
Output: [81, -2, 81, 11, 3136, -12, 9]
```

Bài toán này khá là đơn giản, có 2 cách tiếp cận bài toán này. 

- Cách 1 tạo 1 array mới với kích thước bằng với input. Sau đó chúng ta sao chép những phần tử có index lẻ vào array mới và bình phương các phần tử có chỉ mục index là chẵn.
  - Cách tiếp cận này là chính xác , nó giải quyết được bài toán. Tuy nhiên nó không hiệu quả, bởi vì chúng ta phải tạo ra thêm 1 mảng có kích thước là `length`. ( hay còn gọi là sử dụng O(length) space or space complexity = O(length))
- Cách 2: Chúng ta duyệt mảng và ghi đè lên phần tử có chỉ mục chẵn = giá trị chính nó bình phương. Cách tiếp cận này chúng ta đã giải quyết được vấn đề không tạo ra thêm vùng nhớ mới. Cách làm này gọi là `in-place array operation`

Một điều lưu ý với 2 cách tiếp cận đó là với cách 2 thì chúng ta đã sửa trực tiếp lên input đầu vào. Bởi vậy chúng ta không còn có thể truy cập được dữ liệu gốc ban đầu nữa. Vì vậy, tuỳ vào những bài toán chúng ta sẽ tìm cách tiếp cận và giải quyết cho phù hợp.







