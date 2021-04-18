
Thuật toán sắp xếp chèn thực hiện sắp xếp dãy số theo cách duyệt từng phần tử và chèn từng phần tử đó vào đúng vị trí trong mảng con(dãy số từ đầu đến phần tử phía trước nó) đã sắp xếp sao cho dãy số trong mảng sắp đã xếp đó vẫn đảm bảo tính chất của một dãy số tăng dần.

1. Khởi tạo mảng với dãy con đã sắp xếp có k = 1 phần tử(phần tử đầu tiên, phần tử có chỉ số 0)
2. Duyệt từng phần tử từ phần tử thứ 2, tại mỗi lần duyệt phần tử ở chỉ số i thì đặt phần tử đó vào một vị trí nào đó trong đoạn từ [0…i] sao cho dãy số từ [0…i] vẫn đảm bảo tính chất dãy số tăng dần. Sau mỗi lần duyệt, số phần tử đã được sắp xếp k trong mảng tăng thêm 1 phần tử.
3. Lặp cho tới khi duyệt hết tất cả các phần tử của mảng.

![insertionsort](https://user-images.githubusercontent.com/14192303/113504582-f76fa980-9573-11eb-8ffb-1087861470b9.png)

**Độ phức tạp** Trong mọi trường hợp thì đều là O(n^2)
```
Tốt nhất: O(n^2)
Trung bình:  O(n^2)
Xấu nhất: O(n^2)
```

```swift 
func selectionSort(arr: inout [Int]) -> [Int] {
    for (i, item) in arr.enumerated() {
        var curentIndex = i
        while curentIndex > 0, arr[curentIndex] < arr[curentIndex - 1] {
            let tmp = arr[curentIndex]
            arr[curentIndex] = arr[curentIndex - 1]
            arr[curentIndex - 1] = tmp
            curentIndex -= 1
        }
    }
    return arr
}
``` 
