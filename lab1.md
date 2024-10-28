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
![This is a class diagram](https://www.planttext.com/api/plantuml/png/Z5BDJiCm3BxtAQoUDhHEuXgXQMA0n64IOazWjMQhvCIbSGyLuiauy4Yy0kkM6Jfs89T8jh-VVCxNn-SoAhRQUSvAnXZXtZSiFH6yPR0_1GJqv62ZRHssgLHNPuK6Uqz1rwGx6VS0jgIFuKKcKwk_PqdhwGWpAVJI1NNmm8Bw3-gcbP9YJ3I3mgq84uQHH2lC9X6HiUtlIB7cw62DpStfnREZxYAHbyXbnwYqEK0cbCQSHJJzxTJShCJxEiPQmWN834fh9xIndCUoag23TsgJUu0TXeefzP_fjQEe5rL6IOvpiGNdrpaKnVwQpwzosuM3BbA4HVRNXG5oYzM1nu3R4-1G6_EQdFj9T9XUKgY6N_SD003__mC0)

# Phân tích ca sử dụng Maintain Timecard
Các lớp phân tích
- Employee: Chứa thông tin chấm công.
- Timecard: Lớp chứa dữ liệu về số giờ làm của nhân viên, bao gồm thông tin làm thêm giờ.
- TimecardController: Điều khiển các thao tác liên quan đến chấm công, nhận thông tin từ View và lưu trữ vào Model.

# Hợp nhất kết quả phân tích
Hệ thống Payroll dựa trên kiến trúc MVC sẽ gồm các thành phần và hoạt động chính như sau:
- Model quản lý toàn bộ dữ liệu của hệ thống, đảm bảo tính nhất quán và bảo mật thông tin chấm công và thanh toán.
- View cho phép nhân viên và Payroll Administrator nhập và xem dữ liệu cần thiết, như chấm công và báo cáo cá nhân.
- Controller điều hướng các yêu cầu từ View đến Model, xử lý logic nghiệp vụ như tính lương và tạo báo cáo.

  Kiến trúc MVC giúp hệ thống Payroll dễ mở rộng, bảo trì, và đảm bảo tính tách biệt giữa các thành phần, giúp tối ưu hóa hiệu quả hoạt động và tăng tính linh hoạt khi cần mở rộng chức năng.
