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
* Phương thức:
  - `validate_report_criteria()`: Kiểm tra và xác nhận rằng nhân viên đã cung cấp đủ thông tin cần thiết.
  - `generate_report()`: Quản lý việc tạo báo cáo.
  - `handle_error()`: Hiển thị thông báo lỗi và xử lý các thông tin thiếu hoặc không hợp lệ.
  - `save_report()`: Lưu báo cáo, tương tác với hệ thống lưu trữ file.

![This is a class diagram]()

## Maintain Purchase Order
  Các lớp phân tích:
1. Lớp Nhân Viên Được Hoa Hồng (Commissioned Employee)
* Nhiệm vụ:
  - Khởi tạo việc tạo, cập nhật hoặc xóa đơn hàng mua.
  - Cung cấp các thông tin cần thiết khi tạo hoặc cập nhật đơn hàng.
  - Xác nhận việc xóa đơn hàng nếu cần.
* Thuộc tính:
  - `employee_id`: Mã định danh duy nhất của nhân viên.
  - `name`: Tên nhân viên.
  - `role`: Chức vụ của nhân viên (đảm bảo nhân viên có quyền thực hiện các hành động liên quan đến đơn hàng mua).
* Phương thức:
  - `create_purchase_order()`: Khởi tạo và nhập thông tin cho một đơn hàng mới.
  - `update_purchase_order()`: Chỉnh sửa thông tin của một đơn hàng hiện có.
  - `delete_purchase_order()`: Xóa một đơn hàng đã tồn tại.
2. Lớp Đơn Hàng Mua (Purchase Order)
* Nhiệm vụ
  - Đại diện cho đơn hàng mua được tạo, cập nhật hoặc xóa.
  - Lưu trữ thông tin về đơn hàng, bao gồm các sản phẩm, khách hàng, ngày, và tình trạng của đơn hàng (đang mở hoặc đã đóng).
* Thuộc tính:
  - `purchase_order_id`: Mã định danh duy nhất của đơn hàng mua.
  - `customer_contact`: Thông tin liên hệ của khách hàng.
  - `billing_address`: Địa chỉ thanh toán của khách hàng.
  - `products`: Danh sách các sản phẩm đã mua.
  - `order_date`: Ngày đặt hàng.
  - `status`: Trạng thái của đơn hàng (mở hoặc đóng).
* Phương thức:
  - `generate_order_id()`: Sinh ra một mã đơn hàng mới khi tạo đơn hàng.
  - `update_order()` Xóa đơn hàng khỏi hệ thống.
  - `verify_order_access()`: Xác minh quyền truy cập vào đơn hàng (đảm bảo rằng nhân viên có quyền thay đổi hoặc xóa đơn hàng).
3. Lớp Hệ Thống (System)
* Nhiệm vụ:
  - Quản lý việc tạo, cập nhật và xóa đơn hàng mua.
  - Kiểm tra tính hợp lệ của các thông tin do nhân viên cung cấp và thông báo lỗi khi cần thiết.
  - Hướng dẫn nhân viên qua các bước của quy trình tạo, cập nhật và xóa đơn hàng.
* Thuộc tính:
  - `error_message`: Lưu trữ thông báo lỗi khi có sự cố, chẳng hạn như "Đơn hàng không tồn tại" hoặc "Không có quyền truy cập".
  - `purchase_order`: Đại diện cho đơn hàng được tạo, cập nhật hoặc xóa.
* Phương thức:
  - `request_order_info()`: Yêu cầu nhân viên nhập thông tin cần thiết để tạo, cập nhật hoặc xóa đơn hàng.
  - `validate_order_id()`: Kiểm tra tính hợp lệ của mã đơn hàng (xem có tồn tại hay không).
  - `handle_error()`: Hiển thị thông báo lỗi nếu có sự cố với các bước quy trình (ví dụ: mã đơn hàng không hợp lệ hoặc không phải của nhân viên).
  - `confirm_deletion()`: Xác nhận việc xóa đơn hàng và yêu cầu nhân viên xác nhận lại hành động này.
4. Lớp Cơ Sở Dữ Liệu Đơn Hàng (Purchase Order Database)
* Nhiệm vụ:
  - Lưu trữ và quản lý các đơn hàng mua trong hệ thống.
  - Cung cấp các chức năng để thêm, sửa và xóa các đơn hàng mua.
* Thuộc tính:
  - `purchase_orders`: Danh sách tất cả các đơn hàng mua trong hệ thống.
* Phương thức:
  - add_purchase_order(): Thêm một đơn hàng mới vào cơ sở dữ liệu.
  - update_purchase_order(): Cập nhật thông tin của một đơn hàng hiện có.
  - delete_purchase_order(): Xóa một đơn hàng khỏi cơ sở dữ liệu.
  - retrieve_purchase_order(): Truy xuất thông tin đơn hàng dựa trên mã đơn hàng.
5. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý và thông báo lỗi khi có sự cố xảy ra trong quá trình tạo, cập nhật hoặc xóa đơn hàng.
  - Cung cấp thông báo lỗi rõ ràng cho nhân viên để họ có thể xử lý.
* Thuộc tính:
  - `error_code`: Mã lỗi để phân loại các lỗi.
  - `error_message`: Thông báo lỗi chi tiết.
* Phương thức:
  - `generate_error_message()`: Tạo thông báo lỗi chi tiết dựa trên mã lỗi và ngữ cảnh.

![This is a class diagram]()

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
