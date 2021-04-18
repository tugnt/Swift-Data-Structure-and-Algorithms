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

### Code 

```swift 
public struct Queue<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }
  
  public var count: Int {
    return array.count
  }

  public mutating func enqueue(_ element: T) {
    array.append(element)
  }
  
  public mutating func dequeue() -> T? {
    if isEmpty {
      return nil
    } else {
      return array.removeFirst()
    }
  }
  
  public var front: T? {
    return array.first
  }
}
```

Queue thì hoạt động tốt tuy nhiên đó không phải là tốt nhất.
`Enqueuing` luôn tốn thời gian là O(1) bất kể kích thước của mảng là bao nhiêu bởi vì nó luôn luôn đặt ở cuối mỗi mảng.

Có thể bạn sẽ thắc mắc tại sao thêm 1 phần tử vào cuối mỗi mảng thì thời gian là O(1) or một khoảng thời gian không đổi. Bởi vì trong Swift ở cuối mỗi mảng luôn có một số phần tử trống như dưới đây.

```swift
var queue = Queue<String>()
queue.enqueue("Ada")
queue.enqueue("Steve")
queue.enqueue("Tim")
```
Sau khi thêm 3 phần tử thì kết quả sẽ như sau: `[ "Ada", "Steve", "Tim", xxx, xxx, xxx ]` trong đó xxx chính là bộ nhớ mà chưa được sử dụng. Nếu chúng ta thêm tiếp các phần từ vào trong mảng thì sẽ ghi đè lên vùng nhớ đó.  `[ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]`. Việc này chỉ đơn giản là copy vùng nhớ từ nơi này sang nơi khác và đó luôn là thời gian không đổi.

Chỉ có một số điểm khi thêm phần tử vào vị trí cuối của mảng, đó là khi ta thêm vào phần tử xxx cuối cùng trong mảng khi đó bộ nhớ của mảng cần phải được mở rộng và cần phải thay đổi kích thước để có thể thêm vào những phần tử mới.

Việc thay đổi kích thước của nghĩa là chúng ta sẽ khai báo một vùng nhớ mới, cấp phát bộ nhớ cho chúng, copy dữ liệu từ mảng hiện có sang mảng mới. Để thực hiện việc này thì trung bình tốn O(n) time với n là kích thước mảng. Tuy nhiên, điều này cũng hiếm khi xảy ra bởi vậy việc thêm vào cuối mảng vẫn được coi là nhanh với thời gian thực hiện là 0(1).

Tuy nhiên câu chuyện khi chúng ta lấy phần tử đầu tiên của queue (dequeue) thì là một câu chuyện khác. Sau khi chúng ta lấy phần tử đầu tiên ra khỏi mảng thì các phần tử phía sau sẽ phải di chuyển lên phía trước 1 index. Việc này tiêu tốn n-1 time với n là số phần tử của mảng ban đầu. 

Chúng ta hãy xem qua ví dụ nếu ta gọi `dequeue` dữ liệu đã được thêm lúc trước thì kết quả sẽ ra sao.

```
before   [ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]
                   /       /      /
                  /       /      /
                 /       /      /
                /       /      /
after   [ "Steve", "Tim", "Grace", xxx, xxx, xxx ]
```

Như chúng ta đã thấy, phần tử `Ada` sẽ được lấy ra và các phần tử phía sau sẽ di chuyển lên trước 1 index. Việc này sẽ tốn O(n) time, vì vậy với kiểu dữ liệu Queue thì việc `enqueue` thì khá là nhanh tuy nhiên việc lấy phần tử ra `dequeue` thì sẽ chậm hơn rất nhiều. Và đó cũng chính là nhược điểm của queue.
**Vậy có cách nào cải tiến Queue một cách hiệu quả hơn không ?**

Để cải tiến `Queue` hiệu quả hơn thì chúng ta sẽ phải tìm cách làm sao để `dequeue` hiệu quả hơn. Chúng ta có thể thêm 1 số không gian trống ở trước 1 mảng, tuy nhiên `Swift` không hỗ trợ kiểu dữ liệu này và chúng ta sẽ phải tự giải quyết.
Ý tưởng của cách giải quyết này đó chính là khi chúng ta gọi `dequeue` thì chúng ta sẽ không di chuyển chỉ mục của các phần tử phía sau thêm 1 index. Mà chúng ta sẽ gán giá trị của phần tử đầu tiên bằng null (xxx)


Ví dụ sau khi chúng ta `dequeue(Ada)` thì mảng sẽ trở thành 

```
[ xxx, "Steve", "Tim", "Grace", xxx, xxx ]
```
Tiếp tuc `dequeue(Steve)` -> `[ xxx, xxx , "Tim", "Grace", xxx, xxx ]`.
Bởi vì những phần tử trống ở phía trước sẽ không bao giờ được sử dụng chúng ta sẽ di chuyển chúng lên trước định kỳ. 

```
[ "Tim", "Grace", xxx, xxx, xxx, xxx ]
```
Và tất nhiên việc di chuyển này tốn O(n) time, tuy nhiên việc này chúng ta sẽ chỉ phải làm 1 vài lần trong khi những lần `dequeue` khá thì tốn O(1) time. Nhìn chung lại thì cách tiếp cận này hiệu quả hơn nhiều so với sử dụng `Queue` truyền thống.

Dưới đây là triển khai code của Queue
```swift
public struct Queue<T> {
  fileprivate var array = [T?]()
  fileprivate var head = 0
  
  public var isEmpty: Bool {
    return count == 0
  }

  public var count: Int {
    return array.count - head
  }
  
  public mutating func enqueue(_ element: T) {
    array.append(element)
  }
  
  public mutating func dequeue() -> T? {
    guard head < array.count, let element = array[head] else { return nil }

    array[head] = nil
    head += 1

    let percentage = Double(head)/Double(array.count)
    if array.count > 50 && percentage > 0.25 {
      array.removeFirst(head)
      head = 0
    }
    
    return element
  }
  
  public var front: T? {
    if isEmpty {
      return nil
    } else {
      return array[head]
    }
  }
}

```

Như chúng ta thấy ở đây, mảng này sẽ lưu giá trị là `T?`. thay vì `T` bởi vì chúng ta khi lấy 1 phần tử ra khỏi mảng thì sẽ gán giá trị `nil(null)` cho nó.  Và `head` ở đây cũng chính là chỉ số index của phần tử mang giá trị đầu tiên .

```
[ "Ada", "Steve", "Tim", "Grace", xxx, xxx ]
  head
```

```
[ xxx, "Steve", "Tim", "Grace", xxx, xxx ]
        head
```

Bạn hãy tưởng tượng giống như một hàng dài người đứng thanh toán tại quầy. Thay vì chúng ta chạy đến quầy thì người thanh toán sẽ tự chạy đến chỗ chúng ta. Nếu chúng ta không bao giờ loại bỏ những phần tử trống phía trước thì mảng sẽ tiếp tục phát triển cho đến khi chúng ta sắp xếp lại các phần tử trống ở phía trước. Để giảm bớt các phần tử trống chúng ta sẽ thực hiện như sau

```swift
    let percentage = Double(head)/Double(array.count)
    if array.count > 50 && percentage > 0.25 {
      array.removeFirst(head)
      head = 0
    }
```

Chúng ta sẽ tính tỉ lệ % những phần tử không dùng so với tỉ lệ tất cả các phần tử trong mảng. Nếu tỉ lệ > 25% thì chúng ta sẽ bắt đầu sắp xếp lại mảng. Nếu số phần tử trong mảng nhỏ hơn 50 thì chúng ta không cần phải sắp xếp lại bởi vì sự khác biệt ở đây là không nhiều. 
**Chú ý:** Bạn có thể tự thay đổi những con số sao cho phù hợp với từng bài toán.

Kết quả test queue sau khi đã cải tiến
```swift
var q = Queue<String>()
q.array                   // [] empty array

q.enqueue("Ada")
q.enqueue("Steve")
q.enqueue("Tim")
q.array             // [{Some "Ada"}, {Some "Steve"}, {Some "Tim"}]
q.count             // 3

q.dequeue()         // "Ada"
q.array             // [nil, {Some "Steve"}, {Some "Tim"}]
q.count             // 2

q.dequeue()         // "Steve"
q.array             // [nil, nil, {Some "Tim"}]
q.count             // 1

q.enqueue("Grace")
q.array             // [nil, nil, {Some "Tim"}, {Some "Grace"}]
q.count             // 2

```

