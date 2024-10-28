# Phân Tích Kiến Trúc
Đề xuất kiến trúc MVC
Hệ thống Payroll sẽ tuân theo kiến trúc MVC với ba thành phần chính:
- Model:
  + Đây là nơi xử lý nghiệp vụ và lưu trữ dữ liệu, bao gồm các lớp như Employee, Timecard, PurchaseOrder, Payroll, và Report.
  + Các lớp này chịu trách nhiệm tính toán lương (bao gồm cả phần hoa hồng cho nhân viên được hưởng), xử lý chấm công và lưu trữ các thông tin khác như phương thức thanh toán và dữ liệu báo cáo.
- View:
  + Phần giao diện cho nhân viên và Payroll Administrator, sử dụng giao diện desktop trên nền tảng Windows.
  + Các giao diện sẽ bao gồm các màn hình chính như nhập thông tin chấm công, tạo đơn hàng, cập nhật thông tin cá nhân, và xem báo cáo cá nhân.
- Controller:
  + Controller tiếp nhận các yêu cầu từ người dùng (qua View), thực hiện các thao tác cần thiết lên Model, và sau đó cập nhật View với dữ liệu mới nhất.
  + Các Controller cụ thể sẽ bao gồm: TimecardController, PaymentController, EmployeeController, và ReportController.

# Cơ chế Phân Tích
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

# Phân tích ca sử dụng Maintain Timecard
Các lớp phân tích:
Employee: Chứa thông tin của nhân viên.
Timecard: Lớp chứa các bản ghi chấm công.
PayrollAdministrator: Người quản lý có thể duyệt và chỉnh sửa chấm công.

# Hợp nhất kết quả phân tích
  Kết quả phân tích từ hai ca sử dụng cho thấy hệ thống cần tập trung vào việc quản lý thời gian làm việc của nhân viên, tính toán lương tự động dựa trên chấm công và đơn hàng, đồng thời hỗ trợ các phương thức thanh toán linh hoạt. Hệ thống cũng cần tích hợp với cơ sở dữ liệu DB2 hiện tại để truy xuất thông tin dự án.
  Bố cục tổng thể:
- Giao diện người dùng (UI) cho phép nhân viên và quản trị viên tương tác với hệ thống.
- Máy chủ ứng dụng xử lý các logic nghiệp vụ phức tạp, bao gồm tính toán lương và báo cáo.
- Máy chủ cơ sở dữ liệu lưu trữ thông tin chấm công, đơn hàng và lương.
- Kết nối với DB2 đảm bảo khả năng tương tác với cơ sở dữ liệu hiện có mà không cần thay thế.
