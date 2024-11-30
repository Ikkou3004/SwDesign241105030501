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

## Quy trình hoạt động tổng quan
1. **System Clock Interface** khởi động quy trình bằng cách gọi `runPayroll()` trong **PayrollController**.
2. **PayrollController** lấy dữ liệu nhân viên từ **PayrollDBManager** và:
   - Thu thập dữ liệu chấm công hoặc đơn đặt hàng.
   - Tính toán lương qua **Employee**.
   - Tạo phiếu lương và chuyển tới **PaymentMethod** để xử lý thanh toán.
3. **PaymentMethod** thực hiện thanh toán bằng cách:
   - Gửi thông tin giao dịch đến **Bank System** để gửi ngân hàng.
   - Hoặc chuyển dữ liệu phiếu lương đến **Print Service** để in.
4. Kết quả trả về **PayrollController**, hoàn thành quy trình.
