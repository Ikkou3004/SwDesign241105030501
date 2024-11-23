## Thiết kế các ca sử dụng của hệ thống Payroll
I. Login
  * Tác nhân: Any User
  * Mô tả: Người dùng đăng nhập vào hệ thống để có thể sử dụng các chức năng của hệ thống
  * Các bước thực hiện:
    - Người dùng nhập username và password.
    - Người dùng ấn nút Đăng nhập.
    - Người dùng đăng nhập thành công.
  * Điều kiện trước:
    - Người dùng phải truy cập vào hệ thống
    - Người dùng đã có tài khoản
  * Điều kiện sau:
    - Người dùng có thể sử dụng các chức năng của hệ thống cho phép
  * Ngoại lệ:
    - Người dùng nhập sai username hoặc password: hệ thống thông báo "Sai tài khoản"

![This is a class diagram]()

II. Maintain Timecard
  * Tác nhân: Employee
  * Mô tả: Nhân viên cập nhật thời gian làm việc của họ vào thẻ chấm công. Hệ thống sẽ kiểm tra thông tin thẻ chấm công hiện tại, lấy mã dự án (charge codes) từ cơ sở dữ liệu quản lý dự án, và lưu lại thẻ chấm công sau khi cập nhật.
  * Các bước thực hiện:
    - Nhân viên chọn chức năng Maintain Timecard để mở thẻ chấm công hiện tại.
    - Hệ thống hiển thị giao diện TimecardForm với thông tin thẻ chấm công hiện tại của nhân viên.
    - Hệ thống lấy thẻ chấm công hiện tại (get current timecard) từ cơ sở dữ liệu.
    - Hệ thống lấy mã dự án (charge codes) từ cơ sở dữ liệu Project Management Database thông qua TimecardController.
    - Hệ thống liên lạc với cơ sở dữ liệu quản lý dự án (Project Management Database) để lấy danh sách mã dự án.
    - Nhân viên nhập giờ làm việc của họ cho các mã dự án tương ứng.
    - Hệ thống cập nhật thông tin vào thẻ chấm công (update timecard).
    - TimecardController cập nhật thông tin mới vào đối tượng Timecard.
    - Nhân viên lưu lại thẻ chấm công (save timecard).
    - TimecardController lưu thông tin thẻ chấm công mới vào cơ sở dữ liệu.
 * Điều kiện trước:
    - Nhân viên đã đăng nhập vào hệ thống.
    - Nhân viên có quyền truy cập vào chức năng Maintain Timecard.
    - Thẻ chấm công hiện tại của nhân viên đã có trong hệ thống và sẵn sàng để cập nhật.
 * Điều kiện sau:
    - Thông tin thời gian làm việc của nhân viên đã được cập nhật và lưu vào cơ sở dữ liệu.
    - Bộ phận quản lý dự án có thể xem thông tin cập nhật mới nhất của thẻ chấm công nếu cần.
 * Các trường hợp ngoại lệ:
   - Dữ liệu thẻ chấm công không hợp lệ: Nếu nhân viên nhập sai mã dự án hoặc dữ liệu giờ làm không hợp lệ, hệ thống sẽ hiển thị thông báo lỗi và yêu cầu sửa lại.
   - Lỗi kết nối với cơ sở dữ liệu: Nếu hệ thống không thể lấy mã dự án từ cơ sở dữ liệu quản lý dự án, hệ thống sẽ thông báo lỗi kết nối và yêu cầu nhân viên thử lại sau.
   - Lỗi khi lưu thẻ chấm công: Nếu quá trình lưu thẻ chấm công thất bại, hệ thống sẽ thông báo lỗi và không cập nhật dữ liệu mới.

![This is a class diagram]()

