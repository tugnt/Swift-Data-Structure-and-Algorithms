### Ý tưởng của thuật toán merge sort


Giống như Quick sort, Merge sort là một thuật toán chia để trị. Thuật toán này chia mảng cần sắp xếp thành 2 nửa. Tiếp tục lặp lại việc này ở các nửa mảng đã chia. Sau cùng gộp các nửa đó thành mảng đã sắp xếp. Hàm merge() được sử dụng để gộp hai nửa mảng. Hàm merge(arr, l, m, r) là tiến trình quan trọng nhất sẽ gộp hai nửa mảng thành 1 mảng sắp xếp, các nửa mảng là arr[l…m] và arr[m+1…r] sau khi gộp sẽ thành một mảng duy nhất đã sắp xếp. ( Chú ý mỗi nửa mảng cũng sẽ là 1 mảng đã được sắp xếp )

→　Bài toán trở thành việc merger 2 mảng đã sắp xếp thành 1 mảng sắp xếp
Hãy xem ý tưởng triển khai code dưới đây để hiểu hơn

![Merge-Sort-Tutorial](https://user-images.githubusercontent.com/14192303/113504397-d65a8900-9572-11eb-80e1-d275d674962b.png)

Như chúng ta đa thấy ở hình trên chúng ta sẽ chia cho đến khi các mảng chỉ có 1 phần tử và sau đó chúng ta sẽ bắt đầu merger các mảng này. Kết quả của phép merger chính là các mảng đã được sắp xếp. Bài toán còn lại cần giải quyết đó chính là merger 2 mảnh đã sắp xếp thành 1 mảng xắp xếp. 

Cách sắp xếp ở đây cũng khá là đơn giản chúng ta dùng 2 con trỏ chỉ đến index của mỗi mảng đã được sắp xếp. Và duyệt cho đến khi index của các con trỏ chạy đến vị trí cuối cũng của 2 mảng. 

Thuật toán có độ phức tạp là **0(n*logn)**

``` 
mergeSort(arr[], l,  r)
If r > l
     1. Tìm chỉ số nằm giữa mảng để chia mảng thành 2 nửa:
             middle m = (l+r)/2
     2. Gọi đệ quy hàm mergeSort cho nửa đầu tiên:   
             mergeSort(arr, l, m)
     3. Gọi đệ quy hàm mergeSort cho nửa thứ hai:
             mergeSort(arr, m+1, r)
     4. Gộp 2 nửa mảng đã sắp xếp ở (2) và (3):
             merge(arr, l, m, r)
```


```swift 

func mergeSort(arr: [Int]) -> [Int] {
    guard arr.count > 1 else { return arr }
    let middleVal = arr.count / 2
    let left = mergeSort(arr: Array(arr[0..<middleVal]))
    let right = mergeSort(arr: Array(arr[middleVal..<arr.count]))
    return merge(left: left, right: right)
}

func merge(left: [Int], right: [Int]) -> [Int] {
    if left.count == 0 {
        return right
    }
    if right.count == 0 {
        return left
    }
    
    var result = [Int]()
    var leftIndex = 0
    var rightIndex = 0
    while leftIndex < right.count, rightIndex < right.count {
        if left[leftIndex] < right[rightIndex] {
            result.append(left[leftIndex])
            leftIndex += 1
        } else {
            result.append(right[rightIndex])
            rightIndex += 1
        }
    }
    
    while leftIndex < left.count {
        result.append(left[leftIndex])
        leftIndex += 1
    }
    
    while rightIndex < right.count {
        result.append(right[rightIndex])
        rightIndex += 1
    }
    
    return result
}

```
