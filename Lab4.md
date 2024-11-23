# PAYROLL SYSTEM USE CASE DESIGN

## 1. Describe interaction among design objects 

### Các đối tượng tham gia và cách chúng tương tác với nhau trong các ca sử dụng
a. Nhân viên (Employee)
- Employee gửi thông tin về giờ làm việc thông qua Timecard.
- Các dữ liệu như giờ làm việc, loại nhân viên (nhân viên theo giờ, lương cố định, hoặc hoa hồng), và các thông tin khác được lưu trữ trong cơ sở dữ liệu để phục vụ cho việc tính toán bảng lương.
- Quản lý giờ làm việc (Timecard và TimecardForm)
  
b. Đối tượng Timecard lưu trữ thông tin chi tiết về số giờ làm việc của nhân viên.
- TimecardForm là giao diện người dùng hoặc lớp nhập liệu cho phép nhân viên hoặc quản lý cập nhật thông tin giờ làm việc.
- Sau khi nhận dữ liệu, TimecardForm gửi dữ liệu đến TimecardController để xác minh và cập nhật thông tin trong hệ thống.
- Bộ điều khiển giờ làm việc (TimecardController)
  
c. TimecardController đóng vai trò trung gian, phối hợp giữa Timecard, Employee, và cơ sở dữ liệu quản lý dự án (ProjectManagementDatabase).
- Nó thực hiện các chức năng chính:
- Lấy charge codes (mã công việc/dự án) từ cơ sở dữ liệu dự án.
- Cập nhật giờ làm việc trong Timecard cho từng dự án cụ thể.
- Đảm bảo tổng số giờ làm việc tuân thủ các quy định và không vượt quá giới hạn.
  
d. Xử lý bảng lương (PayRollController)
- Khi đến thời điểm trả lương, PayRollController tương tác với các lớp con của Employee để tính toán:
- HourlyEmployee: Tính lương dựa trên số giờ làm việc thực tế và mức lương theo giờ.
- SalariedEmployee: Lương được cố định dựa trên mức lương hàng tháng.
- CommissionedEmployee: Lương bao gồm lương cơ bản và hoa hồng dựa trên doanh số bán hàng.
  
e. PayRollController xử lý các bước:
- Tính toán tổng lương và khấu trừ các khoản cần thiết.
- Phối hợp với BankSystem để chuyển khoản thanh toán lương.
- Gửi lệnh tới PrinterInterface để tạo bảng lương chi tiết (Paycheck) cho nhân viên.
  
f. Bảng lương (Paycheck)
- Paycheck là đối tượng được PayRollController tạo ra, bao gồm thông tin chi tiết như: Tên nhân viên, loại nhân viên.
- Số giờ làm việc hoặc mức lương cố định.
- Các khoản khấu trừ (thuế, bảo hiểm) và lương thực nhận.
- Paycheck sau đó được gửi qua hệ thống in ấn hoặc giao diện người dùng.
  
g. Đồng hồ hệ thống (SystemClockInterface)
- SystemClockInterface xác định thời gian trả lương và kích hoạt quy trình xử lý bảng lương (Payroll).
- Nó đảm bảo bảng lương được xử lý đúng lịch trình, ví dụ: trả lương hàng tuần, hai tuần một lần, hoặc hàng tháng.

## 2. Simplify sequence diagrams using subsystems 

### Sử dụng các subsystem để đơn giản hóa các biểu đồ sequence. Một số subsystem:

a. Subsystem: Employee Management
Chịu trách nhiệm quản lý thông tin nhân viên, theo dõi giờ làm việc, và các dữ liệu liên quan đến nhân viên.
- Thành phần chính:
  + Employee: Đại diện cho nhân viên, có các thuộc tính như ID, tên, loại nhân viên (hourly, salaried, commissioned).
  + Timecard: Ghi nhận thông tin giờ làm việc của nhân viên.
  + TimecardForm: Giao diện hoặc lớp nhập liệu để nhân viên gửi thông tin giờ làm việc.
  + TimecardController: Điều phối và xử lý các yêu cầu liên quan đến giờ làm việc.
- Mối quan hệ: TimecardController cập nhật dữ liệu từ TimecardForm và liên kết thông tin với đối tượng Employee.
  
b. Subsystem: Project Management
Liên quan đến quản lý các dự án, mã công việc (charge codes), và phân bổ giờ làm việc của nhân viên theo từng dự án.
- Thành phần chính:
  + ProjectManagementDatabase: Lưu trữ thông tin về các dự án, mã công việc, và ngân sách.
  + TimecardController: Lấy mã công việc (charge codes) từ ProjectManagementDatabase và gán giờ làm việc của nhân viên cho từng dự án.
- Mối quan hệ:
  + TimecardController tương tác trực tiếp với ProjectManagementDatabase để đảm bảo thông tin mã công việc được cập nhật và chính xác.

c. Subsystem: Payroll Processing
Chịu trách nhiệm tính toán lương, khấu trừ, và tạo bảng lương chi tiết.
- Thành phần chính:
  + PayRollController: Điều phối toàn bộ quy trình xử lý bảng lương.
  + Employee (và các lớp con):
    HourlyEmployee: Tính lương theo số giờ làm việc.
    SalariedEmployee: Lương cố định hàng tháng.
    CommissionedEmployee: Lương cơ bản cộng hoa hồng.
    SystemClockInterface: Xác định thời gian và tần suất xử lý bảng lương (hàng tuần, hàng tháng).
- Mối quan hệ:
  + PayRollController truy xuất thông tin từ các lớp con của Employee để tính toán lương chính xác.
  + SystemClockInterface kích hoạt xử lý lương vào thời điểm quy định.

d. Subsystem: Payment Processing
Quản lý việc thanh toán lương và xử lý giao dịch.
- Thành phần chính:
  + BankSystem: Chuyển khoản tiền lương vào tài khoản ngân hàng của nhân viên.
  + Paycheck: Lưu thông tin bảng lương chi tiết (lương gộp, khấu trừ, lương thực nhận).
- Mối quan hệ:
  + PayRollController tương tác với BankSystem để thực hiện thanh toán.
  + Paycheck được tạo ra từ kết quả tính toán của PayRollController và được lưu trữ hoặc in.
e. Subsystem: Reporting and Communication
Cung cấp báo cáo và giao tiếp với nhân viên, quản lý, hoặc các bên liên quan.
- Thành phần chính:
  + PrinterInterface: In bảng lương (Paycheck) và các báo cáo liên quan.
  + NotificationSystem (nếu có): Gửi thông báo về lương đã thanh toán hoặc cảnh báo về giờ làm việc vượt giới hạn.
- Mối quan hệ:
  + PayRollController gửi dữ liệu cho PrinterInterface để tạo báo cáo.
  + NotificationSystem có thể tích hợp với Employee để thông báo các cập nhật.

## Sequence diagrams đã được đơn giản hóa:

### Sequence diagrams của ca sử dụng Select Payment Mebthod
![SelectPayment](https://www.planttext.com/api/plantuml/png/X5HBJiCm5Dpd54_Tq4hq0bcWYXIaBeeg2WTuTLuRGs97jbFKO_G6V7Qis7V18eXxS0AkG7xz97749f6UtqncngFyxZv7sg0oIHGwo8nKS1N5eTmG0MhetGJfgu0rJzz5pt7Em4jV67njVtPR3kRxusVt9bQmJfz19mkzqOOY9yxOEECn2WDtF2A6oh-MAYhuJWSzwwedXL4o34dL0CTn7JR3pMqsRg1QqnOe8c5cIZBIccSMSj0bYiTvuQ6nhRWmf2RvOuci3AOvR4Ba0p4pHO4hoZyrHeCBr7jinsaMyI7zuKKjFHSqXHceaZub4qY_7nMlWLFB-GHv3C25DORSHqDs1iUIVqRKATM59HaMU06g5NdI9zsFozt9UE1q-nzsg5Da4YM07Vaw9JNlreKaRXkZAiZ9-1mE9jjjAGdhRTWJveMe3grqxHeDxVgO54kkech_lY3l4jFebGjnFl5A1ZHS2hkMPaaxf1HiyuJbYfT9sA72TaELYLAzLOFzlXej3kJJlsQS4Ga__oFz0G00__y30000)

### Sequence diagrams của ca sử dụng Maintain Timecard
![MT](https://www.planttext.com/api/plantuml/png/Z5GzJiCm6DrpYazP21AzG0PKAG6f0py3YDbrlYQ6n8vifwZ7w0tusPZOEp04SGzEm1LmITB4JGACUNxl-NtFThusRrEbYTH5bZg4QY7X9CjJiK84ei0zJyed3ajMld3NSGuWA1yfg6AkLafZ1ilo0TxNdvir0_tn-hbvvh6J6pT6MKwutdcT4KvYpD10MzVT5YtkMhfBAMwHwZrPZOwho4gAD3KqYaen7bUg2eKMjbLNB4DAPFH3RZw6AQT2PXPj2mnJ0y7rTbkKbg25NISYcio9mlwqORFIcRg_QWvaL-Jas0hfW-6XRA0GDM6fyX9HI7KZv1r6Hv1NlhFmqB7cwrYrQNrOafIPnFXVJsUW2MFTcyQ71MgQ10cHCGOYGkLrNFeNOJAIJw8k90VQ-en5Q50Vg4GpqOMyphkJsIDXNV4i7AniD0yLVC5arYnLMuosidzpVIYiJEPaQexN3JHMVlyb_16p5loUqhvXAX7tGQKccWdkZJJbJ957sz_BDm000F__0m00)

### Sequence diagrams của ca sử dụng Run Payroll
![RP](https://www.planttext.com/api/plantuml/png/d5LBRjim4Dtp50DjuYno0Is2074B54Y284OFCA763b6ALCXH01yZDsZHNLVTUz65YzuZ9-WLIbbaRKjK6sId-Rttvf6IVcz-N7X6nssj1Kgs3XPhprHVQYi_0Nee-XXsYKA84xZSVf7WstlV5vwsd-7dyylcMG7_-lwo-MfMeDNscu775ere0hYIga73S8jhPxM-TLQIzoeqTWGn2_jqSJJrhcwqNHDTey4LrHHItLXAmpvV3Dcwv9Xj1p75TaUD3L7i_Xlb9Hq96R7B1ueUfg0G5JBUewVanJp5XqwaPB3xy3JEpiSEbi1EhLRaOkMkDRDJ8SPEX-6naIKiYUL3AlZtDk44a8plUmL9OXbEcTmwzLufps5qkDpP1BiZRfq1EfZEqkOtpqqB0PbhzfhbvyIej9ybk0_pqu3r5XFoI6_q989DI7cLCNk8ANFI_In1efQjHgQGcWq0uXRzjSwvuF69KaCoeJcEfvmuK63DKhbw4R2g8y9_xZgW2VSW_mwCFWebDFrph6GKZpyakUNRfkfjwteNZDpceNAh3oL53pxk8AkSWBmPSIwj4ai1uV_lHJWzCjMDPRLK4bbPCrOlBa9BzwVu0m00__y30000)

## 3. Describe persistence-related behavior
### Hành vi liên quan đến lưu trữ và truy xuất dữ liệu (persistence-related behavior) trong hệ thống:
#### Các lớp liên quan đến lưu trữ:
- Employee:
  + Lưu trữ thông tin cơ bản về nhân viên, bao gồm:
  + Tên, địa chỉ, thông tin liên lạc.
  + Phương thức thanh toán (ngân hàng, tiền mặt, hoặc phiếu lương).
  + Mã định danh duy nhất (empID).
  + Dữ liệu được lưu trong bảng cơ sở dữ liệu nhân viên, được sử dụng để truy xuất và cập nhật khi cần thiết.
- Timecard:
  + Lưu trữ thông tin chi tiết về số giờ làm việc của nhân viên theo giờ (HourlyEmployee).
  + Thông tin lưu trữ bao gồm: Số giờ làm việc, Tiền công theo giờ, Trạng thái của Timecard (draft, submitted).
  + Timecard được liên kết với Employee thông qua empID.
  + Dữ liệu Timecard được lưu trữ trong một bảng riêng trong cơ sở dữ liệu và liên kết với các dự án thông qua charge codes.
- PurchaseOrder:
  + Đối với nhân viên nhận hoa hồng (CommissionedEmployee), các đơn đặt hàng (PurchaseOrder) được lưu trữ để tính toán hoa hồng dựa trên doanh số.
  + Thông tin lưu trữ: Số lượng đơn đặt hàng, Giá trị đơn đặt hàng, Mã đơn đặt hàng.
- Paycheck:
  + Lưu trữ chi tiết về bảng lương đã được tạo: Số tiền lương gộp (gross pay), Các khoản khấu trừ (thuế, bảo hiểm, v.v.), Số tiền lương thực nhận (net pay), Ngày thanh toán và phương thức thanh toán.
  + Paycheck được lưu vào lịch sử giao dịch của nhân viên để phục vụ báo cáo hoặc kiểm tra sau này.
- Project:
  + Lưu trữ thông tin liên quan đến các dự án hoặc công việc: Mã công việc (charge codes), Thông tin dự án.
  + Liên kết với Timecard để phân bổ giờ làm việc của nhân viên theo từng dự án cụ thể.
#### Hành vi lưu trữ và truy xuất:
##### Khi nhân viên gửi Timecard:
- Hệ thống lưu các thông tin sau vào cơ sở dữ liệu: Số giờ làm việc, Tiền công tính theo giờ,Trạng thái Timecard (draft, submitted).
- Dữ liệu phải được lưu trữ một cách nhất quán, đảm bảo rằng:
  + Timecard được liên kết chính xác với Employee thông qua empID.
  + Các mã công việc (charge codes) được lấy từ bảng Project.
##### Khi tạo Paycheck
- Hệ thống thực hiện:
  + Lưu thông tin chi tiết của Paycheck (gross pay, net pay, khấu trừ, phương thức thanh toán).
  + Ghi lại Paycheck vào lịch sử giao dịch của nhân viên, để phục vụ việc truy xuất trong tương lai.
##### Cập nhật thông tin nhân viên:
- Khi phương thức thanh toán, thông tin ngân hàng hoặc mức lương của nhân viên thay đổi:
  + Hệ thống cập nhật dữ liệu trong cơ sở dữ liệu và lưu phiên bản mới nhất.
##### Truy xuất dữ liệu khi cần:
- Khi tính toán lương:
  + Hệ thống truy xuất thông tin từ các bảng Employee, Timecard, PurchaseOrder, và Project để đảm bảo tính chính xác.
- Khi tạo báo cáo:
  + Truy xuất dữ liệu từ bảng Paycheck và các giao dịch liên quan.
 
## 4. Refine the flow of events description 

### Luồng sự kiện trong Hệ thống tính lương có thể được làm mịn thành các bước sau:

##### Maintain Timecard:
- Nhân viên sử dụng TimecardForm để truy cập và chỉnh sửa thông tin số giờ làm việc.
- TimecardForm hiển thị thông tin chi tiết của timecard hiện tại và cho phép nhân viên cập nhật dữ liệu như giờ làm, mã công việc (charge code).
- TimecardController kiểm tra tính hợp lệ của thông tin đã nhập và liên kết các thông tin mới với hồ sơ của nhân viên trong hệ thống.
- Khi nhân viên hoàn tất việc chỉnh sửa, timecard được chuyển từ trạng thái draft sang submitted, đánh dấu là đã nộp thành công.
##### Run Payroll:
- SystemClockInterface khởi chạy quy trình tính lương vào ngày trả lương được thiết lập (payday).
- PayRollController thực hiện việc tính toán lương cho từng loại nhân viên:
  + HourlyEmployee: Lấy tổng số giờ làm việc và nhân với mức lương theo giờ.
  + SalariedEmployee: Sử dụng mức lương cố định hàng tháng sau khi khấu trừ các khoản cần thiết.
  + CommissionedEmployee: Cộng lương cơ bản với hoa hồng từ doanh số bán hàng.
- BankSystem thực hiện thanh toán bằng cách chuyển khoản trực tiếp cho nhân viên có đăng ký dịch vụ direct deposit, trong khi PrinterInterface in các paychecks cho nhân viên thanh toán thủ công.
- Sau cùng, Paycheck được lưu trữ và xử lý, gửi cho nhân viên qua thông báo hoặc thông qua các hình thức in ấn/giao nhận phù hợp.

## 5. Unify classes and subsystems 
### Thống nhất các lớp và subsystem:
![thongnhat](https://www.planttext.com/api/plantuml/png/Z5MnRjim4Dtr5OIMk0KIDAjG607YeYsG045Te3DDNYNL4gcIL00ZoDIXQuEENPgrG7yW7ZeuF-8lw2-Kf4HACkNK6cJZxjtnxjqxwk_wpvbKMAYwBA8ZTB5T_wZGgx8g-0e0NMz-8hAv9wYmzYBV_6BeSurPL66on2cWs6ClCTE64fX2yteXLr916QER2Ec755ZABcrZj0-KrTjPWdAcEXl39IHehaJEqiwAAHKWPUYeyCgSUWagupHq4roGki0Ahl1gyYn1bDUB0Zf_2kfzNWB1WahZlyYbUkaiKukxZNfTE5U_2zNQWbQeFZT1C_tkR1clXVp0nH9eM0t9i4ZXdDCH1Yh1Fm5H2Rfg_eIrjOv-QMtGWIGlQghv69JL7k275v_6wFXuYk8N9oVFOq-71NbkF4Z_kcfreYEaXq0o8Cj3fAMnWXU5IK3qv7MX-vJbizuCP65jGUVGTX8uKi6brAd2gL2WDL4vPpBqCL2ZCV-HPGeCHADAM-R4bPLughKOhtbEHyRS4DFZfTUtg5dhd_GJDEfokp3p3OsV6ox9iDekpAnBkpGkVkgsoA6dJmlfr0h9WIqexD0WFSH9oTusO_8OY6WlAX2HGNP0ZzlP9-EUvK9hUWOLbxcQEAqbliI0-agFN_bXFntGCkLLFTYclLKshBpJ9GcrXumHvv231l2wcJON_SPx4Z2ZQP2-4Raxye005-_cRsx0D-OgR3CTfFyU9LOqZfMTkXig7hzjrzzrhvd-CQ-lIEdtdROytctNNz1oyvja-ZhUFjohgEb_RZavBxY-DvW2yH4J_xdI2voc85p_DVFxTHkDnhMI7GevEWD6pSVs7m000F__0m00)
