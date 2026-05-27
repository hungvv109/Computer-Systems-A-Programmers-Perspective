# Storage Devices Form a Hierarchy / Các thiết bị lưu trữ tạo thành một hệ phân cấp

- Ý tưởng chính:
    - Mỗi tầng lưu trữ sẽ đóng vai trò **cache** cho tầng tiếp theo.
        - Tầng nhanh hơn sẽ giữ "hot" data (hay dùng).
        - Để tránh phải truy cập tầng chậm hơn.

    ![img](..\1_5\img\image3.png)

- **Ex**:
    - **Register file** là cache cho **L1 cache**:
        - Nếu data không nằm trong register file, CPU sẽ tìm tại L1 cache.
    - **L1 cache** là cache cho **L2 cache**.

