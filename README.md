Linux System Programming
==================

## 1. Mục Tiêu

- Nắm các chủ đề cơ bản của Linux System Programming. (Network, Thread, Memory Management, etc.)
- Nẵm được cơ bản cách hoạt động của các system call trong Linux.

## 2. Kiến thức về Linux System

### 2.1 File và File System

- Linux tuân theo một triết lý đó là: `everything-is-a-file`.

**Yêu cầu**
- Hãy nêu rõ triết lý này bằng cách tìm hiểu ngóc nghách của `file descriptor` trong kernel.
- Tìm hiểu và nêu rõ hai khái niệm `Regular files` và `Special files`.

### 2.2 Process & Thread

**Yêu cầu:**
- Tìm hiểu về Multi-Threading, các vấn đề gặp phải trong multi-threading.
- Làm rõ khái niệm `race condition`, `deadlock`, cách ngăn chặn race condition, deadlock.

### 2.3 Synchronization

**Yêu cầu:**
- Tìm hiểu khái niệm `Semaphore`, so sánh Semaphore với Mutex.
- Tìm hiểu thêm về `Reader Writer Problem`.

### 2.4 Networking

**Yêu cầu**
- Biết sử dụng socket TCP, UDP
- Phân biệt được Nonblocking I/O và Blocking I/O.

## 3. Phần thực hành

### 3.1. Trò chơi xếp bi 

**Mục tiêu**

- Biết cách xây dựng TCP Client, TCP Server
- Vận dụng các kiến thức về Linux System ở trên để giải quyết bài toán, cụ thể là về Networking, Thread, Synchronization,...
- Biết cách sử dụng các công cụ debug trong quá trình code.

**Mô tả**

- Vào mùa thu năm 2019, Bill và đồng bọn đã nghĩ ra một trò chơi hết sức kinh dị như sau: Cả bọn xây dựng một cửa hàng cung cấp bi với số lượng và chất lượng (kích thước) có giới hạn. Sau khi xây dựng xong cửa hàng, cả bọn tập trung tại một điểm và chạy đến cửa hàng để lấy ngẫu nhiên một bi về `tổ ` của từng thằng, sau đó sắp xếp theo kích thước tăng dần của các bi. Một thời gian sau, cửa hàng hết bi và cả bọn tìm ra người chiến thắng bằng cách gửi số liệu bi về cho bác bán hàng, bác bán hàng tiến hành tính tính toán toán và thông báo kẻ thắng cuộc.

**Yêu cầu**

- Xây dựng một chương trình (console) với hai thành phần Client (Bill và đồng bọn) và server (Cửa hàng và bác bán hàng). Khi Server start nó khởi tạo ngẫu nhiên một mảng các phần tử số nguyên, với kích thước mảng `ngẫu nhiên` trong khoảng từ 100-1000 phần tử. Các Client mở kết nối đến Server và tiến hành lấy một phần tử trong mảng và lưu giữ lại. Sau khi Server thông báo mảng đã hết các phần tử, Client tiến hành gửi số liệu đã lưu lại trong quá trình trên cho Server. Server tính toán và đưa ra bảng xếp hạng, bảng xếp hạng theo số lượng bi lấy được, và chất lượng (tổng kích thước) bi lấy được và gửi cho tất cả Client.

- Xây dựng một TCP Server:
  - Lắng nghe và accept kết nối đến từ nhiều Client.
  - Random kích thước mảng và giá trị các phần tử trong mảng.
  - Xử lý logic như yêu cầu trên
- Xây dựng Client:
  - Connect đến Server
  - Request bi và ghi nhận bi vào file
  - Gửi số liệu bi cho Server

- Hint:
  - Xây dựng server hoạt động theo mô hình Non-Blocking, sử dụng system call `select`, `poll` hoặc `epoll`
  - Main thread có nhiệm vụ handle client connection
  - Xây dựng thread pool để xử lý các task của client gửi đến
  - Tham khảo: https://labs.septeni-technology.jp/technote/event-driven-programming-voi-he-thong-tai-cao/

**Ghi chú**

Dùng ngôn ngữ C hoặc C++ để cài đặt chương trình.

## 4. Tham khảo

- GDB on Linux: 
  - [GDB Tutorial](https://www.tutorialspoint.com/gnu_debugger)
  - [GDB command summary](https://darkdust.net/files/GDB%20Cheat%20Sheet.pdf)
- Nên tìm hiểu về makefile
- Viết được makefile cơ bản để compile một chương trình.

  ```sh
  $ make
  $ make clean
  $ make test
  ```

- Tham khảo:
    - [GCC Make](https://www3.ntu.edu.sg/home/ehchua/programming/cpp/gcc_make.html)
    - [CMake](https://cmake.org/cmake-tutorial/)
