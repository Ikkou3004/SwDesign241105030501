## Create Employee Report
Phân tích lớp
1. Nhân Viên (Employee)
* Nhiệm vụ:
- Khởi tạo việc tạo báo cáo bằng cách chỉ định loại báo cáo, khoảng thời gian và các tiêu chí bổ sung.
- Có thể chọn lưu báo cáo hoặc hủy bỏ.
- Nhập thông tin thiếu nếu được hệ thống yêu cầu.
* Thuộc tính:
- `employee_id`: Mã định danh duy nhất của nhân viên.
- `name`: Tên nhân viên.
- `department`: Bộ phận của nhân viên (nếu cần cho các loại báo cáo).
* Phương thức:
- `request_report_type()`: Yêu cầu nhân viên chọn loại báo cáo.
- `provide_dates()`: Cung cấp ngày bắt đầu và kết thúc cho báo cáo.
- `select_charge_number()`: Nếu cần, nhân viên chọn mã công trình (charge number).
- `save_report()`: Lưu báo cáo vào vị trí và tên file đã chỉ định.
- `discard_report()`: Hủy bỏ báo cáo nếu nhân viên không muốn lưu.
2. Lớp Báo Cáo (Report)
* Nhiệm vụ:
- Đại diện cho báo cáo mà nhân viên tạo.
- Lưu trữ dữ liệu về loại báo cáo, khoảng thời gian và các thông tin cụ thể của báo cáo.
* Thuộc tính:
- `report_type`: Loại báo cáo (ví dụ: Tổng số giờ làm việc, Nghỉ phép/ốm, Tổng lương YTD, v.v.).
- `begin_date`: Ngày bắt đầu của báo cáo.
- `end_date`: Ngày kết thúc của báo cáo.
- `charge_number`: (Tùy chọn) Mã công trình nếu báo cáo là "Tổng số giờ làm việc cho một dự án".
- `content`: Dữ liệu hoặc nội dung báo cáo, chẳng hạn như số giờ làm việc, thông tin nghỉ phép, lương, v.v.
- `file_location`: Vị trí lưu báo cáo nếu đã lưu.
* Phương thức:
- `generate_report()`: Tạo báo cáo dựa trên các tiêu chí đầu vào.
- `save_report()`: Lưu báo cáo vào vị trí file đã chỉ định.
- `discard_report()`: Hủy bỏ báo cáo nếu nhân viên không muốn lưu.
3. Lớp Cơ Sở Dữ Liệu Quản Lý Dự Án (Project Management Database)
* Nhiệm vụ:
- Quản lý dữ liệu liên quan đến các dự án, đặc biệt là các mã công trình, khi nhân viên chọn báo cáo "Tổng số giờ làm việc cho một dự án".
* Thuộc tính:
- `charge_numbers`: Danh sách các mã công trình có sẵn liên quan đến các dự án đang thực hiện.
* Phương thức:
- `retrieve_charge_numbers()`: Truy xuất và cung cấp danh sách các mã công trình cho nhân viên khi được yêu cầu.
4. Lớp Hệ Thống (System hoặc Reporting System)
* Nhiệm vụ: 
- Quản lý việc tạo báo cáo, bao gồm việc xử lý lỗi, xác thực đầu vào và cung cấp phản hồi cho nhân viên.
- Nhắc nhở thông tin thiếu hoặc không hợp lệ và hướng dẫn nhân viên qua các bước.
* Thuộc tính:
- `error_message`: Lưu trữ các thông báo lỗi (ví dụ: "Định dạng ngày không hợp lệ" hoặc "Thông tin thiếu").
- `report`: Là một thể hiện của lớp Báo Cáo (Report) đại diện cho báo cáo hiện tại.
Phương thức:

- `validate_report_criteria()`: Kiểm tra và xác nhận rằng nhân viên đã cung cấp đủ thông tin cần thiết.
- `generate_report()`: Quản lý việc tạo báo cáo.
- `handle_error()`: Hiển thị thông báo lỗi và xử lý các thông tin thiếu hoặc không hợp lệ.
- `save_report()`: Lưu báo cáo, tương tác với hệ thống lưu trữ file.

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
