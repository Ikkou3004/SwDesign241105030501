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

![This is a class diagram](https://www.planttext.com/api/plantuml/png/N96nJiGm38RtF8ML4Qa3QwUJW841X7I7c7sDTQrecYfsXmhn48YHYUVem89uZti2Ne5mIjfBCrZwVplEP-Tt-jgme9V1jaeQQGcsFv_m_NQStg4zJXyzLBM3HoQumX2smzus0hl6KeNUA5Mro0mtjc_TI0Gl2i8fWA9nQqfeEebkXvPAOF5DTuWM6kE9UUMcwxknNr_eSRJKoHr9xKBpXtEfNXDG0WHaq4de6K-Ya-CPbF3QTOZHgDtW-SdvPyhggXhzWUu7koT_xYVgSjx70fHndgWoPq6p9vqD7fhC2zQN6ee2z8LUPYoXHbQp_4-7gfbXdSXNjg7EXC__0m00__y30000)

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
  + Nhiệm vụ: Xác định phương thức thanh toán của nhân viên nếu có yêu cầu chi trả liên quan đến việc quản lý đơn đặt hàng.

![This is a class diagram](https://www.planttext.com/api/plantuml/png/P94zJiGm48Lxds9AGCe5KgtGKb0iKAn4FSIZ95h_PCTs4I5EWsYGkC16Q8izIKx05R1Dj2HGUPxcwRtFzjTmN3cFx8DMebBe7DpeJjcU29u504tYTXs5GKtnG2cPd9jjjtsN5XtscepVa6-iZBg02iq63TRq4BXgqD4zI-ABonAkhLM4Hho8gNRXoDqsJRauJslqgQJrf5DtfFPX3l4RjMqrLSWof_X9v23vaz7OmExHyeuIPgpbckw2VYAUySmlavDq7lDTe-lyJ5T5yGU-X7qO3wy6rEbJB5VHUwOhGRMdTmExyN3q_trBW1BSE7o078StKmkn8YFZbtq3003__mC0)

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

![This is a class diagram]()

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

## Maintain Employee Info
Các lớp phân tích
* Employee: Là đối tượng chính được quản lý trong Use Case này.
  - Thuộc tính liên quan: `employeeID`, `name`, `department`, `role`, `contactInfo`, `address`, `emergencyContact`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động cập nhật thông tin.
* Timecard: Gián tiếp liên quan đến việc cập nhật thông tin nhân viên.
  - Thuộc tính liên quan: `employeeID`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động cập nhật thông tin.
* PaymentMethod: Gián tiếp liên quan đến việc cập nhật thông tin nhân viên.
  - Thuộc tính liên quan: `employeeID`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động cập nhật thông tin.

  ## Run Payroll
* Employee: Là đối tượng nhận lương.
  - Thuộc tính liên quan: `employeeID`, `name`, `salary`, `paymentInfo`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động chạy bảng lương.
* Timecard: Cung cấp dữ liệu về thời gian làm việc để tính toán lương.
  - Thuộc tính liên quan: `employeeID`, `date`, `hoursWorked`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động chạy bảng lương.
* PaymentMethod: Xác định phương thức thanh toán lương cho nhân viên.
  - Thuộc tính liên quan: `paymentMethodID`, `methodType`, `bankAccount`.
  - Nhiệm vụ: Không trực tiếp thực hiện hành động chạy bảng lương.
