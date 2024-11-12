## Submit Timecard
Các lớp phân tích
- Employee: Đại diện cho nhân viên
  + Thuộc tính: `emloyee`, `name`, `address`, `employeeType`, `paymentMethod`.
  + Nhiệm vụ: Lưu trữ thông tin cơ bản và xác định loại hình công việc cũng như phương thức thanh toán.
- Timecard: Đai diện cho thẻ chấm công.
  + Thuộc tính: `timecardID`, `date`, `hoursWorked` , `chargeNumber`.
  + Nhiệm vụ: ghi nhận và lưu trữ số giờ làm việc của nhân viên.
- PaymentMethod: Đại diện cho phương thức thanh toán
  + Thuộc tính: `methodType` (PostOffice, Banking, At Work).
  + Nhiệm vụ: Cung cấp các phương thức thanh toán khác nhau cho nhân viên.

  ## Maintain Purchase Order
  Các lớp phân tích:
- Employee: Đại diện cho nhân viên.
  + Thuộc tính: `employeeID`, `name`, `address`, `employeeType`, `aymentMethod`.
  + Nhiệm vụ: Lưu trữ thông tin cơ bản của nhân viên và phân quyền cho phép nhân viên quản lý đơn đặt hàng.
- Timecard: Đại diện cho thẻ chấm công.
  + Thuộc tính: `timecardID`, `date`, `hoursWorked`, `chargeNumber`.
  + Nhiệm vụ: Cung cấp thông tin chấm công, đảm bảo rằng thời gian làm việc của nhân viên đủ điều kiện để quản lý đơn đặt hàng (nếu có yêu cầu về số giờ làm việc tối thiểu).
- PaymentMethod: Đại diện cho phương thức thanh toán.
  + Thuộc tính: `methodType` (PostOffice, Banking, At Work).
  + Nhiệm vụ: Xác định phương thức thanh toán của nhân viên nếu có yêu cầu chi trả liên quan đến     việc quản lý đơn đặt hàng.

## Login
Các lớp phân tích
* Employee: Là đối tượng chính thực hiện hành động đăng nhập.
  - Thuộc tính liên quan: `employeeID`, `password`.
  - Nhiệm vụ:
    + Nhập thông tin đăng nhập (tên đăng nhập và mật khẩu).
    + Hệ thống xác thực thông tin.
    + Nếu thông tin đúng, cấp quyền truy cập cho nhân viên vào các chức năng tương ứng với vai trò của họ.
* Timecard: Gián tiếp liên quan đến quá trình đăng nhập.
  - Thuộc tính liên quan: `employeeID`.
  - Nhiệm vụ: Không có nhiệm vụ trực tiếp liên quan đến Use Case Login.
* PaymentMethod: Gián tiếp liên quan đến quá trình đăng nhập.
  - Thuộc tính liên quan: Không liên quan trực tiếp.
  - Nhiệm vụ: Không có nhiệm vụ trực tiếp liên quan đến Use Case Login.

## Create Administrative Report
Các lớp phân tích
* Employee: Là đối tượng được báo cáo trong nhiều loại báo cáo quản trị.
  - Thuộc tính liên quan: `employeeID`, `name`, `department`, `role`, `performance`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động tạo báo cáo.
* Timecard: Cung cấp dữ liệu để tính toán các chỉ số hiệu suất liên quan đến thời gian làm việc.
  - Thuộc tính liên quan: `employeeID`, `date`, `hoursWorked`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động tạo báo cáo.
* PaymentMethod: Có thể được sử dụng để tạo báo cáo về chi phí nhân công và các khoản thanh toán.
  - Thuộc tính liên quan: `paymentMethodID`, `methodType`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động tạo báo cáo.


