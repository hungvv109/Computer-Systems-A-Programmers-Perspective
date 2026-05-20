# Việc hiểu cách hệ thống biên dịch hoạt động là rất hữu ích

- Có 1 số lý do quan trọng khiến dev cần hiểu cần hiểu các cách các **compilation systems** hoạt động:

    - **Tối ưu hóa hiệu năng program**: cần có hiểu biết cơ bản về **machine-level code** và cách compiler chuyển các câu lệnh C khác nhau thành **machine code**.
        - Example:
            - Một câu lệnh ```switch``` có phải lúc nào cũng hiệu quả hơn một chuỗi câu lệnh ```if-else``` không?
            - Chi phí phát sinh khi gọi hàm là bao nhiêu?
            - Một vòng lặp ```while``` có hiệu quả hơn vòng lặp ```for``` không?
            - Việc tham chiếu bằng ```pointer``` có hiệu quả hơn truy cập bằng ```array index``` không?
            - Tại sao một vòng lặp lại chạy nhanh hơn nhiều nếu ta gom tổng vào một biến cục bộ thay vì truyền một đối số bằng ```reference```?
            - Làm thế nào một hàm có thể chạy nhanh hơn chỉ nhờ việc sắp xếp lại dấu ngoặc trong một biểu thức số học?

    - **Hiểu các lỗi xảy ra tại thời điểm liên kết**: 1 số lỗi khó hiểu nhất thường liên quan đến ```linker```, đặc biệt khi đang xây **big program system**.
        - Example:
            - Điều đó có nghĩa là gì khi ```linker``` báo rằng nó không thể xử lý một ```reference```?
            - Sự khác nhau giữa ```static variable``` và ```global variable``` là gì?
            - Điều gì xảy ra nếu bạn định nghĩa hai ```global variables``` có cùng tên trong hai file C khác nhau?
            - Sự khác nhau giữa ```static library``` và ```dynamic library``` là gì?
            - Tại sao thứ tự liệt kê các ***library*** trên ***command line*** lại quan trọng?
            - Và đáng sợ nhất là: tại sao một số lỗi liên quan đến ```linker``` lại không xuất hiện cho đến lúc chương trình chạy?

    - **Tránh các lỗ hổng bảo mật**:
        - Trong nhiều năm, các **buffer overflow vulnerabilities** đã gây ra nhiều lỗ hổng bảo mật trong **network** và **Internet servers**.

        - Những lỗ hổng này tồn tại vì quá ít lập trình viên hiểu được sự cần thiết của việc giới hạn cẩn thận số lượng và kiểu dữ liệu mà họ nhận từ các nguồn không đáng tin cậy.

        - Một bước đầu tiên trong việc học **secure programming** là hiểu hậu quả của cách dữ liệu và thông tin điều khiển được lưu trữ trên **program stack**.

        - Chúng ta sẽ nghiên cứu **stack discipline** và các **buffer overflow vulnerabilities** trong Chương 3 như một phần của quá trình học **assembly language**.

        - Chúng ta cũng sẽ học về các phương pháp mà lập trình viên **compiler**, và **operating system** có thể sử dụng để giảm nguy cơ bị tấn công.