## Subsystem context diagrams
1. BankSystem

![This is a class diagram](https://www.planttext.com/api/plantuml/png/f5DBJiCm4Dtx5BEZI8swhwAeuhFehe8J66TAh3fsP4zG8-1aB3WILy1suk0IYGrPEPutRzwy6NzzVEuSSKjzgzWLtE5HQWH7QD7GqA63ex4WZ2Phr1gazf4Z5xW6rp-vmGFRDN1T0sgID33FSU23nwhRCKUX1UuI0mZ5dGDgE7akIP8JXb-4Rio2pXg1ph4HkEGgoucggk2LWVys6x2zJWIhQ_OULEoJqjZ03TUdnwWMo40zTbbZPvmaQ94QKxEvDzXdyB469F2AUqcYGN7QGZf5Mqp8sSP2U-rBjfoaqPEOWpNduRSGYvr55tpJpz42BgZdwiVOoOCifIpdO33gFCmc_5FWVPpUD9qBOOd3ynENAXlCU5sMu-Ihwc-UKDVBc0jdpMLo0iS3gdXsZUnStAqu6UzEk6JBbIYAwc9aMwYbHK794hzzGQg35ybP3YpVYYApzo8MI5EJYy12zGvr7LxGDm000F__0m00)

* Giải thích:
  - PayrollController: Đóng vai trò là lớp điều khiển chính trong hệ thống bảng lương, chịu trách nhiệm khởi tạo quá trình trả lương (chạy payroll()). Nó gửi yêu cầu thực hiện chuyển khoản lương đến ngân hàng thông qua giao diện IBankSystem.
  - IBankSystem: Là một giao diện định nghĩa các phương thức cần thiết cho BankSystem, trong trường hợp này là deposit(aPaycheck: Paycheck, intoBank: BankInformation). Giao diện này đảm bảo rằng PayrollController chỉ cần tương tác với giao diện chuẩn thay vì lớp cụ thể của BankSystem.
  - BankSystem: Hệ thống con thực tế chịu trách nhiệm xử lý các thao tác chuyển khoản tiền lương. BankSystem triển khai IBankSystem và thực hiện phương thức deposit để chuyển lương vào tài khoản ngân hàng.
  - Paycheck: Đại diện cho thực thể phiếu lương, chứa các chi tiết về khoản lương cần chuyển cho nhân viên.
  - BankInformation: Lớp lưu trữ thông tin về ngân hàng của nhân viên, cần thiết để thực hiện giao dịch chuyển khoản lương.

2. PrintService

![This is a class diagram](https://www.planttext.com/api/plantuml/png/X99DJiCm48NtFiNiA5AZxgiegWGikelW18CpRInSExAd5H5mCXOSYIlWdxYGTa5MYVtcUpDlyltvjV6CZey7BMxWddRA47WcHvR7WJpih0Df3Jkhbw1CkDcXf2NuuxCVW_2m13GTa675emYC5iUWrNUvHfC3z8K0KgFtm3roO2bMo1G_2GONsE39dPIaP3hWA7kIBoBNN6FhUg8s3Rm92Czg1Niov08rDPMX1RIu5H-nmMqP8jcqKVCq-RA5BaUGIm_4lUt4UMpOpkJP5R9uWUraj8RoDZcsphwErswE1aS-9cVsAGIKV4Jz6sqP_MzHNP-lWs_WdgV_lu-7jAHf2JFt8WpZCohjVqFFntMT5zmqaVD86bbPutir-9HqIYYq7m_5zQggghc8Rdsn70ydXMAkgT-hQZRynNsabWw5s93fub_y0m00__y30000)

* Giải thích:
  - PayrollController: Đây là lớp điều khiển chính trong hệ thống bảng lương. Nó có trách nhiệm khởi tạo quy trình in phiếu lương của nhân viên bằng cách gọi phương thức print() trong giao diện IPrintService.
  - IPrintService: Là giao diện định nghĩa phương thức print(aPaycheck: Paycheck) cần thiết cho PrintService. Giao diện này giúp tách biệt việc triển khai cụ thể của hệ thống con in phiếu lương với các lớp điều khiển, đảm bảo rằng PayrollController chỉ cần gọi phương thức chuẩn mà không quan tâm đến chi tiết thực hiện.
  - PrintService: Là hệ thống con thực tế chịu trách nhiệm in phiếu lương của nhân viên. PrintService triển khai giao diện IPrintService và thực hiện phương thức print để in phiếu lương.
  - Paycheck: Đây là lớp đại diện cho phiếu lương của nhân viên, chứa các thông tin cần thiết để in ra phiếu lương hoàn chỉnh.

3. ProjectManagementDatabase subsystems

![This is a class diagram](https://www.planttext.com/api/plantuml/png/f5FBQiCm4BphA_RM1c9o3y84aXu2RGdzWuszZbLaoKZh4DFsothe9_KNAlb5Gabwg6-sPaUpC-Flpw-LPtJSL5hSmOOAPGWyaoFBRKqU2kiWiuQTrNDG9fmKcD4SVBFtRG1MSq2J0nbMt8h0iSCsOFMwdz7a0Ft809b6xu5BvC2bM267AsfdNodZn94Expdao0YOPUIzw0T-SqevKAOfl0a8ps811N5MZdIGbUWE1AQfzkJy_KnyH7dRSOLkirsFVKA31wh24fjmznuz0Ll8UpSwEOxOAJgYXegujBcOh83jTP9U6OpJjEuaFG-AgAgrROcs-J8wErl2e_8ipq5fBphSS6h_4EoeTkHZ3kOG7ARW83T1xnJKwELL1YadR3Jnr4xU_d-3XwuVG_uNKi_1mN96fSVOBuwax3kMff7l9NP5MUDBLVkkWLqWOUVuKVmkJ9Aajv9Q3eMRsjEbVbGeRWp9zoIvxkUjoQZcV3iXLcJo-1F-0000__y30000)

* Giải thích:
  - PayrollController: Đây là lớp điều khiển chính trong hệ thống bảng lương. Nó có nhiệm vụ khởi tạo quy trình truy xuất các mã công trình (charge numbers) của nhân viên, để phục vụ cho các báo cáo hoặc tính toán lương liên quan đến dự án.

  - IProjectManagementDatabase: Là giao diện định nghĩa phương thức retrieveChargeNumbers(employeeId: int): List<ChargeNumber> để lấy danh sách mã công trình của nhân viên. Giao diện này cho phép PayrollController truy cập dữ liệu dự án mà không cần biết chi tiết của hệ thống con.

  - ProjectManagementDatabase: Là hệ thống con thực tế chứa và quản lý dữ liệu dự án. ProjectManagementDatabase triển khai giao diện IProjectManagementDatabase và thực hiện phương thức retrieveChargeNumbers để trả về danh sách mã công trình.

  - ChargeNumber: Lớp này đại diện cho mã công trình, bao gồm các thông tin chi tiết liên quan đến các dự án mà nhân viên đã tham gia.

## Analysis class to design element map

| Analysis class | Design Element |
| ----------- | ----------- |
| Employee | Employee class trong PayrollDB |
| Payroll Administrator | AdminInterface class và PayrollControllerProcess |
| Timecard | TimecardDBManager |
| Project Management Database | ProjectManagementDBAccess trong External System Interfaces |
| Purchase Order | PurchaseOrder class trong PayrollDBManager |
| Bank System | BankSystemAccess trong External System Interfaces |
| Print Service | PrinterAccess trong External System Interfaces |
| Report Generation | ReportGenerationModule trong PayrollControllerProcess |

