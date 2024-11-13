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

![This is a class diagram](https://www.planttext.com/api/plantuml/png/d5HBJiCm4Dtd51OhM7J1ja9L5x032RK7i5nxI8rYEymuaIh4oLXm9Ax0rFcqRaE5sCJApFZDUsziVtz-BIagZ8sh2bqf8l7WwYhi0CHx8SHCGFyhhH5piOveVPaINZd88mPgHdBWOnQVyKS8XBS6A4g4Ec2KSLV3zGtNjS6QL51ZQAq1QLG4obC45UWezLPX2T8tRWDuKg5QwA7pXB6a5Pgpt4VHorsbH2_sY5mkRGEbzOaQn-zvwRpnvYoMaSn1TF3nr1pnOYkGLT0gsk0dV2l10pBufBh_otx6yCgUFYclIjYFZ0MeZQ9Xx9aCuksFbk9THsvnF5ME09F8wrF3RCVOUBsZ26uuN8W1fGCYPf7xqZ7dM3UWGyjMLTOS394QRGIqAZVWecrRvGsxdhh_mL3cFbwAgzih9h98wsgWg17sXxRejKtMkEGqJIFzFetvS76e7udeB9xgTHcb6zG9p2JdaU9yD9k4zNKJYoKV-VrJyGC00F__0m00)

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
  - `add_purchase_order()`: Thêm một đơn hàng mới vào cơ sở dữ liệu.
  - `update_purchase_order()`: Cập nhật thông tin của một đơn hàng hiện có.
  - `delete_purchase_order()`: Xóa một đơn hàng khỏi cơ sở dữ liệu.
  - `retrieve_purchase_order()`: Truy xuất thông tin đơn hàng dựa trên mã đơn hàng.
5. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý và thông báo lỗi khi có sự cố xảy ra trong quá trình tạo, cập nhật hoặc xóa đơn hàng.
  - Cung cấp thông báo lỗi rõ ràng cho nhân viên để họ có thể xử lý.
* Thuộc tính:
  - `error_code`: Mã lỗi để phân loại các lỗi.
  - `error_message`: Thông báo lỗi chi tiết.
* Phương thức:
  - `generate_error_message()`: Tạo thông báo lỗi chi tiết dựa trên mã lỗi và ngữ cảnh.

![This is a class diagram](https://www.planttext.com/api/plantuml/png/Z5HBRi8m4Dtd51OhMgdGRb65a5fsbLgL0qJ67i2IF-dOGK9LJzP5ZzGhTEA4W4CARFAPUUFClFSolzy_CnyuXjBeJ6ZkFNjonYZlbRCWvwRGRWV0FZF6xXWqhxcIRC8M0PLTnuJb1j88Efr6xkZ2c43W0VAYHB7X7dA74d1uGyYjKp92oa9UWaZGS0RobJMZl3M0rohVp90MdKmYIX-SeOHmDd0HqknIQKtFEPSIWJwG90jqiXIXYhue7nxhr3JcwezLWr7scMunIio7qlVGj0OBMB6mRp8Erw9QadgusGAgrQufv49Gcn6mTAG8jmTo5ZiVmEoLHNIO6mBpTKV9b33A9QmUUaRuAC67VSjsvJgDSQtaoKpxjYh4Xbkf8O-zfBKanagXoQFmvCnBMXF3V4allPgt0YKbqyCaf6xNMuNh3dw5PoyKzRkuSCUUJ0eGA0RRAqfIYLgEvXMpxr0u30HCf1TETdJ_tn8TZoR0ONBGaMkfYTxDCdWOq8dJU4__rqcpBVoufjUFQyPyrbZtNAdXbhgv36sTCc7A1Xg8Vk2-eWvrayQilgR9P_s7jYVSZqQtfqtIgg4rait0och__W400F__0m00)

## Login
Các lớp phân tích
1. Lớp Người Dùng (User)
* Nhiệm vụ:
  - Đại diện cho người dùng muốn đăng nhập vào hệ thống.
  - Cung cấp tên và mật khẩu khi đăng nhập.
* Thuộc tính:
  - `username`: Tên đăng nhập của người dùng.
  - `password`: Mật khẩu của người dùng (có thể được mã hóa khi lưu trữ).
* Phương thức:
  - `enter_credentials()`: Người dùng nhập tên và mật khẩu.
  - `retry_login()`: Cho phép người dùng thử lại sau khi nhập sai thông tin đăng nhập.
  - `cancel_login()`: Hủy bỏ quá trình đăng nhập.
2. Lớp Hệ Thống (System hoặc Authentication System)
* Nhiệm vụ:
  - Quản lý và xử lý quá trình đăng nhập cho người dùng.
  - Kiểm tra thông tin đăng nhập (tên đăng nhập và mật khẩu).
  - Thông báo lỗi khi tên hoặc mật khẩu không hợp lệ.
* Thuộc tính:
  - `login_state`: Trạng thái hiện tại của hệ thống (đang hiển thị màn hình đăng nhập).
  - `error_message`: Thông báo lỗi khi đăng nhập thất bại.
* Phương thức:
  - `validate_credentials(username, password)`: Kiểm tra xem tên đăng nhập và mật khẩu có hợp lệ hay không.
  - `display_error_message()`: Hiển thị thông báo lỗi khi tên đăng nhập hoặc mật khẩu không hợp lệ.
  - `login_user()`: Đăng nhập người dùng vào hệ thống nếu thông tin hợp lệ.
3. Lớp Quản Lý Phiên Đăng Nhập (Session Manager)
* Nhiệm vụ:
  - Quản lý phiên đăng nhập của người dùng khi họ đăng nhập thành công.
  - Lưu trữ và duy trì trạng thái phiên đăng nhập cho người dùng đã đăng nhập.
* Thuộc tính:
  - `session_id`: Mã định danh duy nhất cho mỗi phiên đăng nhập.
  - `user_id`: Mã định danh của người dùng đã đăng nhập.
  - `login_timestamp`: Thời điểm đăng nhập vào hệ thống.
* Phương thức:
  - `create_session(user_id)`: Tạo một phiên đăng nhập mới cho người dùng sau khi xác thực thành công.
  - `terminate_session()`: Kết thúc phiên đăng nhập khi người dùng đăng xuất hoặc khi phiên hết hạn.
4. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý các thông báo lỗi khi người dùng nhập sai thông tin đăng nhập.
  - Cung cấp thông báo lỗi cụ thể để người dùng biết vấn đề xảy ra.
* Thuộc tính:
  - `error_code`: Mã lỗi cụ thể để phân loại lỗi (ví dụ: lỗi "Tên đăng nhập không tồn tại" hoặc "Mật khẩu không chính xác").
  - `error_message`: Thông báo lỗi chi tiết để hiển thị cho người dùng.
* Phương thức:
  - `generate_error_message(error_code)`: Tạo thông báo lỗi dựa trên mã lỗi cụ thể.

![This is a class diagram](https://www.planttext.com/api/plantuml/png/b5DDJyCm3BttLrWxRHARuDe36X8xSc7YN8N6wYBoKINUfWdnopZma_WBE6d7bhOIuh9Qjj_pUtRs_Vcr3YGyxOqkQYr2W9U07juBW2NiERJ289Im9Qziax8jTnsTbrbsoJy0Q0bzLNkK72cXmtp1NGUdP2fx97-gj6kKpGkri3NgOUMZw2Kzx6aN2Mj1ojdjAH2QNcA2L6o11YhHU-ShWo681YUa7eHMab6Psf7Xcx7RAE_LEOt29YAfGgl5gSe6vlOwaP5ymjoM4UpgILZ6dJSVkcIbyYsdYuoI7Jqfdat2j5nyP6CNg-mm6kqvvqEEJ2hVpoXxtJvMl8bEdx5rdXZUA-xirqx-ymuDMlHnNhw_2Rh51SrIqZETtSsOvpvz9nz92Ie-IL5JWAEYNJ7PTKqpE4S99aNXV9A_6GRhAM4dhDJCa3o5OZ3X5tgxMd6OV9MWbNqBGAuercXb_7V-0000__y30000)

## Create Administrative Report
Các lớp phân tích
1. Lớp Quản Trị Viên Tiền Lương (Payroll Administrator)
* Nhiệm vụ:
  - Khởi tạo yêu cầu tạo báo cáo.
  - Cung cấp các thông tin cần thiết để tạo báo cáo, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc và tên nhân viên.
  - Quyết định có lưu báo cáo sau khi tạo xong hay không.
* Thuộc tính:
  - `administrator_id`: Mã định danh duy nhất của Quản Trị Viên Tiền Lương.
  - `name`: Tên của Quản Trị Viên Tiền Lương.
* Phương thức:
  - `request_report()`: Khởi tạo yêu cầu tạo báo cáo với các tiêu chí cần thiết.
  - `save_report()`: Yêu cầu hệ thống lưu báo cáo sau khi đã tạo xong.
  - `discard_report()`: Hủy bỏ báo cáo nếu không cần lưu lại.
2. Lớp Báo Cáo (Report)
* Nhiệm vụ:
  - Đại diện cho báo cáo được tạo dựa trên các tiêu chí của Quản Trị Viên Tiền Lương.
  - Lưu trữ thông tin liên quan đến báo cáo, bao gồm loại báo cáo, ngày bắt đầu, ngày kết thúc, và danh sách nhân viên liên quan.
* Thuộc tính:
  - `report_id`: Mã định danh duy nhất của báo cáo.
  - `report_type`: Loại báo cáo (Tổng số giờ làm việc hoặc Lương từ đầu năm đến nay).
  - `start_date`: Ngày bắt đầu của báo cáo.
  - `end_date`: Ngày kết thúc của báo cáo.
  - `employee_names`: Danh sách tên của các nhân viên trong báo cáo.
* Phương thức:
  - `generate_report()`: Tạo báo cáo dựa trên các tiêu chí do Quản Trị Viên Tiền Lương cung cấp.
  - `display_report()`: Hiển thị báo cáo đã tạo.
  - `save_to_location(location, name)`: Lưu báo cáo tại vị trí và tên file do Quản Trị Viên Tiền Lương chỉ định.
3. Lớp Hệ Thống (System)
* Nhiệm vụ:
  - Xử lý yêu cầu tạo báo cáo từ Quản Trị Viên Tiền Lương.
  - Xác thực các thông tin cần thiết cho báo cáo (loại báo cáo, ngày tháng, danh sách nhân viên).
  - Thông báo lỗi nếu thiếu thông tin hoặc có lỗi trong quá trình tạo báo cáo.
  - Yêu cầu lưu báo cáo nếu Quản Trị Viên Tiền Lương muốn lưu báo cáo.
* Thuộc tính:
  - `login_state`: Trạng thái đăng nhập hiện tại của hệ thống (xác nhận Quản Trị Viên Tiền Lương đã đăng nhập).
  - `error_message`: Thông báo lỗi nếu có sự cố khi tạo báo cáo.
* Phương thức:
  - `request_criteria()`: Yêu cầu Quản Trị Viên Tiền Lương nhập các tiêu chí cần thiết để tạo báo cáo.
  - `validate_criteria()`: Xác thực tiêu chí do Quản Trị Viên Tiền Lương cung cấp.
  - `display_error_message()`: Hiển thị thông báo lỗi nếu có sự cố.
  - `save_report_prompt()`: Hiển thị thông báo yêu cầu lưu báo cáo nếu Quản Trị Viên Tiền Lương muốn lưu.
4. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý các thông báo lỗi khi có thông tin không đầy đủ hoặc không hợp lệ trong quá trình tạo báo cáo.
  - Cung cấp thông báo lỗi chi tiết để Quản Trị Viên Tiền Lương có thể xử lý.
* Thuộc tính:
  - `error_code`: Mã lỗi cụ thể để phân loại các lỗi (ví dụ: thiếu ngày bắt đầu hoặc tên nhân viên không tồn tại).
  - `error_message`: Thông báo lỗi chi tiết để hiển thị cho Quản Trị Viên Tiền Lương.
* Phương thức:
  - `generate_error_message(error_code)`: Tạo thông báo lỗi dựa trên mã lỗi cụ thể.

![This is a class diagram]()

## Maintain Employee Info
Các lớp phân tích
1. Lớp Quản Trị Viên Tiền Lương (Payroll Administrator)
* Nhiệm vụ:
  - Khởi tạo yêu cầu thêm, cập nhật hoặc xóa thông tin nhân viên trong hệ thống.
  - Cung cấp thông tin cần thiết để thêm, sửa, hoặc xóa nhân viên.
  - Xác nhận các thao tác (như xóa nhân viên) khi hệ thống yêu cầu.
* Thuộc tính:
  - `administrator_id`: Mã định danh duy nhất của Quản Trị Viên Tiền Lương.
  - `name`: Tên của Quản Trị Viên Tiền Lương.
* Phương thức:
  - `request_add_employee()`: Khởi tạo yêu cầu thêm mới một nhân viên với thông tin chi tiết.
  - `request_update_employee(employee_id)`: Khởi tạo yêu cầu cập nhật thông tin của một nhân viên cụ thể.
  - `request_delete_employee(employee_id)`: Khởi tạo yêu cầu xóa một nhân viên cụ thể.
  - `confirm_deletion()`: Xác nhận việc xóa nhân viên khỏi hệ thống.
2. Lớp Nhân Viên (Employee)
* Nhiệm vụ:
  - Đại diện cho một nhân viên trong hệ thống, bao gồm các thông tin cần thiết để tính lương và quản lý nhân viên.
  - Lưu trữ và quản lý các thông tin cá nhân, mức lương, và phương thức thanh toán của nhân viên.
* Thuộc tính:
  - `employee_id`: Mã định danh duy nhất của nhân viên.
  - `name`: Tên của nhân viên.
  - `employee_type`: Loại nhân viên (theo giờ, lương cố định, hoặc hoa hồng).
  - `mailing_address`: Địa chỉ liên lạc.
  - `phone_number`: Số điện thoại.
  - `hourly_rate`: Mức lương theo giờ (cho nhân viên làm việc theo giờ).
  - `salary`: Mức lương cố định (cho nhân viên lương cố định và nhân viên hoa hồng).
  - `commission_rate`: Tỷ lệ hoa hồng (cho nhân viên hoa hồng).
  - `hour_limit`: Giới hạn giờ làm việc (nếu có).
  - `pay_delivery_method`: Phương thức nhận lương (mặc định là "nhận trực tiếp").
* Phương thức:
  - `add_employee_info()`: Thêm thông tin nhân viên vào hệ thống.
  - `update_employee_info()`: Cập nhật thông tin nhân viên hiện tại.
  - `delete_employee()`: Xóa nhân viên khỏi hệ thống.
3. Lớp Hệ Thống (System)
* Nhiệm vụ:
  - Xử lý các yêu cầu của Quản Trị Viên Tiền Lương về việc thêm, cập nhật, hoặc xóa nhân viên.
  - Xác thực và lưu trữ thông tin của nhân viên mới vào hệ thống, đồng thời hiển thị các lỗi nếu không tìm thấy nhân viên hoặc thông tin không đầy đủ.
  - Đánh dấu nhân viên cần xóa và xử lý trong chu kỳ trả lương tiếp theo.
* Thuộc tính:
  - `login_state`: Trạng thái đăng nhập hiện tại của hệ thống, đảm bảo Quản Trị Viên Tiền Lương đã đăng nhập.
  - `error_message`: Thông báo lỗi khi có vấn đề trong quá trình xử lý.
* Phương thức:
  - `request_function()`: Yêu cầu Quản Trị Viên Tiền Lương chọn chức năng (thêm, sửa, hoặc xóa nhân viên).
  - `validate_employee_id(employee_id)`: Xác thực mã nhân viên để kiểm tra sự tồn tại trong hệ thống.
  - `display_error_message()`: Hiển thị lỗi nếu có vấn đề (ví dụ: không tìm thấy nhân viên).
  - `finalize_deletion(employee_id)`: Đánh dấu nhân viên cần xóa và lên lịch cho lần thanh toán cuối cùng.
4. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý và hiển thị thông báo lỗi nếu có thông tin không hợp lệ hoặc không tìm thấy nhân viên.
  - Cung cấp các thông tin lỗi chi tiết để Quản Trị Viên Tiền Lương có thể xử lý.
* Thuộc tính:
  - `error_code`: Mã lỗi để xác định vấn đề (ví dụ: mã nhân viên không tồn tại).
  - `error_message`: Thông báo chi tiết về lỗi.
* Phương thức:
  - `generate_error_message(error_code)`: Tạo thông báo lỗi dựa trên mã lỗi cụ thể để hiển thị cho Quản Trị Viên Tiền Lương.

![This is a class diagram]()

## Run Payroll
Các lớp phân tích
1. Lớp Hệ Thống (System)
* Nhiệm vụ:
  - Tự động khởi tạo quy trình chạy bảng lương vào mỗi thứ Sáu và ngày làm việc cuối cùng của tháng.
  - Thu thập thông tin nhân viên, phiếu chấm công và đơn đặt hàng để tính toán tiền lương.
  - Quản lý phương thức thanh toán và xử lý các giao dịch ngân hàng cho nhân viên.
* Thuộc tính:
  - `payroll_date`: Ngày hiện tại mà bảng lương cần được xử lý.
* Phương thức:
  - `initiate_payroll()`: Khởi chạy quy trình bảng lương tự động vào những ngày đã chỉ định.
  - `retrieve_employees_to_pay(payroll_date)`: Lấy danh sách nhân viên đủ điều kiện nhận lương trong ngày.
  - `calculate_pay(employee)`: Tính toán lương cho nhân viên dựa trên phiếu chấm công, đơn hàng, thông tin lương và khấu trừ.
  - `process_payment(employee)`: Xử lý thanh toán cho nhân viên qua các phương thức đã chọn (in phiếu hoặc chuyển khoản).
2. Lớp Nhân Viên (Employee)
* Nhiệm vụ:
  - Đại diện cho một nhân viên trong hệ thống, bao gồm các thông tin cá nhân, phương thức nhận lương, và trạng thái xóa.
  - Cung cấp dữ liệu cần thiết cho quá trình tính lương như bảng chấm công, đơn đặt hàng và mức lương cơ bản.
* Thuộc tính:
  - `employee_id`: Mã định danh duy nhất của nhân viên.
  - `name`: Tên của nhân viên.
  - `salary_info`: Thông tin về mức lương và các khoản lợi ích.
  - `payment_method`: Phương thức nhận lương (trực tiếp qua ngân hàng, nhận qua thư hoặc trực tiếp nhận tại công ty).
  - `is_deleted`: Trạng thái đã được đánh dấu xóa.
* Phương thức:
  - `get_payment_method()`: Lấy phương thức thanh toán đã chỉ định của nhân viên.
  - `mark_for_deletion()`: Đánh dấu nhân viên để xóa sau khi trả lương lần cuối cùng.
3. Lớp Bảng Chấm Công (Timecard)
* Nhiệm vụ:
  - Lưu trữ và cung cấp thông tin về thời gian làm việc của nhân viên, được sử dụng trong tính lương.
* Thuộc tính:
  - `timecard_id`: Mã định danh của bảng chấm công.
  - `employee_id`: Mã định danh nhân viên tương ứng.
  - `hours_worked`: Số giờ làm việc.
  - `date`: Ngày ghi nhận thời gian làm việc.
* Phương thức:
  - `get_hours_worked()`: Lấy số giờ làm việc của nhân viên từ bảng chấm công.
4. Lớp Đơn Đặt Hàng (Purchase Order)
* Nhiệm vụ:
  - Quản lý thông tin đơn đặt hàng của nhân viên hoa hồng, được sử dụng trong quá trình tính lương để xác định hoa hồng.
* Thuộc tính:
  - `purchase_order_id`: Mã định danh của đơn đặt hàng.
  - `employee_id`: Mã định danh của nhân viên hoa hồng.
  - `amount`: Số tiền của đơn đặt hàng.
  -`commission_rate`: Tỷ lệ hoa hồng.
* Phương thức:
  - `get_commission()`: Tính toán hoa hồng dựa trên số tiền đơn đặt hàng và tỷ lệ hoa hồng.
5. Lớp Giao Dịch Ngân Hàng (Bank Transaction)
* Nhiệm vụ:
  - Xử lý và gửi các giao dịch ngân hàng cho nhân viên nhận lương qua hình thức chuyển khoản trực tiếp.
* Thuộc tính:
  - `transaction_id`: Mã định danh của giao dịch.
  - `employee_id`: Mã định danh của nhân viên.
  - `amount`: Số tiền giao dịch.
  - `status`: Trạng thái giao dịch (đang xử lý, đã hoàn thành, thất bại).
* Phương thức:
  - `send_to_bank()`: Gửi giao dịch đến hệ thống ngân hàng.
6. Lớp Báo Cáo Lỗi (Error Reporting)
* Nhiệm vụ:
  - Quản lý và hiển thị thông báo lỗi khi không thể thực hiện giao dịch ngân hàng hoặc các lỗi khác trong quá trình xử lý bảng lương.
* Thuộc tính:
  - `error_code`: Mã lỗi (ví dụ: hệ thống ngân hàng không khả dụng).
  - `error_message`: Thông báo chi tiết về lỗi.
* Phương thức:
  - `generate_error_message(error_code)`: Tạo và hiển thị thông báo lỗi cho Quản Trị Viên.
 
![This is a class diagram]()
