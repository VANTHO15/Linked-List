# Linked-List
- Khi phát triển ứng dụng, nhất là các ứng dụng trên vi điều khiển, ngoài phần code cấu hình ngoại vi (Peripheral), lập trình viên cần nắm về cấu trúc dữ liệu, các cấu trúc liên quan đến container (Vector, Linked List, cấu trúc cây,...) đặt biệt là Linked List. Để ứng dụng Linked List vào ứng dụng thực tế, các bạn cần thao tác rất nhuần nhuyễn, tự mình code Linked List, không dùng thư viện chuẩn của C, do nhiều MCU bộ nhớ bị giới hạn, khi đó sẽ không sử dụng được thư viện chuẩn C Standard Library.
- Linked List được sử dụng để hiện thực thao tác bộ nhớ động heap, các hàm malloc(), free(), ruột bên trong là các thao tác Linked List, Linked List cũng là xương sống trong các hệ điều hành thời gian thực RTOS. Tóm lại, nắm được Linked List, ứng dụng của bạn sẽ rất linh hoạt.
- Danh sách liên kết (Linked List) là một cấu trúc dữ liệu dạng danh sách, mảng (Array) cũng là một cấu trúc dữ liệu dạng danh sách. Để truy cập các phần tử trong Array, chúng ta sẽ thông qua index (chỉ mục) đến vị trí của phần tử trong mảng, và phải duyệt mảng. Kích thước của Array thường được chốt cố định, không thay đổi trong quá trình chạy của chương trình, nếu ứng dụng mà dùng được C++ các bạn nên sử dụng Vector thay cho Array, sẽ linh hoạt hơn nhiều.

![image](https://github.com/user-attachments/assets/179746ad-c179-413d-a467-bbf3e17a7a02)
- Khác với Array, Linked list cho phép tổ chức danh sách này ở dạng động, tức là không biết trước số lượng phần tử cần thêm vào danh sách. Việc truy cập đến phần tử trong Linked list sẽ được truy cập thông qua head (vị trí đầu danh sách) hoặc tail (vị trí cuối danh sách).
- Các bạn hình dung Linked List giống một sợi dây xích vậy, từng phần tử trong danh sách sẽ móc nối và tạo liên kết với nhau.

![image](https://github.com/user-attachments/assets/fd203697-9627-4e8a-b2de-8510c46b049b)
### Khi mình thêm một phần tử vào danh sách, sợi dây này sẽ dài ra, khi mình lấy một phần tử ra, sợi dây này sẽ ngắn lại. Từng phần tử đều có mối liên hệ liền kề với phần tử ở cạnh nó.
Tùy nhu cầu sử dụng Linked List có thể biến thành Queue, Ring Buffer, Pool memory,.. Linked List có 2 dạng để duyệt list.
- Linked List Đơn (Singly Linked List): List chỉ duyệt từ đầu tới đuôi.
- Linked List Đôi (Doubly Linked List): List có thể duyệt từ đầu đến đuôi và ngược lại từ đuôi đến đầu.


Linked List được cấu thành từ những phần tử (element) và được liên kết (linked) lại với nhau tạo thành một danh sách. Mỗi phần tử trong Linked List gọi là một Node. Mỗi Node được cấu thành từ hai thành phần cơ bản như sau:
- Dữ liệu: là thành phần lưu trữ dữ liệu của Node.
- Con trỏ next: lưu trữ địa chỉ của Node kế tiếp.


Đối với danh sách liên kết đôi (Doubly Linked List) còn có thêm con trỏ prev để lưu trữ địa chỉ của Node trước đó. Trong khuôn khổ bài viết này, mình sẽ trình bày danh sách liên kết đơn (Singly Linked List) nên chỉ cần hai thành phần như trên là đủ.

Ở ví dụ này, mình sẽ viết code mẫu cho xây dựng danh sách liên kết đơn cơ bản với các thành phần như sau:
- Khởi tạo danh sách
- Thêm một phần tử vào danh sách
- Xóa một phần tử khỏi danh sách

### CODE NHÉ !
- Đầu tiên, mình sẽ định nghĩa cấu trúc dữ liệu cho một Node như sau:

![image](https://github.com/user-attachments/assets/22a42897-334c-4068-aa59-6088d9ac0292)
- Trong định nghĩa Node này, data chính là nơi lưu trữ dữ liệu của Node, các bạn có thể thay thế kiểu dữ liệu khác cho data này hoặc thêm các data khác nữa tùy thuộc vào ứng dụng. Con trỏ next của Node để lưu địa chỉ của Node tiếp theo khi khởi tạo danh sách.
- Mình sẽ định nghĩa một danh sách liên kết đơn với head và tail nhằm quản lý việc thêm, xóa phần tử trong danh sách.

![image](https://github.com/user-attachments/assets/efc5fb7e-89db-4ee5-abe2-930552d8066a)
- Trong cấu trúc list_t phía trên, khi được khởi tạo head sẽ trỏ đến đầu danh sách và tail sẽ trỏ đến cuối danh sách. Đối với loại Đơn các bạn không cần tail cũng được nha, không có tail thì Node nào trỏ đến NULL chính là tail. 
- Tiếp theo, mình sẽ tạo các hàm quản lý các phần tử trong danh sách. 
- Để thêm một Node mới vào danh sách, mình cần cấp phát vùng nhớ cho Node này.

![image](https://github.com/user-attachments/assets/752e9300-1b2b-4d29-948b-c4bf21218757)
- Ở ví dụ này mình đang cấp phát bộ nhớ ở dạng động (dynamic). Mỗi lần khởi tạo một Node mới nó sẽ lấy dữ liệu từ vùng nhớ Heap để cấp phát cho Node. Ở bài viết kế tiếp, mình sẽ trình bày cơ chế Pool memory, ta sẽ cấp phát tĩnh một "bể" dữ liệu để thay cho việc lấy bộ nhớ từ vùng Heap này (Một dạng Linked List nằm trong 1 Array :) )
- Để thêm một Node vào danh sách, mình sẽ tạo các hàm như sau:

![image](https://github.com/user-attachments/assets/b99cd259-1517-40fa-88d5-40d48616ff05)

![image](https://github.com/user-attachments/assets/bb4ecacd-c772-43cc-8bcd-02b220167438)
- Hàm xóa một Node khỏi danh sách:
![image](https://github.com/user-attachments/assets/ad0ae2e2-7e93-4305-abca-268831da9eac)
- Như vậy tương đối đã đủ các thành phần cơ bản để quản lý các thao tác trên Linked List. Mình tạo thêm một hàm để in ra các phần tử trong danh sách này để dễ quan sát.
![image](https://github.com/user-attachments/assets/e5007393-331c-419a-9f02-243efa9b70c6)

# Test thử code
![image](https://github.com/user-attachments/assets/29a0154c-c9b5-4cf0-a582-1074865987ff)
- Kết quả
![image](https://github.com/user-attachments/assets/fd38ae9e-b6db-4839-8c9c-add0fb8c27fd)













