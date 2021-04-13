### Cấu trúc dữ liệu LIFO 

<img width="528" alt="screen-shot-2018-06-02-at-203523" src="https://user-images.githubusercontent.com/14192303/114582642-bb4af000-9cbb-11eb-9480-3c5105a6cede.png">


Trong cấu trúc dữ liệu LIFO, phần tử mới nhất được thêm vào hàng đợi sẽ được xử lý đầu tiên.

Khác với hàng đợi, ngăn xếp là một cấu trúc dữ liệu LIFO. Thông thường, hoạt động `insert` phần tử được gọi là `push` trong một ngăn xếp. 
Tương tự như hàng đợi, một phần tử mới luôn được thêm vào cuối `stack`. Tuy nhiên, thao tác `delete, pop` sẽ luôn xóa phần tử cuối cùng (ngược với hàng đợi).

**Ví dụ:**

1. Khi thêm phân tử 8 vào trong `stack` thì nó sẽ luôn đc insert phía trên cùng của cuốn sách. Giống như bạn đặt một cuốn sách lên phía trên cùng của chồng sách.
2. Cũng giống như khi lấy cuốn sách ở trên cùng của chồng sách thì `pop` trong stack cũng sẽ luôn luôn lấy phần tử phía cuối cùng.

<img width="212" alt="screen-shot-2018-06-03-at-113737" src="https://user-images.githubusercontent.com/14192303/114583385-80958780-9cbc-11eb-9c45-d96e96626d7e.png"> <img width="218" alt="screen-shot-2018-06-03-at-113755" src="https://user-images.githubusercontent.com/14192303/114583446-8d19e000-9cbc-11eb-8276-248432d1e596.png">


Ví dụ chúng ta sẽ `push` phần tử `5` vào trong `Stack`

```swift
stack.push(5)
```
Bây giờ stack sẽ có 1 phần tử là `[5]`. Bây giờ chúng ta sẽ `push` thêm 1 phần tử nữa vào.

```swift
stack.push(3)
``` 
Bây giờ giá trị của stack là [ 5, 3 ]. Chúng ta sẽ thử `pop` lấy giá trị vừa thêm vào cuối cùng trong stack.

```swift 
stack.pop()
```
Chúng ta sẽ nhận đc giá trị là 3. Bởi vì nó là giá trị cuối cùng mà chúng ta thêm vào `Stack`. Sau khi lấy giá trị `3` thì stack trở thành `[5]`

Dưới đây là impement của cấu trúc dữ liệu `Stack` được viết bằng Swift 

```swift
public struct Stack<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }

  public mutating func push(_ element: T) {
    array.append(element)
  }

  public mutating func pop() -> T? {
    return array.popLast()
  }

  public var top: T? {
    return array.last
  }
}
```

Vậy chúng ta cùng xem xét việc này so với cấu trúc dữ liệu mảng là gì. Nếu để ý thì chúng ta sẽ thấy `push` luôn chèn phần tử vào cuối mỗi mảng( `stack`) , việc này sẽ nhanh hơn với việc chèn phần tử ở đầu mảng vì chúng ta sẽ phải dịch chuyển mỗi phần tử thêm 1 index(O(n)). Vì vậy việc chèn phần tử vào cuối chỉ tốn O(1) bất kể kích thuóc của mảng là lớn như thế nào.

- Tràn ngăn xếp (Stack over flow): Vấn đề này xảy ra khi bộ nhớ stack của CPU bị hết dung lượng khi bạn gọi quá nhiều hàm or gọi hàm đệ quy không bao giờ kết thúc. 
