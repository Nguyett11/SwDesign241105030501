## BÀI TẬP
## 1. Phân tích kiến trúc 
   - Lựa chọn kiến trúc: Kiến trúc phân lớp (Layered Architecture)
   - Lý do lựa chọn:
     + Dễ bảo trì, vì các tầng hoạt động độc lập.
     + Dễ mở rộng khi cần thêm chức năng hoặc thay đổi logic nghiệp vụ.
     + Bảo mật tốt hơn, có thể đặt các cơ chế bảo mật mạnh mẽ ở từng lớp.
   - Ý nghĩa từng thành phần trong kiến trúc:
     + Presentation Layer (Tầng giao diện): Quản lý giao diện người dùng (UI) và các yêu cầu từ người dùng, như nhân viên, quản lý, bộ phận kế toán.
     + Business Logic Layer (Tầng nghiệp vụ): Xử lý các quy trình nghiệp vụ liên quan đến tính toán lương, khấu trừ thuế, và phát hành lương.
     + Data Access Layer (Tầng truy cập dữ liệu): Giao tiếp với cơ sở dữ liệu để lấy và cập nhật thông tin về nhân viên, lương, giờ làm việc, v.v.
     + Database Layer (Tầng cơ sở dữ liệu): Lưu trữ toàn bộ dữ liệu của hệ thống, bao gồm thông tin nhân viên, lịch sử lương và các khoản chi trả.
   - Biểu đồ UML Package cho Hệ thống Payroll:
     ![UML](https://www.planttext.com/api/plantuml/png/T9112i9034NtEKKkC5UGMhliebS8OnX2fpCoIHSYdio5H_8AEeXKQitolmSFyhZT6pKgDayHG4T9MB8oW8b5ne7yI84L7HuYgM8d50fD0AStmQ6mSZ8ooQcdCnV42rmNtiugYLNx7CHl2HqPxRsloX_Qal8t-qqwjziAmSPMrNKIriD7MihmkeRJiRxf2G00__y30000)

## 2. Cơ chế phân tích
###  Danh sách các cơ chế phân tích trong hệ thống Payroll:
###  a. Cơ chế xác thực và phân quyền: 
      Hệ thống Payroll lưu trữ thông tin nhạy cảm, bao gồm thông tin cá nhân và bảng lương của nhân viên. Do đó, cần đảm bảo rằng chỉ những người dùng được ủy quyền (như quản lý, nhân viên phòng nhân sự, và nhân viên kế toán) mới có thể truy cập vào các phần dữ liệu hoặc thực hiện các hành động nhất định.
###  c. Cơ chế tính toán lương
      Hệ thống cần tính toán bảng lương dựa trên các yếu tố như số giờ làm, lương cơ bản, hoa hồng, và các quy định khác (ví dụ làm thêm giờ). Việc tự động hóa giúp tăng độ chính xác và giảm thiểu rủi ro sai sót trong tính toán thủ công.
###  d. Cơ chế thanh toán đa phương thức
      Nhân viên có thể lựa chọn phương thức thanh toán: nhận lương qua thư, lấy tại văn phòng, hoặc chuyển khoản trực tiếp vào tài khoản ngân hàng. Hệ thống cần hỗ trợ việc tích hợp với hệ thống ngân hàng để xử lý thanh toán tự động.
###  e. Cơ chế lập lịch tự động và xử lý hàng loạt
      Đảm bảo hệ thống tự động chạy bảng lương vào thứ Sáu hàng tuần và vào ngày làm việc cuối cùng của tháng mà không cần can thiệp thủ công.
###  g. Cơ chế quản lý dữ liệu nhân viên
     Hệ thống cần quản lý toàn bộ thông tin liên quan đến nhân viên như hợp đồng lao động, giờ làm việc, chế độ phúc lợi và thông tin ngân hàng, thông tin này thay đổi theo thời gian (lương, thăng chức, điều chỉnh hợp đồng). Do đó cần một cơ chế để theo dõi và cập nhật dữ liệu.
###  h. Cơ chế quản lý bảng chấm công
      Nhân viên ghi nhận giờ làm việc hàng tuần vào bảng chấm công, bao gồm thời gian làm và dự án được tính phí.
     Nhân viên hưởng hoa hồng (Commissioned Employee) có thể thêm, cập nhật, hoặc xóa đơn hàng để ghi nhận doanh thu và nhận hoa hồng.
###  l. Quản lý đơn hàng
      Nhân viên hưởng hoa hồng (Commissioned Employee) có thể thêm, cập nhật, hoặc xóa đơn hàng để ghi nhận doanh thu và nhận hoa hồng.
Hệ thống kiểm tra quyền truy cập và trạng thái của đơn hàng trước khi cho phép cập nhật hoặc xóa.
###  m. Quản lý báo cáo
      Payroll Administrator có thể tạo báo cáo "Total Hours Worked" hoặc "Pay Year-to-Date" dựa trên các tiêu chí đầu vào (loại báo cáo, ngày bắt đầu và kết thúc, tên nhân viên). Báo cáo có thể được lưu với tên và vị trí do Payroll Administrator chỉ định hoặc sẽ bị hủy nếu không lưu.
      
##  3. Phân tích ca sử dụng Select Payment
### a. Các lớp phân tích cho ca sử dụng Selected Payment
    -  Lớp Boundary: PaymentForm
    -  Lớp Controller: SelectPaymentController
    -  Lớp Entities: Employee và Payment
### b. Biểu Sequence của ca sử dụng Select Payment
![Sequence](https://www.planttext.com/api/plantuml/png/T9112i9034NtEKKkC5UGMhliebS8OnX2fpCoIHSYdio5H_8AEeXKQitolmSFyhZT6pKgDayHG4T9MB8oW8b5ne7yI84L7HuYgM8d50fD0AStmQ6mSZ8ooQcdCnV42rmNtiugYLNx7CHl2HqPxRsloX_Qal8t-qqwjziAmSPMrNKIriD7MihmkeRJiRxf2G00__y30000)
### c. Nhiệm vụ của từng lớp phân tích:
      - PaymentForm: Đây là lớp Boundary (biên) vì nó đóng vai trò là lớp giao tiếp giữa hệ thống và nhân viên (Employee). Lớp này hiển thị thông tin đến người dùng và nhận dữ liệu đầu vào từ họ.
      - SelectPaymentController: Đây là lớp Controller (điều khiển), có trách nhiệm xử lý logic của quy trình chọn phương thức thanh toán. Lớp này điều phối các yêu cầu và phản hồi giữa các lớp Boundary và Entity, đảm bảo rằng thông tin chọn phương thức thanh toán được xử lý đúng cách.
      - Employee chứa thông tin cơ bản của nhân viên như mã nhân viên, tên, và phương thức thanh toán.
      - PaymentMethod lưu trữ các chi tiết về phương thức thanh toán (loại thanh toán, địa chỉ hoặc thông tin tài khoản ngân hàng).
### d. Một số thuộc tính và phương thức của các lớp phân tích:
      - PaymentForm: không có thuộc tính, tập trung vào các phương thức hiển thị yêu cầu nhập thông tin và trả lời thông báo cho nhân viên.
      - SelectPaymentController: 
        + selectMethod(): Lấy thông tin phương thức thanh toán mà nhân viên lựa chọn.
        + validateInfo(): Kiểm tra tính hợp lệ của dữ liệu đầu vào (địa chỉ, tài khoản ngân hàng, v.v.).
      - Employee: 
        + employeeId: ID duy nhất của nhân viên.
        + name: Tên nhân viên.
        + payment: Tham chiếu đến phương thức thanh toán của nhân viên, kiểu Payment.
      - Payment: 
        + type: Loại phương thức thanh toán ("Pick-up", "Mail", "Direct Deposit").
        + address: Địa chỉ gửi séc, nếu chọn "Mail".
        + bankName: Tên ngân hàng, nếu chọn "Direct Deposit".
        + accountNumber: Số tài khoản, nếu chọn "Direct Deposit".
### e. Mối quan hệ giữa các lớp
      - Employee liên kết với Payment thông qua thuộc tính payment.
      - PaymentForm kết nối với SelectPaymentController để khởi tạo quy trình chọn phương thức thanh toán và nhận các kết quả từ lớp này.
      - SelectPaymentController tương tác với Payment để cập nhật hoặc lấy thông tin phương thức thanh toán đã chọn.
### f. Biểu đồ lớp mô tả lớp phân tích
![class](https://www.planttext.com/api/plantuml/png/DCwn3OGm30NGtbDu0NO00jH8J9035qXEZ8mfCjiLDzAj01PGVUdvVyd_xw_UBQeTYG4-SkGbQi4nbaJP1j64SSS6PiccmZWHqspFETp8f5vguQBL2lPfOob4Zk75P-BM0JHOLTUWzGXuPuS0DUN5Fpa1003__mC0)
## 4. Phân tích ca sử dụng Maintain Timecard

## 5. Hợp nhất kết quả phân tích
