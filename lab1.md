# Phan Tich Kien Truc
Đề xuất kiến trúc cho bài toán là Client Server
Hệ thống sẽ bao gồm các thành phần sau:
- Client (Windows-based desktop): Giao diện người dùng cho phép các nhân viên nhập thông tin và truy xuất dữ liệu liên quan đến bảng chấm công, đơn hàng và báo cáo.
- Application Server: Xử lý logic nghiệp vụ liên quan đến việc tính toán lương, quản lý nhân viên và kết nối với cơ sở dữ liệu.
- Database Server: Lưu trữ thông tin về nhân viên, chấm công, đơn hàng, và tích hợp với cơ sở dữ liệu quản lý dự án hiện có (DB2 trên IBM mainframe).

# Co Che Phan Tich
Một số cơ chế cần giải quyết trong bài toán:
- Xác thực và phân quyền: Nhân viên chỉ có thể truy cập và chỉnh sửa dữ liệu cá nhân. Payroll Admin có quyền thay đổi thông tin của tất cả nhân viên.
- Tính toán lương: Cơ chế xử lý tự động tính toán lương theo thời gian, loại hình nhân viên (giờ công, lương cứng, hoa hồng), và ngày thanh toán.
- Báo cáo cho nhân viên: Hệ thống phải hỗ trợ các báo cáo tự động về giờ công, đơn hàng, và lương đã nhận.
- Tích hợp với DB2: Hệ thống phải kết nối an toàn và chỉ truy xuất dữ liệu từ cơ sở dữ liệu DB2 hiện có.

# Phân tích ca sử dụng Payment
Các lớp phân tích:
- Employee: Lớp chứa thông tin cơ bản của nhân viên (ID, tên, loại nhân viên, phương thức thanh toán).
- Timecard: Lớp đại diện cho chấm công của nhân viên.
- Payment: Lớp đại diện cho giao dịch thanh toán, chứa thông tin về số tiền và phương thức thanh toán.
- PayrollAdministrator: Lớp đại diện cho người quản lý hệ thống payroll, có quyền thêm, xóa, và chỉnh sửa thông tin nhân viên.
