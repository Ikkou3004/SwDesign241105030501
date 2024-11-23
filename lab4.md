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

III. Run Payroll
   * Tác nhân:
     - Hệ thống đồng hồ (System Clock)
     - Máy in (Printer)
     - Ngân hàng (Bank System)
   * Mô tả: Ca sử dụng "Run Payroll" thực hiện tính toán và chi trả lương cho nhân viên vào ngày trả lương. Hệ thống sẽ lấy thông tin thẻ chấm công, phương thức thanh toán, thông tin ngân hàng và gửi phiếu lương đến ngân hàng cũng như in phiếu chi lương.
   * Các bước thực hiện:
     - Hệ thống đồng hồ (System Clock) kích hoạt ca sử dụng "Run Payroll" khi đến ngày trả lương.
     - PayrollController bắt đầu quá trình tính lương.
     - PayrollController kiểm tra xem có phải ngày trả lương hay không (is payday?).
     - PayrollController lấy số tiền lương (pay amount) cho từng nhân viên.
     - PayrollController lấy phương thức thanh toán (payment method) của nhân viên.
     - PayrollController lấy thông tin ngân hàng (bank info) của nhân viên.
     - PayrollController tính toán số tiền lương (calculatePay) dựa trên:
     - Thông tin thẻ chấm công (timecard info) từ Timecard
     - Thông tin đơn đặt hàng (PO info) từ PurchaseOrder (nếu có)
     - PayrollController tạo phiếu lương (create paycheck) với số tiền đã tính.
     - PayrollController gửi phiếu lương đến máy in qua PrinterInterface để in phiếu chi lương.
     - PrinterInterface gửi lệnh in phiếu lương (print).
     - PayrollController gửi thông tin giao dịch thanh toán (paycheck, bank info) đến ngân hàng qua BankSystem.
     - BankSystem thực hiện giao dịch thanh toán (send transaction) và gửi phiếu lương vào tài khoản ngân hàng của nhân viên.
   * Điều kiện trước:
     - Hệ thống đồng hồ đã kích hoạt ca sử dụng khi đến ngày trả lương.
     - Các thông tin thẻ chấm công và đơn đặt hàng của nhân viên đã được cập nhật trong hệ thống.
     - Nhân viên đã có phương thức thanh toán và thông tin ngân hàng trong hệ thống.
   * Điều kiện sau:
     - Phiếu lương của nhân viên đã được in và lưu lại.
     - Ngân hàng đã nhận yêu cầu thanh toán lương cho nhân viên và thực hiện giao dịch thành công.
   * Các trường hợp ngoại lệ:
     - Không phải ngày trả lương: Hệ thống dừng lại và không thực hiện tính lương.
     - Lỗi kết nối với máy in: Hệ thống không thể in phiếu lương và ghi nhận lỗi.
     - Lỗi kết nối với ngân hàng: Nếu giao dịch thanh toán thất bại, hệ thống sẽ lưu lại lỗi và gửi thông báo cho bộ phận liên quan.
     - Thiếu thông tin thẻ chấm công hoặc đơn đặt hàng: Hệ thống hiển thị thông báo lỗi và không thể tính toán số tiền lương.

![This is a class diagram]()


