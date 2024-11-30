# Payroll System - Thiết kế hệ thống con

## 1. Hệ thống con: System Clock Interface
- **Mô tả**: Chịu trách nhiệm khởi động quy trình tính lương theo lịch.
- **Chức năng chính**:
  - `lookupString(URL)`: Lấy tham chiếu tới PayrollController để bắt đầu quy trình tính lương.
- **Tương tác**:
  - Gửi tín hiệu khởi chạy `runPayroll()` đến **PayrollController**.

---

## 2. Hệ thống con: PayrollController
- **Mô tả**: Hệ thống trung tâm quản lý các quy trình trong Payroll System.
- **Chức năng chính**:
  - `runPayroll()`: Phương thức chính điều phối toàn bộ quy trình tính lương.
- **Quy trình chính**:
  1. Gọi `getEmployee()` từ **PayrollDBManager** để lấy dữ liệu nhân viên.
  2. Với mỗi nhân viên:
     - Kiểm tra `isPayday()` để xác định có phải ngày trả lương không.
     - Lấy thông tin chấm công (`getTimecardInfo()`) hoặc đơn đặt hàng (`getPOInfo()`).
     - Tính lương qua `calculatePay()`.
     - Tạo phiếu lương qua `addPaycheck()`.
     - Xử lý thanh toán qua **PaymentMethod**:
       - In phiếu lương (`printPaycheck()`).
       - Hoặc gửi tiền trực tiếp vào tài khoản ngân hàng (`deposit()`).
- **Tương tác**:
  - Điều phối các hệ thống con như **PayrollDBManager**, **Employee**, **PaymentMethod**, và **Print Service**.

---

## 3. Hệ thống con: PayrollDBManager
- **Mô tả**: Quản lý dữ liệu nhân viên, chấm công, và đơn đặt hàng.
- **Chức năng chính**:
  - `getEmployee(employeeId)`: Lấy thông tin nhân viên từ cơ sở dữ liệu.
  - `getTimecard(employeeId)`: Lấy dữ liệu chấm công của nhân viên.
  - `getPOInfo(employeeId)`: Lấy thông tin đơn đặt hàng của nhân viên hoa hồng.
- **Tương tác**:
  - Gửi dữ liệu đến **PayrollController** để xử lý.

---

## 4. Hệ thống con: Employee
- **Mô tả**: Đại diện cho nhân viên trong hệ thống, xử lý các phép tính lương cá nhân.
- **Chức năng chính**:
  - `isPayday()`: Xác định hôm nay có phải ngày trả lương không.
  - `calculatePay(timecard, poInfo)`: Tính toán lương dựa trên chấm công hoặc đơn đặt hàng.
  - `addPaycheck(calculatedPay)`: Tạo phiếu lương chứa thông tin lương đã tính toán.
- **Tương tác**:
  - Nhận dữ liệu từ **PayrollDBManager** và trả kết quả về **PayrollController**.

---

## 5. Hệ thống con: PaymentMethod
- **Mô tả**: Quản lý phương thức thanh toán lương cho nhân viên (gửi ngân hàng, in phiếu lương, hoặc gửi thư).
- **Chức năng chính**:
  - `getPaymentMethod()`: Lấy thông tin phương thức thanh toán.
  - `deposit(paycheck, bankInfo)`: Gửi tiền vào tài khoản ngân hàng.
  - `printPaycheck(paycheck)`: In phiếu lương để gửi qua thư hoặc phát trực tiếp.
- **Tương tác**:
  - Nhận phiếu lương từ **PayrollController** và xử lý thanh toán.

---

## 6. Hệ thống con: Timescard
- **Mô tả**: Lưu trữ và cung cấp thông tin chấm công của nhân viên.
- **Chức năng chính**:
  - `getTimecardInfo(employeeId)`: Truy xuất dữ liệu chấm công.
- **Tương tác**:
  - Gửi thông tin chấm công đến **PayrollController** thông qua **PayrollDBManager**.

---

## 7. Hệ thống con: PurchaseOrder
- **Mô tả**: Lưu trữ thông tin đơn đặt hàng, hỗ trợ tính lương cho nhân viên làm việc hoa hồng.
- **Chức năng chính**:
  - `getPOInfo(employeeId)`: Lấy dữ liệu đơn đặt hàng của nhân viên.
- **Tương tác**:
  - Gửi thông tin đến **PayrollController** thông qua **PayrollDBManager**.

---

## 8. Hệ thống con: Bank System
- **Mô tả**: Hệ thống ngân hàng xử lý các giao dịch thanh toán lương.
- **Chức năng chính**:
  - `deposit(paycheck, bankInfo)`: Gửi tiền vào tài khoản ngân hàng của nhân viên.
- **Tương tác**:
  - Nhận thông tin giao dịch từ **PaymentMethod** và xử lý.

---

## 9. Hệ thống con: Print Service
- **Mô tả**: Xử lý việc in phiếu lương cho nhân viên.
- **Chức năng chính**:
  - `print(paycheck)`: In phiếu lương từ dữ liệu được cung cấp.
- **Tương tác**:
  - Nhận dữ liệu phiếu lương từ **PaymentMethod** và thực hiện in.

---
# Payroll System - Thiết kế hệ thống con: Maintain Timecard

## 1. Hệ thống con: Timecard Form
- **Mô tả**: Giao diện người dùng cho phép nhân viên quản lý thông tin chấm công.
- **Chức năng chính**:
  - `open(SecureUser)`: Khởi tạo phiên làm việc an toàn cho nhân viên.
  - `displayTimecard(timecard)`: Hiển thị thông tin chấm công hiện tại.
  - `displayChargeCodes(chargeCodes)`: Hiển thị danh sách mã chi phí.
  - `updateTimecard(timecard)`: Cho phép nhân viên cập nhật thông tin chấm công.
  - `saveTimecard()`: Lưu thông tin chấm công đã thay đổi.
- **Tương tác**:
  - Gửi yêu cầu đến **TimecardController** để thực hiện các thao tác trên dữ liệu.

---

## 2. Hệ thống con: TimecardController
- **Mô tả**: Điều phối toàn bộ quy trình duy trì thông tin chấm công.
- **Chức năng chính**:
  - `getTimecard(employeeId)`: Lấy dữ liệu chấm công của nhân viên từ cơ sở dữ liệu.
  - `saveTimecard(timecard)`: Lưu thông tin chấm công đã được cập nhật.
  - `updateTimecard(timecard)`: Cập nhật nội dung chấm công.
  - `getChargeNumbers()`: Lấy danh sách mã chi phí từ hệ thống quản lý dự án.
- **Tương tác**:
  - Gọi **PayrollDBManager** để truy xuất hoặc lưu dữ liệu chấm công.
  - Kết nối với **Project Management Database** để lấy danh sách mã chi phí.

---

## 3. Hệ thống con: PayrollDBManager
- **Mô tả**: Quản lý thông tin chấm công trong cơ sở dữ liệu của hệ thống Payroll.
- **Chức năng chính**:
  - `getTimecard(employeeId, date)`: Lấy thông tin chấm công theo nhân viên và ngày.
  - `saveTimecard(timecard)`: Lưu thông tin chấm công mới vào cơ sở dữ liệu.
- **Tương tác**:
  - Cung cấp dữ liệu cho **TimecardController**.

---

## 4. Hệ thống con: EmployeeSession
- **Mô tả**: Xác minh và duy trì quyền truy cập của nhân viên.
- **Chức năng chính**:
  - `checkAccess(employeeId)`: Xác nhận rằng nhân viên có quyền truy cập vào thông tin chấm công của họ.
- **Tương tác**:
  - Được gọi bởi **TimecardController** để xác thực quyền truy cập của nhân viên.

---

## 5. Hệ thống con: TimecardAccess - SecurityAccess
- **Mô tả**: Đảm bảo quyền bảo mật và phân quyền cho việc truy cập thông tin chấm công.
- **Chức năng chính**:
  - `setAccess(employeeId, accessLevel)`: Gán quyền truy cập cho nhân viên.
  - `checkAccess(employeeId)`: Kiểm tra quyền truy cập theo nhân viên.
- **Tương tác**:
  - Kết nối với **EmployeeSession** và **TimecardController**.

---

## 6. Hệ thống con: Project Management Database
- **Mô tả**: Hệ thống quản lý dự án cung cấp thông tin mã chi phí liên quan đến các dự án.
- **Chức năng chính**:
  - `getChargeNumbers(projectId)`: Trả về danh sách mã chi phí liên quan đến một dự án cụ thể.
- **Tương tác**:
  - Cung cấp dữ liệu mã chi phí cho **TimecardController**.

---

## 7. Hệ thống con: Timecard
- **Mô tả**: Đại diện dữ liệu chấm công của một nhân viên.
- **Chức năng chính**:
  - `new(date, employeeId)`: Tạo một thông tin chấm công mới.
  - `makeReadable()`: Chuyển đổi dữ liệu để hiển thị dễ dàng.
  - `makeEditable()`: Cho phép chỉnh sửa dữ liệu.
  - `saveChanges(timecard)`: Lưu thay đổi vào cơ sở dữ liệu.
- **Tương tác**:
  - Được tạo và cập nhật thông qua **TimecardController**.

---


