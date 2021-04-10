### Algorithm Efficiency (Hiệu quả của thuật toán)

Chúng ta thường nói rằng thuật toán này hiệu quả hơn thuật toán kia, thuật toán A chạy nhanh hơn thuật toán B. Vậy chúng ta dựa vào tiêu chí nào để đánh giá một thuật toán là hiệu quả. 

Độ phức tạp của thuật toán là một hàm mô tả hiệu quả của thuật toán về lượng dữ liệu mà thuật toán phải xử lý.  Có hai thước đo độ phức tạp chính về hiệu quả của một thuật toán:
- Time complexity( Độ phức tạp thời gian hay còn gọi là thời gian chạy):  là một hàm mô tả thời gian một thuật toán thực hiện với một lượng dữ liệu đầu vào. "Thời gian" có thể có nghĩa là số lần truy cập bộ nhớ được thực hiện, số lần so sánh giữa các số nguyên, số lần một số vòng lặp bên trong được thực hiện hoặc một số đơn vị tự nhiên khác liên quan đến lượng thời gian thực mà thuật toán sẽ sử dụng. Chúng tôi cố gắng giữ ý tưởng về thời gian này tách biệt với "thời gian" ( thời gian theo ý nghĩa thực tế ), vì nhiều yếu tố không liên quan đến bản thân thuật toán có thể ảnh hưởng đến thời gian thực (như ngôn ngữ được sử dụng, loại phần cứng máy tính, trình độ của lập trình viên, tối ưu hóa trong trình biên dịch, vv.).  

- Space complexity ( Độ phức tạp không gian) : là một hàm mô tả lượng bộ nhớ (không gian) mà một thuật toán sử dụng về lượng dữ liệu đầu vào cho thuật toán.  Chúng ta thường nói về bộ nhớ "bổ sung" cần thiết, không tính bộ nhớ cần thiết để lưu trữ dữ liệu đầu vào. Một lần nữa, chúng tôi sử dụng các đơn vị tự nhiên (nhưng độ dài cố định) để đo lường điều này. Chúng ta có thể sử dụng byte, nhưng sẽ dễ sử dụng hơn, chẳng hạn như số lượng số nguyên được sử dụng, số lượng cấu trúc có kích thước cố định, v.v. Cuối cùng, hàm mà chúng ta nghĩ ra sẽ độc lập với số byte thực tế cần thiết để biểu diễn đơn vị. Sự phức tạp về không gian đôi khi bị bỏ qua vì không gian được sử dụng là tối thiểu (và / hoặc) hiển nhiên, nhưng đôi khi nó trở thành một vấn đề quan trọng như "thời gian".

**Ví dụ**: Chúng ta thường nói thuật toán này mất `n^2` thời gian chạy với n là độ lớn của dữ liệu đầu vào. Hoặc thuật toán này chiếm không đổi có nghĩa là space complexity = 0(1) ( không tạo thêm không gian mới trong khi thực hiện thuật toán). Ví dụ như các thuật toán in-place order thì độ phức tạp không gian là O(1).


**Đối với cả thời gian và không gian, chúng tôi quan tâm đến độ phức tạp tiệm cận của thuật toán: Khi n (số mục của đầu vào) đi đến vô cùng, điều gì sẽ xảy ra với hiệu suất của thuật toán?**

Ví dụ thuật toán Selection sort:

Giả sử chúng ta muốn sắp xếp 1 mảng theo thứ tự tăng dần. Một thuật toán đơn giản đó chính là Selection Sort. Chúng ta sẽ chạy từ chỉ số đầu tiên đến cuối cùng của mảng 0 -> n - 1. Sau đó chúng ta sẽ swap giá trị của index i với phần từ nhỏ nhất từ i -> n.

```
index	0	1	2	3	4	5	6	comments
---------------------------------------------------------	--------
    |	4	3	9	6	1	7	0	initial
i=0 |	0	3	9	6	1	7	4	swap 0,4
i=1 |	0	1	9	6	3	7	4	swap 1,3
i=2 |	0	1	3	6	9	7	4	swap 3, 9
i=3 |	0	1	3	4	9	7	6	swap 6, 4
i=4 |	0	1	3	4	6	7	9	swap 9, 6
i=5 |	0	1	3	4	6	7	9	(done)
```

```C
 Đây là thuật toán selection sort đc viết bằng C
int find_min_index (float [], int, int);
void swap (float [], int, int);

/* selection sort on array v of n floats */

void selection_sort (float v[], int n) {
	int	i;

	/*  duyệt từ 0 đên n-1 và swap giá trị tại i với giá trị nhỏ nhất từ i + 1 -> n - 1
	 */
	for (i=0; i<n-1; i++) 
		swap (v, i, find_min_index (v, i, n));
}

/* find the index of the minimum element of float array v from
 * indices start to end
 */
int find_min_index (float v[], int start, int end) {
	int	i, mini;

	mini = start;
	for (i=start+1; i<end; i++) 
		if (v[i] < v[mini]) mini = i;
	return mini;
}

/* swap i'th with j'th elements of float array v */
void swap (float v[], int i, int j) {
	float	t;

	t = v[i];
	v[i] = v[j];
	v[j] = t;
}

```

Bây giờ chúng ta muốn định lượng hiệu suất của thuật toán, tức là lượng thời gian và không gian được thực hiện theo n. Chúng tôi chủ yếu quan tâm đến việc các yêu cầu về thời gian và không gian thay đổi như thế nào khi n lớn lên; Việc sắp xếp 10 mục là điều tầm thường đối với hầu hết mọi thuật toán hợp lý mà bạn có thể nghĩ ra, nhưng 1.000, 10.000, 1.000.000 hoặc nhiều  hơn nữa thì sao?

Đối với ví dụ này, lượng không gian cần thiết bị chi phối rõ ràng bởi bộ nhớ mà mảng sử dụng(input đầu vào), vì vậy chúng ta không phải lo lắng về điều đó; nếu chúng ta có thể lưu trữ mảng, chúng ta có thể sắp xếp nó. 

Vì vậy, chúng tôi chủ yếu quan tâm đến thời gian mà thuật toán thực hiện. Một cách tiếp cận là đếm số lượng truy cập mảng được thực hiện trong quá trình thực thi thuật toán; vì mỗi truy cập mảng mất một khoảng thời gian nhất định (s) liên quan đến phần cứng, số lượng này tỷ lệ với thời gian mà thuật toán thực hiện. Chúng ta gọi hàm T(n) chính là hàm liên quan đến thời gian thuật toán thực hiện.

T (n) là tổng số lần truy cập được thực hiện từ đầu **select_sort** cho đến khi kết thúc. **select_sort** chính nó chỉ gọi swap và **find_min_index** khi tôi đi từ 0 đến n-1, vì vậy

Bỏ qua các tính toán phức tạp thì ta thấy thuật toán trên sẽ chạy hết tất cả `T(n) = n2 + 3n - 4 .` lần để thực hiện xong phép tính toán. 

Ta gọi T-M(n) là độ phức tạp của thuật toán `merge sort` thì chúng ta có thể có bảng so sánh độ phức tạp của 2 thuật toán trong trường hợp n tiến đến vô cực.

```
 n		T(n)			Tm(n)
---		----			-----
100     	10,296    		3,684
1,000    	1,002,996  		55,262
10,000   	100,029,996       	736,827
100,000  	10,000,299,996     	9,210,340
1,000,000 	1,000,002,999,996   	110,524,084
10,000,000      100,000,029,999,996 	1,289,447,652
```

Rõ ràng ta thấy với n tăng lên thì thuật toán selection sort này tỏ ra thiếu hiệu quả và thời gian chạy của nó gấp nhiều lần so với thuật toán `merge sort`. 

### Tiệm cận

Tôi đã bỏ qua cách tính toán để làm sao tính ra được T(n) = n^2 + 3n - 4 . Tuy nhiên chúng ta nhận thấy là việc tính toán đến một giá trị chính xác tuyệt đối này là không thực sự cần thiết. Bởi với n tiến đến vô cực or cực lớn thì giá trị 3n sẽ là rất nhỏ so với n^2 và giá trị đó có thể bỏ qua.  Từ đó sinh ra khái niệm gọi là `tiệm cận`. Độ phức tạp của thuật toán được định nghĩa theo giá trị tiệm cận này. 
 Trong trường hợp này thì tiệm cận của `n^2 + 3n -4 = O(n^2)` . Được gọi là `Big O`

Big O cung cấp cho chúng ta một cách chính thức để biểu thị các giới hạn trên của tiệm cận, một cách giới hạn từ phía trên sự tăng trưởng của một hàm. Việc biết vị trí của một hàm trong phân cấp big-O cho phép chúng tôi so sánh nó nhanh chóng với các hàm khác và cho chúng tôi ý tưởng về thuật toán nào có hiệu suất thời gian tốt nhất.  Chúng ta sẽ cùng đi tìm hiểu qua các ví dụ sau.

### Thuộc tính của Big O
Định nghĩa của bigO cũng không thực sự tốt khi làm việc với tất cả thời gian cũng giống như định nghĩa giới hạn của đạo hàm vậy. Dưới đây là một số định lý , tuy tắc hữu ích mà bạn có thể sử dụng để đơn giản hóa các phép tính  Big O:

 **Quy tắc bỏ hằng số:**
	* VD: bạn tính ra TM của một function là **2n + 3n² + 10000**thì bỏ hết những hằng số (mấy số nằm dưới): **2, 3, 10000** → và nó trở thành **n + n²**
	Ủa sao kì vậy? Mấy số đó cũng ảnh hưởng tới tốc độ thực thi function mà?
	*  → Đơn giản là vì nó không đáng kể. Bạn xin vợ 50k (n) đi nhậu thì bạn thích vợ cho 2 * 50k hay 500k? → giá trị n lớn thì có giá trị hơn là hằng số → vứt
* **Quy tắc lấy Max:**
	* Cũng VD trên sau khi đã ra **n + n²**bạn tiếp tục lấy Max của phép toán → nó thành **n²**
* **Quy tắc cộng:**
	* Thuật toán gồm 2 phép tính có độ phức tạp là   **n²** và **m³** → cộng lại đc **n² + m³**
* **Quy tắc nhân:**
        * Tương tự giống quy tắc nhân thì quy tắc cộng cũng như nhau. = m *n 

###  Big Omega và Big Theta

Tương tự như Big O chúng ta thường nghe chúng ta cũng đã từng nghe qua Big Omega (Ω) và Big Theta(Θ) và chúng ta nghĩ liệu nó có liên quan gì với nhau không. 
 **Big Omega (Ω)** thực ra chính là độ phức tạp của thuật toán trong trường hợp tốt nhất. Ví dụ như trong thuật toán Quick Sort thì độ phức tạp trong trường hợp tốt nhất là khi ta chọn được phần tử có độ lớn nằm giữa.
**Big Theta (Θ)** : Bao gồm cả trường hợp tệ nhất và xịn nhất

Bảng tham khảo độ phức tạp của một số thuật toán

![1*sUPzq3cBixVl7lTrl11lXQ](https://user-images.githubusercontent.com/14192303/114276975-0e2a6a80-9a64-11eb-8e76-e5da06460b4c.jpeg)
