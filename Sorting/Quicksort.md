Thuật toán Quick Sort là một thuật toán sắp xếp, còn được gọi là sắp xếp kiểu phân chia (Part Sort). Là một thuật toán hiệu quả dựa trên việc phân chia mảng dữ liệu thành các nhóm phần tử nhỏ hơn.
Giải thuật sắp xếp nhanh chia mảng thành hai phần bằng cách so sánh từng phần tử của mảng với một phần tử được gọi là phần tử chốt. Một mảng bao gồm các phần tử nhỏ hơn hoặc bằng phần tử chốt và một mảng gồm các phần tử lớn hơn phần tử chốt.

Quá trình phân chia này diễn ra cho đến khi độ dài của các mảng con đều bằng 1. Với phương pháp đệ quy ta có thể sắp xếp nhanh các mảng con sau khi kết thúc chương trình ta được một mảng đã sắp xếp hoàn chỉnh.


```swift
func quickSort(arr: [Int]) -> [Int] {
    guard arr.count > 1 else { return arr }
    let middle = arr.count / 2
    let middleValue = arr[middle]
    let beforeArr = arr.filter{ $0 < middleValue }
    let middleArr = arr.filter{ $0 == middleValue }
    let afterArr = arr.filter{ $0 > middleValue }
    return quickSort(arr: beforeArr) + middleArr + quickSort(arr: afterArr)
}
```

**Giải thích**
- Thuật toán này có độ phức tạp trong trường hợp tốt nhất là O(n*logn) trong trường hợp xấu nhất là O(n). Độ phức tạp tốt nhất khi ta chọn được giá trị giữa nằm ở phần ở giữa giá trị của mảng. Còn trường hợp xấu nhất là giá trị ta chọn là giá trị nhỏ nhất or lớn nhất.

- Thuật toán này dùng kĩ thuật đệ quy để tính toán ta chia mảng ra thành 3 phần 1 phần giá trị nhỏ hơn giá trị giữa **arr[length / 2]** một phần lớn hơn giá trị giữa.  Sau đó ta cứ chia cho đến khi không chia nhỏ hơn đc nữa.
 
