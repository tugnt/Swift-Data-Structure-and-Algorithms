# Linked list
#google/data_structures
**Danh sách liên kết đơn**
Với mỗi nốt trong danh sách liên kết đơn không chỉ bao gồm giá trị mà nó còn bao gồm 1 con trỏ đến vị trí của node tiếp theo trong danh sách.
Bằng cách này danh sách liên kết đơn sắp xếp tất cả các giá trị theo một trình tự như dưới đây

![](Linked%20list/screen-shot-2018-04-12-at-152754.png)

Các mũi tên màu xanh lam cho biết cách các nút trong danh sách được liên kết đơn được kết hợp với nhau.

**Cấu trúc của một node**
Đoạn code dưới đây sẽ định nghĩa 1 node trong danh sách liên kết đơn ( Su dung ngon ngu Swift)

```swift
class SinglyListNode<T> {
	let value: T
	let nextNode: SinglyListNode?
	weak var previousNode: SinglyListNode?

	init(value: T) {
		value = value
	}
}
```

Trong hầu hết trường hợp chúng ta sẽ sử dụng node đầu tiên là `head` để đại diện cho Linked List

**Cách hoạt động của Linked List**

Không giống như array chúng ta không thể truy cập vào giá trị cụ thể của mảng trong thời gian O(1). Nếu chúng ta muốn truy cập phần tử thứ. `i` của Linked List thì chúng ta bắt buộc phải chạy từ phần tử `head` đầu tiên. Và việc này tốn thời gian là O(i).

Chúng ta cùng xem xét ví dụ trong hình được đưa ra ở trên, `head` ở đây mang giá trị là `23`. Cách duy nhất truy cập đến giá trị thứ 3 là `15` đó là từ node `head` truy cập vào giá trị thứ 2, sau đó từ node thứ 2 truy cập vào giá trị thứ 3.

Chắc hẳn đến đây bạn sẽ thắc mắc tại sao lại cần phải có danh sách liên kết (Linked List) trong khi hiệu suất của nó kém so với mảng trong việc truy cập dữ liệu dựa theo chỉ mục.  Ở phần tiếp theo tôi sẽ trình bày các thao tác `insert` và `delete` giá trị trong `Linked List` từ đó bạn sẽ nhận ra lợi ích của sanh sách liên kết so với mảng.

### Thêm phần tử vào danh sách liên kết
- - - -
1. **Thêm node vào vị trí bất kì**
Nếu chúng ta muốn thêm 1 node vào sau `prev` thì việc cần làm đó là:
	1. Khởi tạo một node cur như dưới 
	![](Linked%20list/screen-shot-2018-04-25-at-163224.png)
	2. Link con trỏ của `cur` đến node tiếp theo của `prev` đó chính là node `next`
	![](Linked%20list/screen-shot-2018-04-25-at-163234.png)
	3. Link con trỏ của `prev` đến `cur`
![](Linked%20list/screen-shot-2018-04-25-at-163243.png)

Không giống như trong array nếu chúng ta muốn thêm một giá trị vào mảng ở vị trí thứ i thì chúng ta sẽ phải move tất cả các phần từ từ vị trí i+1 đến phần tử cuối cùng của mảng. Bởi vậy chúng ta có thể thêm phần tử vào trong `Linked List` với độ phức tạp là `O(1)`

2. **Thêm node vào trị trí đầu tiên**
Như chúng ta đã nhắc đến đó là Linked List sử dụng phần tử đầu tiên là `head` để đại diện cho chính nó.  Vì vậy, điều cần thiết là phải cập nhật head khi thêm một nút mới vào đầu danh sách.

	* Khởi tạo một node mới gọi là `cur`
	* Liên kết node mới với node đầu ban đầu
	* Chỉ định `cur` cho head.
**Ví dụ:** 
Chúng ta khởi tạo 1 node mới với giá trị là 9.  Sau đó gán con trỏ của node này trỏ đến `head` ban đầu.
![](Linked%20list/screen-shot-2018-04-19-at-125118.png)

Sau đó gán new head là node có giá trị là 9
![](Linked%20list/screen-shot-2018-04-19-at-125350.png)

Vậy còn nếu chúng ta thêm 1 node vào cuối cùng thì sao? Đây chính là bài tập dành cho bạn


### Thao tác xoá phần tử trong danh sách liên kết
- - - -
1. **Xoá node bất kì trong Linked List**
Nếu bạn muốn xoá 1 node `cur` trong Linked List thì cần làm theo 2 bước sau
	1. Tìm node phía trước của node `cur` và phần tử tiếp theo của `cur` . 
![](Linked%20list/screen-shot-2018-04-26-at-203558.png)
	2. Gán con trỏ của `prev` cho `nex`
![](Linked%20list/screen-shot-2018-04-26-at-203640.png)

Cũng giống như thao tác thêm 1 node vào Linked List thì chúng ta không phải duyệt toàn bộ mảng vì vậy thao tác này chỉ mất `O(1)` trong khi thao tác trên mảng sẽ mất `O(n)` thời gian

2. **Xoá node đầu**

Cũng giống như việc thêm node đầu thì việc xoá node đầu cũng khá là đơn giản. Chúng ta chỉ cần chỉ định `head` chính là next node của node đầu tiên.
![](Linked%20list/screen-shot-2018-04-19-at-130031.png)


**Thiết kế Linked List**
Bây giờ chúng ta sẽ đi thực hành thiết kế 1 Linked List sử dụng ngôn ngữ Swift. Trước khi bắt đầu viết code thì chúng ta cần làm rõ những vấn đề sau.  Nó sẽ có các chức năng như sau
**get(int index):** Trả về giá trị của phần tử thứ index
**addAtHead(int val)**: Thêm 1 node vào `head`
**addAtTail(int val)**: Thêm 1 node vào `tail`
**addAtIndex(int index, int val)**: Thêm 1 node có giá trị `val` vào vị trí index
**deleteAtIndex(int index)**: Xoá node thứ index

```swift
class Node {
    var value: Int
    var next: Node?
    weak var prev: Node?
    
    init(value: Int) {
        self.value = value
    }
}


class MyLinkedList {
    var head: Node?

    init() {
        
    }
    
    /** Lấy giá trị của node thứ index trong Linked List và trả về giá trị đó , nếu ko tồn tại node đó thì trả về -1. */
    func get(_ index: Int) -> Int {
        guard head != nil else { return -1 }
        var node = self.head
        var curentNodeIndex = 0
        while curentNodeIndex < index {
            node = node?.next
            curentNodeIndex += 1
        }
        return node?.value ?? -1
    }
    
    /** Add node vào đầu của Linked List. */
    func addAtHead(_ val: Int) {
        if let headNode = head {
            let node = Node(value: val)
            node.next = head
            head = node
        } else {
            let node = Node(value: val)
            head = node
        }
    }
    
    /** Add node vào đuôi của Linked List */
    func addAtTail(_ val: Int) {
        guard head != nil else {
            self.head = Node(value: val)
            return
        }
        var tailNode = self.head
        while tailNode?.next != nil {
            if let tail = tailNode?.next {
                tailNode = tail
            }
        }
        
        // 2. Add tailNode = newNode
        let newNode = Node(value: val)
        tailNode?.next = newNode
    }
    
    /** Add Node vào index của Linked List */
    func addAtIndex(_ index: Int, _ val: Int) {
        let newNode = Node(value: val)
        guard head != nil else {
            head = newNode
            return
        }
        if index == 0 {
            // Add head
            addAtHead(val)
            return
        }
        
        var node = self.head
        var curentNodeIndex = 0
        // 1. cur to next node
        while curentNodeIndex < index - 1{
            node = node?.next
            curentNodeIndex += 1
        }
        newNode.next = node?.next
        node?.next = newNode
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    func deleteAtIndex(_ index: Int) {
        if index == 0 {
            head = head?.next
            return
        }
        var nodeIndex = 0
        var node = self.head
        while nodeIndex < index - 1 {
            node = node?.next
            nodeIndex += 1
        }
        node?.next = node?.next?.next
    }
}

```


### Hai con trỏ trong danh sách liên kết
- - - -
Chúng ta hãy xem xét qua một vấn đề kinh điển
`Cho một danh sách liên kết, hãy xác định xem nó có là một dach sách liên kết vòng hay không(Có nghĩa là tail.next = head`

Bạn có thể đưa ra giải pháp đó là sử dụng `hash table` . Nhưng có một giải pháp đơn giản hơn đó chính là sử dụng kĩ thuật `two pointer`. Hãy cố gắng suy nghĩa về kĩ thuật này trước khi đọc nội dung tiếp theo. 

Chúng ta hãy tưởng tượng như là 2 người cùng chạy trên 1 đường thẳng thì người nào chạy nhanh hơn sẽ về đích trước. Tuy nhiên, nếu chạy theo vòng tròn thì sẽ có 1 lúc nào đó người chạy nhanh hơn sẽ gặp người chạy chạy hơn ở một thời điểm nào đó.

Đó chính xác là những gì chúng ta sẽ gặp khi sử dụng 2 con trở có tốc độ khác nhau ở Linked List.
	1. Nếu mà không phải là danh sách liên kết vòng, thì còn trỏ tốc độ nhanh hơn sẽ kết thúc ở cuối danh sách liên kết.
	2. Nếu là danh sách liên kết vòng thì con trỏ nhanh hơn sẽ gặp con trỏ chậm ở một thời điểm nào đó.

Vấn đề còn lại ở đây là 
`Tốc độ của hai con trỏ nên chọn như thế nào cho thích hợp ?`

Lựa chọn an toàn đó là con trỏ chậm sẽ chạy one-step và con trỏ nhanh sẽ chạy 2-step mỗi bước chạy.  Nếu độ dài của chu kỳ là M thì sau M lặp đi lặp lại, con trỏ nhanh chắc chắn sẽ di chuyển thêm một chu kỳ và bắt kịp con trỏ chậm.

`Còn những lựa chọn khác thì sao? Chúng có hoạt động không? Chúng có hiệu quả hơn không?`

- - - -
**Bài tập**
1. 
Given head, the head of a linked list, determine if the linked list has a cycle in it.
There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail’s next pointer is connected to. **Note that pos is not passed as a parameter**.
Return true*if there is a cycle in the linked list*. Otherwise, return false.
 
**Example 1:**
![](Linked%20list/circularlinkedlist.png)**Input:** head = [3,2,0,-4], pos = 1
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
**Example 2:**
![](Linked%20list/circularlinkedlist_test2.png)

**Input:** head = [1,2], pos = 0
**Output:** true
**Explanation:** There is a cycle in the linked list, where the tail connects to the 0th node.

**Example 3:**
![](Linked%20list/circularlinkedlist_test3.png)
**Input:** head = [1], pos = -1
**Output:** false
**Explanation:** There is no cycle in the linked list.
 
**Constraints:**
* The number of the nodes in the list is in the range [0, 104].
* -105 <= Node.val <= 105
* pos is -1 or a **valid index** in the linked-list.
 
**Follow up:** Can you solve it using O(1) (i.e. constant) memory?
 
```swift
public class ListNode {
    public var val: Int
    public var next: ListNode?
    public init(_ val: Int) {
        self.val = val
        self.next = nil
    }
}

class Solution {
    func hasCycle(_ head: ListNode?) -> Bool {
		 if head?.next == nil {
            return false
        }
        var slowNode = head
        var fastNode = head
        while fastNode?.next != nil {
            //showNode
            slowNode = slowNode?.next // 1 step
            fastNode = fastNode?.next?.next // 2 step
            // Phải kiểm tra trong này xem nó có gặp nhau hay ko
            if slowNode === fastNode {
                return true
            }
        }
        
        return false
    }
}
```



