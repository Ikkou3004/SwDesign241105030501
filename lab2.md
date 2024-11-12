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
  + Thuộc tính: timecardID, date, hoursWorked, chargeNumber.
  + Nhiệm vụ: Cung cấp thông tin chấm công, đảm bảo rằng thời gian làm việc của nhân viên đủ điều kiện để quản lý đơn đặt hàng (nếu có yêu cầu về số giờ làm việc tối thiểu).
- PaymentMethod: Đại diện cho phương thức thanh toán.
  + Thuộc tính: methodType (PostOffice, Banking, At Work).
  + Nhiệm vụ: Xác định phương thức thanh toán của nhân viên nếu có yêu cầu chi trả liên quan đến     việc quản lý đơn đặt hàng.
