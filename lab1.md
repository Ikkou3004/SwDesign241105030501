# Phân Tích Kiến Trúc
Đề xuất kiến trúc MVC
Hệ thống Payroll sẽ tuân theo kiến trúc MVC với ba thành phần chính:
- Model:
  + Đây là nơi xử lý nghiệp vụ và lưu trữ dữ liệu, bao gồm các lớp như Employee, Timecard, PurchaseOrder, Payroll, và Report.
  + Các lớp này chịu trách nhiệm tính toán lương (bao gồm cả phần hoa hồng cho nhân viên được hưởng), xử lý chấm công và lưu trữ các thông tin khác như phương thức thanh toán và dữ liệu báo cáo.
- View:
  + Phần giao diện cho nhân viên và Payroll Administrator, sử dụng giao diện desktop trên nền tảng Windows.
  + Các giao diện sẽ bao gồm các màn hình chính như nhập thông tin chấm công, tạo đơn hàng, cập nhật thông tin cá nhân, và xem báo cáo cá nhân.
- Controller:
  + Controller tiếp nhận các yêu cầu từ người dùng (qua View), thực hiện các thao tác cần thiết lên Model, và sau đó cập nhật View với dữ liệu mới nhất.
  + Các Controller cụ thể sẽ bao gồm: TimecardController, PaymentController, EmployeeController, và ReportController.

# Cơ chế Phân Tích
Cơ chế cần giải quyết trong hệ thống MVC
- Phân quyền người dùng: Các nhân viên chỉ có quyền truy cập và chỉnh sửa thông tin cá nhân, trong khi Payroll Administrator có quyền thêm, xóa, và cập nhật thông tin nhân viên.
- Xử lý và tính toán lương tự động: Tự động tính toán tiền lương hàng tuần cho nhân viên tính theo giờ và cuối tháng cho nhân viên hưởng lương cứng, xử lý thêm phần tính lương ngoài giờ và hoa hồng từ đơn hàng.
- Quản lý phương thức thanh toán: Cập nhật phương thức thanh toán theo yêu cầu nhân viên (gửi qua bưu điện, chuyển khoản hoặc nhận trực tiếp).
Báo cáo thông tin: Cho phép nhân viên xem các báo cáo cá nhân, bao gồm số giờ làm, tổng tiền lương nhận được, và các chỉ số khác.

# Phân tích ca sử dụng Payment
Các lớp phân tích (Analysis Classes)
- Employee: Chứa thông tin cá nhân và phương thức thanh toán.
- Payment: Đơn vị giao dịch thanh toán chứa chi tiết về số tiền và phương thức thanh toán.
- Payroll: Quản lý chi tiết lương cho từng nhân viên, bao gồm xử lý lương theo thời gian và hoa hồng.
- PaymentController: Điều khiển các thao tác liên quan đến thanh toán, nhận yêu cầu từ người dùng và chuyển đổi lương đã tính toán đến phương thức thanh toán được chọn.

![This is a class diagram](https://www.planttext.com/api/plantuml/png/Z5ExJWCn4Epp5Qkh0b8Yqbw18W451H8Y1VNcl5mi_0Zs6kc4-38AFebVm4vy9d90uGhhDBExCpk--_huN7f6nq6hIQVGUxZHMsK78dYRG7ncG1cu5Ir8mnargAc55Jjf-WnjST1a-8vuOqN5eH2ElAzGqYXLmTudsSBzVb1nWDe6moq86zQA_g6MkMlaw36T6O-hSl2_2Zghr8cLr-XfXGhTK5dPsE3yetNF92gcirfBxwKr3pil1oH0XweBAk9HVdfMaJqPSdikhPBu_7gKqvKrdEoJomi0E7e9v7bihlQ9irwj5BdMM9PFmtZjqvnTaHkBeshvD9f50xCPD1Vp-NbJhgk53NguF2vRD2NX5ZGQx2dLZTXVqyO8Scsrwi7m8jZ6m7S59rj-_CGyeah7gML9HgG_uHi00F__0m00)

![This is a class diagram](https://www.planttext.com/api/plantuml/png/T90z3i8m38NtdC9ZAvKBT42LW841YIjOgH6LyaVg33aR0qVY2YGqHQY5yJr_VlvvtX_ToEWvQ2LGilLmq4xPI2HSiWSvE3GCPuoQ3E-iOM-L8h-iPlTNXn1p7coswvWMFDq2ZLmg5HNwsDTYHPU8B5gGg6HGo9ISPLiclkObsDD4leUWji5m0sxI9-AhxJzodyW6qbSuZ7-Mc6zgmLWUBd7MLOceHKUcppzz0G00__y30000)

# Phân tích ca sử dụng Maintain Timecard
Các lớp phân tích
- Employee: Chứa thông tin chấm công.
- Timecard: Lớp chứa dữ liệu về số giờ làm của nhân viên, bao gồm thông tin làm thêm giờ.
- TimecardController: Điều khiển các thao tác liên quan đến chấm công, nhận thông tin từ View và lưu trữ vào Model.

![This is a class diagram](https://www.planttext.com/api/plantuml/png/T90z3i8m38NtdC9ZAvKBT42LW841YIjOgH6LyaVg33aR0qVY2YGqHQY5yJr_VlvvtX_ToEWvQ2LGilLmq4xPI2HSiWSvE3GCPuoQ3E-iOM-L8h-iPlTNXn1p7coswvWMFDq2ZLmg5HNwsDTYHPU8B5gGg6HGo9ISPLiclkObsDD4leUWji5m0sxI9-AhxJzodyW6qbSuZ7-Mc6zgmLWUBd7MLOceHKUcppzz0G00__y30000)

![This is a class diagram](https://www.planttext.com/api/plantuml/png/X91B2i8m48RtESKiA-W5kf22k73XgbuW9bC899cGJ8IUpOL7yWgcfLc8BMx_npUFz_FL9PQHixD2AgO8PnSiZOWY5Dae4wHdk1c7IaPz8i-HhCMuQd-9Lz9eXQWyE1nNC2saV7U6gzFW4h_eFV0YxiHlSSBD4mf1Fl1FVqvkRQ383oQwlc2QhL7rYXOyiHd6FYk5APLyXrvFt_i0003__mC0)

# Hợp nhất kết quả phân tích
Hệ thống Payroll dựa trên kiến trúc MVC sẽ gồm các thành phần và hoạt động chính như sau:
- Model quản lý toàn bộ dữ liệu của hệ thống, đảm bảo tính nhất quán và bảo mật thông tin chấm công và thanh toán.
- View cho phép nhân viên và Payroll Administrator nhập và xem dữ liệu cần thiết, như chấm công và báo cáo cá nhân.
- Controller điều hướng các yêu cầu từ View đến Model, xử lý logic nghiệp vụ như tính lương và tạo báo cáo.

  Kiến trúc MVC giúp hệ thống Payroll dễ mở rộng, bảo trì, và đảm bảo tính tách biệt giữa các thành phần, giúp tối ưu hóa hiệu quả hoạt động và tăng tính linh hoạt khi cần mở rộng chức năng.
