### Reorder Data in Log Files

Đây là một câu hỏi phỏng vấn vị trí Software Engineering của Amazon India. ( Vòng 1 phỏng vấn qua điện thoại của một lập trình viên Ấn Độ)

Bài này đó chính là cho một dãy logs gồm n phần tử là `String` có định dạng như sau. `["dig1 8 1 5 1","let1 art can","dig2 3 6","let2 own kit dig","let3 art zero"]`. Log được chia ra làm 2 loại đó là Letter Log và Digit Logs. 

- Letter Logs là những log mà tất cả các phần tử phía sau là  `lowercase English letters.` (Trừ phần tử key)
- Digit Log là những log mà phần tử phía sau là số . Trừ phần tử đầu tiên
Nhiệm vụ của chúng ta đó chính là sắp xếp letter logs và trả lại một mảng các logs đã được sắp xếp thoả mãn các điều kiện sau

1. Letter Log sẽ được so sánh dựa vào content của chúng ví
- Ví dụ:  "let1 art can" và "let3 art zero" thì ta thấy log thứu 2 sẽ "nhỏ" hơn log đầu vì content của log1 = "art can" < log2 = "art zero". Nếu trong trường hợp content log1 = content log2 thì ta sẽ so sánh đến key đó là let1 với let3. Trường hợp này là let1 < let3
2. Còn digit log thì sẽ chỉ trả lại thứ tự ban đầu của nó không phải sắp xếp gì cả.


### Thuật toán
- Thực ra mình không nghĩ đây là một bài của phỏng vấn amazon vì nó thuộc dạng một câu hỏi sắp xếp một mảng khá là cơ bản. Vấn đề ở đây chỉ là chúng ta lọc ra được 2 mảng con đó là `letter_logs` và  `digit_logs`. Sau đó dùng các giải thuật sắp xếp mà chúng ta để biết để sắp xếp mảng `letter_log ` theo điều kiện ở trên đề bài.
Kết quả trả về đó chính là `return letter_logs + digit_logs` . 

Độ phức tạp của giải thuật này cũng chính là độ phức tạp của thuật toán sắp xếp = O(nLogn)
