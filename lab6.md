# Bank System Class Diagram

## 1. Operations
### a) BankSystem
- `deposit(aPaycheck: Paycheck, intoBank: BankInformation): void`
  - Gửi giao dịch thanh toán đến ngân hàng.

### b) BankTransaction
- `create(op: BankOperation, amount: float, routingNum: String): void`
  - Tạo giao dịch ngân hàng mới.

### c) Paycheck
- `getAmount(): float`
  - Trả về số tiền trên phiếu lương.
- `getEmployee(): Employee`
  - Trả về thông tin nhân viên liên quan đến phiếu lương.

### d) BankInformation
- Lưu trữ thông tin ngân hàng, không có operations.

## 2. States
### a) BankTransaction
- **Pending**: Giao dịch đang chờ xử lý.
- **Completed**: Giao dịch đã hoàn tất.
- **Failed**: Giao dịch thất bại.

### b) Paycheck
- **Issued**: Phiếu lương đã được tạo.
- **Processed**: Phiếu lương đã được gửi tới ngân hàng.

## 3. Attributes
### a) BankSystem
- Không lưu trữ trạng thái, chỉ đóng vai trò như một proxy.

### b) BankTransaction
- `amount: float`
- `transactionOperation: BankOperation` (Loại giao dịch).
- `routingNumber: String` (Số định tuyến ngân hàng).
- `status: String` (Trạng thái giao dịch).

### c) Paycheck
- `amount: float`
- `status: String` (Trạng thái của phiếu lương).

### d) BankInformation
- `name: String`
- `routingNumber: String`

### e) Employee
- `name: String`
- `employeeId: int`

## 4. Relationships and Associations
- **BankSystem** nhận thông tin từ **Paycheck** và **BankInformation** để tạo **BankTransaction**.
- **BankTransaction** sử dụng thông tin từ **BankInformation** để định tuyến giao dịch.
- **Paycheck** liên kết với **Employee** để lấy thông tin người nhận.
