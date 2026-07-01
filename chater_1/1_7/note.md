# The Operating System Manages the Hardware

- **Operating System** là người trung gian giữa **applicaion** và **hardware**.
- Nếu không có operating system, app sẽ làm việc trực tiếp trên hardware có thể xảy ra nguy hiểm như app sẽ chiếm toàn bộ hardware như CPU, RAM, lấy, chèn data, v,v. Như vậy operating system sinh ra để làm cầu nối, thông qua, giao tiếp trung gian giữa app và hardware, và chúng quản lý các hardware.
- Ví dụ như file code muốn print `hello, world!` ra màn hình, nó sẽ gọi operation system, operating system sẽ sử dụng screen in dòng chữ đó ra.
    - `hello, world!` -> operating system -> screen.

## 1.7.1 Processes

- Khi 1 file đang nằm im (chúng ta không sử dụng) như hello.exe, chorme, v,v, thì gọi là **program**.
- Sau khi cta click chúng và run, thì file đó sẽ sinh ra 1 **process**, đây coi là chương trình đang chạy trong computer. giống như "phiên bản sống" của program.

- Khi 1 program đang chạy, operating system sẽ tạo ra **illusion**.
    - ví dụ như khi mở chrome, vscode, youtube, v.v, chúng **tưởng** như **CPU, RAM, .. là của mình**. Nhưng thực tế CPU trong 1 thời điểm siêu nhỏ chạy process này, rồi chuyển qua process khác, liên tục như vậy.
    - 0.001 giây: CPU chạy Chrome
    - 0.001 giây tiếp: CPU chạy VS Code
    - 0.001 giây tiếp: CPU chạy Zalo
    - 0.001 giây tiếp: CPU chạy lại Chrome
    - User cảm giác như các program đang chạy đồng thời -> **concurrent execution**.

- **Concurrent = nhiều process cùng làm việc, nhưng thay phiên nhau**
    - Ví dụ như đầu bếp xào rau, chiên trứng, xào thịt. 1 người làm nhiều việc bằng cách chuyển qua lại giữa các task.

- **Parallel = nhiều process chạy cùng lúc**.
    - 3 đầu bếp cùng nấu món ăn.

- **Context = toàn bộ trạng thái cần thiết để một process có thể tiếp tục chạy đúng chỗ nó đã dừng.**
    - Ví dụ bạn đang đọc sách đến trang 53, dòng thứ 10. Sau đó bạn đi ăn cơm. Muốn quay lại đọc tiếp, bạn cần nhớ:
        - Mình đang đọc sách nào?
        - Đang ở trang mấy?
        - Đang đọc dòng nào?
        - Đang hiểu đến đoạn nào?
    - Đó là **context**.

- **PC = Program Counter** (thanh ghi cho biết CPU đang chạy đến dòng lệnh nào tiếp theo.)

- **Register file** = các thanh ghi CPU đang chứa dữ liệu tạm thời.

- **Context switch** = OS tạm dừng process hiện tại, lưu trạng thái của nó, rồi khôi phục trạng thái của process khác để chạy tiếp.
    ![img](img/image.png)

- **Kernel là phần lõi của Operating System, luôn nằm trong memory, chuyên quản lý hardware và process.**

## 1.7.2 Threads

- Thread là luồng thực thi bên trong process.
- Một process chứa nhiều thread.
- Các thread bên trong process:
    - Dùng chung code, global data, heap, shared libraries.
    - Có riêng: stack, register context, thread ID

- Ưu điểm:
    - nhẹ hơn process
    - chia sẻ dữ liệu dễ hơn
    - tận dụng nhiều CPU/core tốt hơn
    - phù hợp cho server và chương trình concurrent

- Nhược điểm:
    - dễ bị race condition
    - khó debug
    - cần synchronization
    - có thể deadlock

## 1.7.3 Virtual Memory (Bộ nhớ ảo)

- Khi mở app (Chorm, VS Code, terminal, ..), mỗi process sẽ được hệ điều hành cho sử dụng **virtual address space**, process sẽ nghĩ là của riêng nó @@
    - Thực tế, hệ điều hành sẽ map RAM thật với các địa chỉ ảo đó.
- Bố cục:

Địa chỉ cao
┌─────────────────────────┐
│ Kernel virtual memory   │
├─────────────────────────┤
│ User stack              │
│                         │
│        ↓ stack grows    │
├─────────────────────────┤
│ Shared libraries        │
├─────────────────────────┤
│        ↑ heap grows     │
│ Heap                    │
├─────────────────────────┤
│ Program code and data   │
└─────────────────────────┘
Địa chỉ thấp

- **Program code and data**: chứa code. `main()` nằm trong code, biến global nằm ở data.

    - Vùng này thường được tạo ra khi program bắt đầu chạy

- **Heap**: vùng bộ nhớ dùng để cấp phát động khi chương trình đang chạy.

    - Heap có thể lớn lên hoặc nhỏ đi trong lúc chương trình chạy

- **Shared libraries**: vùng chứa code và data của các thư viện dùng chung.
- **Stack**: vùng bộ nhớ dùng cho function calls.
- **Kernel virtual memory**: vùng bộ nhớ dành riêng cho **kernel** — phần lõi của hệ điều hành.
    - Muốn dùng chức năng của kernel, chương trình phải đi qua cơ chế đặc biệt gọi là system call (`read()`, `write()`, `open()`, `fork()`, `execve()`)

- Cần Virtual Memory vì:
    - Mỗi process được cô lập.
        - Process A không thể tùy tiện đọc bộ nhớ của Process B.
        - Chrome không nên đọc được mật khẩu đang nằm trong memory của VS Code hoặc app ngân hàng.

    - Chương trình tưởng có bộ nhớ liên tục.
    - Dùng disk như bộ nhớ phụ.
    
## 1.7.4 Files
![i](img/2.jpg)
![i](img/1.jpg)