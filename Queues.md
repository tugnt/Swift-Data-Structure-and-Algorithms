### Queue 
`Queue` là một cấu trúc dữ liệu danh sách nơi mà bạn có thể insert item vào cuối và lấy ra ở phía đầu. Điều này đảm bảo là phần tử vào đầu tiên thì cũng sẽ là phần tử được lấy ra đầu tiên. Điều này hoàn toàn giống vs trong cuộc sống đến trước thì phục vụ trước.

Vậy tại sao chúng ta cần `Queue`? Trong nhiều thuật toán, bạn muốn thêm các đối tượng vào danh sách tạm thời và kéo chúng ra khỏi danh sách này sau. Thông thường, thứ tự mà bạn thêm và xóa các đối tượng này rất quan trọng.

Các phương thức của Queue:
- enqueue: Chính là phương thức thêm phần tử vào cuối hàng đợi 
- dequeue: là phương thức lấy phần tử đầu tiên của hàng đợi. 

Ví dụ: Chúng ta sẽ thêm phần tử 10 vào Queue

```swift 
queue.enqueue(10)
```

Bây giờ giá trị của queue là `[10]`. Thêm tiếp phần tử 5 vào.

```swift 
queue.enqueue(5)
```

queue = [10, 5]. Bây giờ chúng ta sẽ lấy phần tử đầu tiên của queue bằng cách gọi `dequeue`

```swift
queue.dequeue()
```
Câu lệnh trên sẽ trả về giá trị là 5 và queue = [10]


> Chú ý: Hàng đợi `Queue` không phải lúc nào cũng là sự lựa chọn tốt nhất. Nếu thứ tự các mục được thêm vào và xóa khỏi danh sách không quan trọng, bạn có thể sử dụng ngăn xếp thay vì hàng đợi. Các ngăn xếp đơn giản hơn và nhanh hơn.
