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
Cơ chế cần giải quyết trong hệ thống MVC
- Phân quyền người dùng: Các nhân viên chỉ có quyền truy cập và chỉnh sửa thông tin cá nhân, trong khi Payroll Administrator có quyền thêm, xóa, và cập nhật thông tin nhân viên.
- Xử lý và tính toán lương tự động: Tự động tính toán tiền lương hàng tuần cho nhân viên tính theo giờ và cuối tháng cho nhân viên hưởng lương cứng, xử lý thêm phần tính lương ngoài giờ và hoa hồng từ đơn hàng.
- Quản lý phương thức thanh toán: Cập nhật phương thức thanh toán theo yêu cầu nhân viên (gửi qua bưu điện, chuyển khoản hoặc nhận trực tiếp).
Báo cáo thông tin: Cho phép nhân viên xem các báo cáo cá nhân, bao gồm số giờ làm, tổng tiền lương nhận được, và các chỉ số khác.

# Phân tích ca sử dụng Payment
Các lớp phân tích (Analysis Classes)
- Employee: Chứa thông tin cá nhân và phương thức thanh toán.
- Payment: Đơn vị giao dịch thanh toán chứa chi tiết về số tiền và phương thức thanh toán.
- Payroll: Quản lý chi tiết lương cho từng nhân viên, bao gồm xử lý lương theo thời gian và hoa hồng.
- PaymentController: Điều khiển các thao tác liên quan đến thanh toán, nhận yêu cầu từ người dùng và chuyển đổi lương đã tính toán đến phương thức thanh toán được chọn.

# Phân tích ca sử dụng Maintain Timecard
Các lớp phân tích
- Employee: Chứa thông tin chấm công.
- Timecard: Lớp chứa dữ liệu về số giờ làm của nhân viên, bao gồm thông tin làm thêm giờ.
- TimecardController: Điều khiển các thao tác liên quan đến chấm công, nhận thông tin từ View và lưu trữ vào Model.

# Hợp nhất kết quả phân tích
  Kết quả phân tích từ hai ca sử dụng cho thấy hệ thống cần tập trung vào việc quản lý thời gian làm việc của nhân viên, tính toán lương tự động dựa trên chấm công và đơn hàng, đồng thời hỗ trợ các phương thức thanh toán linh hoạt. Hệ thống cũng cần tích hợp với cơ sở dữ liệu DB2 hiện tại để truy xuất thông tin dự án.
  Bố cục tổng thể:
- Giao diện người dùng (UI) cho phép nhân viên và quản trị viên tương tác với hệ thống.
- Máy chủ ứng dụng xử lý các logic nghiệp vụ phức tạp, bao gồm tính toán lương và báo cáo.
- Máy chủ cơ sở dữ liệu lưu trữ thông tin chấm công, đơn hàng và lương.
- Kết nối với DB2 đảm bảo khả năng tương tác với cơ sở dữ liệu hiện có mà không cần thay thế.
