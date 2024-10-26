## LAB 1
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
     ![UML](https://www.planttext.com/api/plantuml/png/T9112i9034NtEKKkO8yWjNRPHQyGnb12fpCoIHSYdgmBZ-GLT12fr37B_nuyo6EvrsgKR9uyW8uIC4Lb01FpZ3svaGPMtE7HaogsGaEY2U3y9jWdLWv69Z5qTE64U8NRofjP9R1g5mTn9Q4beuDpMVb36rB-Ph_9gjgNGb3OihfDmdRuI6iPNbTpEEKtFG400F__0m00)

## 2. Cơ chế phân tích
###  Danh sách các cơ chế phân tích trong hệ thống Payroll:
###  a. Cơ chế xác thực và phân quyền: 
      Hệ thống Payroll lưu trữ thông tin nhạy cảm, bao gồm thông tin cá nhân và bảng lương của nhân viên. Do đó, cần đảm bảo rằng chỉ những người dùng được ủy quyền (như quản lý, nhân viên phòng nhân sự, và nhân viên kế toán) mới có thể truy cập vào các phần dữ liệu hoặc thực hiện các hành động nhất định.
###  b. Cơ chế tính toán lương
      Hệ thống cần tính toán bảng lương dựa trên các yếu tố như số giờ làm, lương cơ bản, hoa hồng, và các quy định khác (ví dụ làm thêm giờ). Việc tự động hóa giúp tăng độ chính xác và giảm thiểu rủi ro sai sót trong tính toán thủ công.
###  c. Cơ chế thanh toán đa phương thức
      Nhân viên có thể lựa chọn phương thức thanh toán: nhận lương qua thư, lấy tại văn phòng, hoặc chuyển khoản trực tiếp vào tài khoản ngân hàng. Hệ thống cần hỗ trợ việc tích hợp với hệ thống ngân hàng để xử lý thanh toán tự động.
###  d. Cơ chế lập lịch tự động và xử lý hàng loạt
      Đảm bảo hệ thống tự động chạy bảng lương vào thứ Sáu hàng tuần và vào ngày làm việc cuối cùng của tháng mà không cần can thiệp thủ công.
###  e. Cơ chế quản lý dữ liệu nhân viên
     Hệ thống cần quản lý toàn bộ thông tin liên quan đến nhân viên như hợp đồng lao động, giờ làm việc, chế độ phúc lợi và thông tin ngân hàng, thông tin này thay đổi theo thời gian (lương, thăng chức, điều chỉnh hợp đồng). Do đó cần một cơ chế để theo dõi và cập nhật dữ liệu.
###  f. Cơ chế quản lý bảng chấm công
      Nhân viên ghi nhận giờ làm việc hàng tuần vào bảng chấm công, bao gồm thời gian làm và dự án được tính phí.
     Nhân viên hưởng hoa hồng (Commissioned Employee) có thể thêm, cập nhật, hoặc xóa đơn hàng để ghi nhận doanh thu và nhận hoa hồng.
###  g. Quản lý đơn hàng
      Nhân viên hưởng hoa hồng (Commissioned Employee) có thể thêm, cập nhật, hoặc xóa đơn hàng để ghi nhận doanh thu và nhận hoa hồng.
Hệ thống kiểm tra quyền truy cập và trạng thái của đơn hàng trước khi cho phép cập nhật hoặc xóa.
###  h. Quản lý báo cáo
      Payroll Administrator có thể tạo báo cáo "Total Hours Worked" hoặc "Pay Year-to-Date" dựa trên các tiêu chí đầu vào (loại báo cáo, ngày bắt đầu và kết thúc, tên nhân viên). Báo cáo có thể được lưu với tên và vị trí do Payroll Administrator chỉ định hoặc sẽ bị hủy nếu không lưu.
      
##  3. Phân tích ca sử dụng Select Payment
### a. Các lớp phân tích cho ca sử dụng Selected Payment
    -  Lớp Boundary: PaymentForm
    -  Lớp Controller: SelectPaymentController
    -  Lớp Entities: Employee và Payment
### b. Biểu Sequence của ca sử dụng Select Payment
![Sequence](https://www.planttext.com/api/plantuml/png/f5InJiCm4Dtz5QTE8D4VO62Xi21G9Rem1jUgBLmxf4wbp4m8CNH42D62409HYO6f6HYC-0z_0R_0EQGbJTLI88jbd--zTy-N-qXV0sfq15ljKEg4CSAK4IRvtX_gM3M3A85waBGnkAsZDg5QcKXBs6UIKPD7DhyE9Ol687c043A6W-f64GZMOPExz5n1oD-VtmUg1GRt3nING74msWuKAIPW_XnInDh1t6i1RpsNNY3KSPo0YUmJ0j6VMUR18kD4_JeSsCSOg1lTnw2ulL7G5VPHBO4FAvMwe4VLEAoiGMKt4DAlDH4XATHOg3l2L5QdZ9fVQ2DoerkGBhqIq7NffLZ8_DQpjxb2GW9fe5wwF5560By5HkI7_jdSQ1YY1RYO6N9f-oLCmcI7pV9cDYn9clTBuG7yEvy5MMMdq7BfK437Fj0CRtx3xV5C-gBaKiFzfkgielnDfYYeI--ocoUB32drmv-jCRufLSitABTz9EYYk8vBUnZf2pZY6Xj8BUVKBx3-OLofyjn2m-sBloZKD1bEc2OP3uPPvOslj4CxqC0rYlP0VJy72ZhASwNmbnVpnvd-v1C00F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
      - PaymentForm: Đây là lớp Boundary (biên) vì nó đóng vai trò là lớp giao tiếp giữa hệ thống và nhân viên (Employee). Lớp này hiển thị thông tin đến người dùng và nhận dữ liệu đầu vào từ họ.
      - SelectPaymentController: Đây là lớp Controller (điều khiển), có trách nhiệm xử lý logic của quy trình chọn phương thức thanh toán. Lớp này điều phối các yêu cầu và phản hồi giữa các lớp Boundary và Entity, đảm bảo rằng thông tin chọn phương thức thanh toán được xử lý đúng cách.
      - Employee chứa thông tin cơ bản của nhân viên như mã nhân viên, tên, và phương thức thanh toán.
      - Payment lưu trữ các chi tiết về phương thức thanh toán (loại thanh toán, địa chỉ hoặc thông tin tài khoản ngân hàng).
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
![class](https://www.planttext.com/api/plantuml/png/DCwn3OGm30NGtbDu0NO0mbsDn0G1N9pan2TZYin6mKYiG292zQNd_oLVnzbkvjNsm02px77rcd3qAL2qhsX0ls47YqHJOPo8QR5wTWyoQIdraEbd2J_XpvA82heNwwJO0D1Xq-H1Ns90S3MXfRZcJsu0003__mC0)
## 4. Phân tích ca sử dụng Maintain Timecard
### a. Các lớp phân tích cho ca sử dụng Selected Payment
    -  Lớp Boundary: EmployeeUI
    -  Lớp Controller: TimecardController
    -  Lớp Entities: Timecard, Employee
### b. Biểu Sequence của ca sử dụng Select Payment
![sequence](https://www.planttext.com/api/plantuml/png/f5InJiCm4Dtz5QTE8D4VO62Xi21G9Rem1jUgBLmxf4wbp4m8CNH42D62409HYO6f6HYC-0z_0R_0EQGbJTLI88jbd--zTy-N-qXV0sfq15ljKEg4CSAK4IRvtX_gM3M3A85waBGnkAsZDg5QcKXBs6UIKPD7DhyE9Ol687c043A6W-f64GZMOPExz5n1oD-VtmUg1GRt3nING74msWuKAIPW_XnInDh1t6i1RpsNNY3KSPo0YUmJ0j6VMUR18kD4_JeSsCSOg1lTnw2ulL7G5VPHBO4FAvMwe4VLEAoiGMKt4DAlDH4XATHOg3l2L5QdZ9fVQ2DoerkGBhqIq7NffLZ8_DQpjxb2GW9fe5wwF5560By5HkI7_jdSQ1YY1RYO6N9f-oLCmcI7pV9cDYn9clTBuG7yEvy5MMMdq7BfK437Fj0CRtx3xV5C-gBaKiFzfkgielnDfYYeI--ocoUB32drmv-jCRufLSitABTz9EYYk8vBUnZf2pZY6Xj8BUVKBx3-OLofyjn2m-sBloZKD1bEc2OP3uPPvOslj4CxqC0rYlP0VJy72ZhASwNmbnVpnvd-v1C00F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
      - EmployeeUI: Đây là lớp giao diện người dùng cho phép nhân viên tương tác với hệ thống. Nó hiển thị thông tin thời gian và nhận đầu vào từ người dùng.
      - TimecardController: Lớp này xử lý logic của ứng dụng và kết nối giữa giao diện người dùng và lớp entity. Nó quản lý việc gửi thông tin thời gian làm việc đến hệ thống và xác thực các giờ làm việc.
      - Timecard: Lớp này đại diện cho thông tin thời gian làm việc của nhân viên. Nó lưu trữ các thuộc tính như ID thời gian, ngày bắt đầu, ngày kết thúc, số giờ làm việc và trạng thái của thời gian.
      - Employee: chứa thông tin cơ bản của nhân viên như mã nhân viên, tên, và truy xuất thông tin liên quan đến thời gian làm việc của họ.
### d. Một số thuộc tính và phương thức của các lớp phân tích:
      - EmployeeUI: không có thuộc tính, hiển thị giao diện tương tác với nhân viên.
      - TimecardController: 
        + submitTimecard(): Phương thức này được gọi khi nhân viên muốn gửi thông tin thời gian làm việc của họ. Nó thực hiện các bước xác thực và cập nhật trạng thái của thời gian.
        + validateHours(): Phương thức này kiểm tra tính hợp lệ của số giờ làm việc mà nhân viên đã nhập.
        + retrieveChargeNumbers(): Phương thức này được gọi để lấy danh sách các số tài khoản mà nhân viên có thể sử dụng khi nhập giờ làm việc.
        + retrieveTimecard(): Phương thức này truy xuất thời gian hiện tại của nhân viên.
        + saveHours(): Phương thức này lưu trữ số giờ làm việc mà nhân viên đã nhập vào đối tượng Timecard.
      - Timecard: 
        + timecardId
        + startDate
        + endDate
        + hoursWorked (mảng chứa số giờ làm việc theo từng số tài khoản)
      - Employee:
        + employeeId: ID duy nhất của nhân viên.
        + name: Tên nhân viên.
        + Chức vụ
        + Giới hạn giờ làm việc (như số giờ tối đa cho phép)
        + payment: Tham chiếu đến phương thức thanh toán của nhân viên, kiểu Payment.
      
### e. Mối quan hệ giữa các lớp
      - EmployeeUI giao tiếp với TimecardController để cho phép nhân viên thực hiện các hành động như xem và cập nhật thông tin thời gian. EmployeeUI gửi yêu cầu tới TimecardController..
      - TimecardController quản lý đối tượng Timecard: Tạo, lưu trữ thông tin, xác thực giờ làm việc và thay đổi trạng thái.
Giao tiếp với ProjectManagementDatabase để lấy danh sách các số tài khoản (ChargeNumber) mà nhân viên có thể sử dụng.
      - Mỗi đối tượng Timecard có thể được liên kết với một đối tượng Employee, cho phép theo dõi thời gian làm việc của từng nhân viên.
      - TimecardController có thể sử dụng thông tin từ lớp Employee để xác thực và quản lý thông tin thời gian cho nhân viên.
### f. Biểu đồ lớp mô tả lớp phân tích
![classUML](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNKdvfNafYKQM2Qsv1JdvbQcgefq9YiO8ZLt9-NabHVev2I6PkQd9YKOepX9-JMWIIT-9ApIl9BAc4IuC4dM62CBD0WYvSN8uAkhf07KuWoba1GhieS3c3QIukBeVKl1IWOm00003__mC0)
## 5. Hợp nhất kết quả phân tích
![UMLHopNhat](https://www.planttext.com/api/plantuml/png/L8_D3S8m38Nldi8BT8UsQHDnGm862AaFbVA3qlIGsNfW95OWfWs2qvE_z-mdlxPdkoGTq-eim3siVj8nurbdHpx941tg1JimmQSOB5x8aac7BNPeANAeXuBcb75q3nio4KDHuR72RFWfgjdRYPtnstET7HaTf_yAMQzLcw42wB1fId_FCY28ZyB88a6og1sgVH88q9AVojDl0000__y30000)
### Tài Liệu Mô Tả Ca Sử Dụng: Quản Lý Thời Gian và Phương Thức Thanh Toán
#### Mô Tả Ngắn Gọn
      Ca sử dụng này cho phép Nhân viên cập nhật và gửi thông tin thời gian làm việc, đồng thời chọn phương thức thanh toán cho khoản lương của mình. Nhân viên sẽ ghi lại giờ làm việc hàng tuần cho các dự án cụ thể và có thể chọn cách nhận lương, bao gồm nhận trực tiếp, nhận qua bưu điện, hoặc chuyển khoản trực tiếp vào tài khoản ngân hàng.
#### Luồng Sự Kiện
##### Luồng Cơ Bản
      Ca sử dụng này bắt đầu khi Nhân viên muốn nhập số giờ làm việc và chọn phương thức thanh toán.
##### 1. Cập Nhật Thời Gian Làm Việc
      - Hệ thống lấy và hiển thị thời gian làm việc hiện tại của Nhân viên. Nếu không có thời gian làm việc cho kỳ thanh toán hiện tại, hệ thống sẽ tạo một cái mới. Ngày bắt đầu và kết thúc của thời gian làm việc được hệ thống thiết lập và không thể thay đổi.
      - Hệ thống lấy và hiển thị danh sách các mã dự án có sẵn từ Cơ sở Dữ liệu Quản lý Dự án.
      - Nhân viên chọn mã dự án thích hợp và nhập số giờ làm việc cho bất kỳ ngày nào trong khoảng thời gian của thời gian làm việc.
      - Khi Nhân viên đã nhập thông tin, hệ thống lưu thời gian làm việc.
##### 2. Gửi Thời Gian Làm Việc
      - Nhân viên có thể yêu cầu hệ thống gửi thời gian làm việc. Hệ thống sẽ gán ngày hiện tại cho thời gian làm việc như ngày gửi và thay đổi trạng thái thành “đã gửi.” Không được phép thay đổi sau khi gửi.
      - Hệ thống xác thực thời gian làm việc, đảm bảo tổng số giờ không vượt quá giới hạn quy định.
      - Hệ thống lưu và làm cho thời gian làm việc trở thành chỉ đọc.
      - Chọn Phương Thức Thanh Toán
##### 3. Hệ thống yêu cầu Nhân viên chỉ định phương thức thanh toán mong muốn (nhận trực tiếp, qua bưu điện, hoặc chuyển khoản trực tiếp).
      - Nếu Nhân viên chọn phương thức “nhận trực tiếp”, không yêu cầu thêm thông tin.
      - Nếu Nhân viên chọn phương thức “qua bưu điện”, hệ thống yêu cầu Nhân viên cung cấp địa chỉ nhận séc.
      - Nếu Nhân viên chọn phương thức “chuyển khoản trực tiếp”, hệ thống yêu cầu Nhân viên cung cấp tên ngân hàng và số tài khoản.
      - Hệ thống cập nhật thông tin Nhân viên với phương thức thanh toán đã chọn.
#### Luồng Thay Thế
      - Số Giờ Không Hợp Lệ: Nếu số giờ không hợp lệ được nhập (>24 hoặc vượt quá giới hạn), hệ thống hiển thị thông báo lỗi và yêu cầu nhập lại.
      - Thời Gian Làm Việc Đã Được Gửi: Nếu thời gian làm việc đã được gửi, hệ thống hiển thị bản sao chỉ đọc và thông báo rằng không thể thay đổi.
      - Cơ Sở Dữ Liệu Quản Lý Dự Án Không Có Sẵn: Nếu không có danh sách mã dự án, hệ thống thông báo lỗi và cho phép Nhân viên chọn tiếp tục hoặc hủy bỏ.
      - Nhân Viên Không Được Tìm Thấy: Nếu thông tin Nhân viên không thể tìm thấy, hệ thống hiển thị thông báo lỗi và ca sử dụng kết thúc.
#### Yêu Cầu Đặc Biệt: Không có.
#### Điều Kiện Tiền Đề: 
      Nhân viên phải đăng nhập vào hệ thống trước khi ca sử dụng này bắt đầu.
#### Điều Kiện Hậu Đề: 
      Nếu ca sử dụng thành công, thông tin thời gian làm việc và phương thức thanh toán của Nhân viên sẽ được lưu vào hệ thống. Ngược lại, trạng thái của hệ thống không thay đổi.



