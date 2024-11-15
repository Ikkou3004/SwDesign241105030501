## Subsystem context diagrams
1. BankSystem

![This is a class diagram](https://www.planttext.com/api/plantuml/png/f5DBJiCm4Dtx5BEZI8swhwAeuhFehe8J66TAh3fsP4zG8-1aB3WILy1suk0IYGrPEPutRzwy6NzzVEuSSKjzgzWLtE5HQWH7QD7GqA63ex4WZ2Phr1gazf4Z5xW6rp-vmGFRDN1T0sgID33FSU23nwhRCKUX1UuI0mZ5dGDgE7akIP8JXb-4Rio2pXg1ph4HkEGgoucggk2LWVys6x2zJWIhQ_OULEoJqjZ03TUdnwWMo40zTbbZPvmaQ94QKxEvDzXdyB469F2AUqcYGN7QGZf5Mqp8sSP2U-rBjfoaqPEOWpNduRSGYvr55tpJpz42BgZdwiVOoOCifIpdO33gFCmc_5FWVPpUD9qBOOd3ynENAXlCU5sMu-Ihwc-UKDVBc0jdpMLo0iS3gdXsZUnStAqu6UzEk6JBbIYAwc9aMwYbHK794hzzGQg35ybP3YpVYYApzo8MI5EJYy12zGvr7LxGDm000F__0m00)

* Giải thích:
- PayrollController: Đóng vai trò là lớp điều khiển chính trong hệ thống bảng lương, chịu trách nhiệm khởi tạo quá trình trả lương (chạy payroll()). Nó gửi yêu cầu thực hiện chuyển khoản lương đến ngân hàng thông qua giao diện IBankSystem.

- IBankSystem: Là một giao diện định nghĩa các phương thức cần thiết cho BankSystem, trong trường hợp này là deposit(aPaycheck: Paycheck, intoBank: BankInformation). Giao diện này đảm bảo rằng PayrollController chỉ cần tương tác với giao diện chuẩn thay vì lớp cụ thể của BankSystem.

- BankSystem: Hệ thống con thực tế chịu trách nhiệm xử lý các thao tác chuyển khoản tiền lương. BankSystem triển khai IBankSystem và thực hiện phương thức deposit để chuyển lương vào tài khoản ngân hàng.

- Paycheck: Đại diện cho thực thể phiếu lương, chứa các chi tiết về khoản lương cần chuyển cho nhân viên.

- BankInformation: Lớp lưu trữ thông tin về ngân hàng của nhân viên, cần thiết để thực hiện giao dịch chuyển khoản lương.

