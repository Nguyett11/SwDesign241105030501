# LAB2 PHÂN TÍCH CÁC CA SỬ DỤNG TRONG PAYROLL SYSTEM

## 1. Ca sử dụng Create Administrative Report
### a. Các lớp phân tích
- Lớp Boundary: PayrollAdministratorUI
- Lớp Controller: ReportController
- Lớp entities: ReportGenerator, Report, ReportStorage
### b. Biểu đồ Sequence
![CreateAdministrativeReport](https://www.planttext.com/api/plantuml/png/f9InJkD048RxVOefEGbU8BeWWf5yI5T43XIKZhEALonhv8mZkJnTGK6LYkAQS152GegWeB8BYaMynpu1ht2pkyab4LPq9roil3kVv_zdTkJt-kLWX76EnOLaB4umow4RbtacPMTm8PGOOHxRmtW4tGvZ_QnGWpWl6w7JOukT7hCaKqXHYFXbbcFWTvAxB570k4A1vI8QSiN_IaJXPj2TRHxr28s7t4LwZBNRS6AgsmmEDIs9NTfjrkt0tZuvQS6PVYWWCTLz0UYu_f9ZP9UWADW6mTZKlmIWS4Igvx0ZCqB42ja5DTJJ4lgcUaHudTWqoxDpKxqWOAghP1TGFoXGgVwjO4pvr1SM1Sv1s5hKi99Tg7mYDuibmf6f7q4AKryLa9fwTWcItXdG4uLEUobDkUi95VhsH9WQhhN9mG5ytVD6SrFDR5T-hBbzdUYPxvoZgR6MfiP-8-cVYaoQ-dej9PSZlk7jFDNF9DfiaVAS-BZBGE4RiKq7Fy1S3ToaV7zxAlvXKAJ5ckOaDFLSGBb9Bc-nr_BvFyoElPgndjejcSlrtD-DWydhLAM4asDVSw-nvaPsLVzsrhLx8MUgExJZT2ksoTck-UB-fy_-2zVi0rhjB-KF0000__y30000)
### c. Nhiệm vụ của từng lớp phân tích:
- Lớp PayrollAdministratorUI: Lớp này là lớp giao diện hiển thị form để nhập tiêu chí báo cáo, chọn lưu hoặc hủy báo cáo được thực hiện bởi Report Administrator
- Lớp ReportController: Nhận yêu cầu tạo và lưu báo cáo từ giao diện, kiểm tra dữ liệu, và điều phối việc tạo/lưu báo cáo.
- Lớp ReportGenerator: Tạo báo cáo dựa trên tiêu chí (loại báo cáo, ngày bắt đầu, ngày kết thúc, tên nhân viên).
- Lớp Report: Chứa nội dung báo cáo được tạo.
- ReportStorage: Xử lý việc lưu báo cáo vào vị trí chỉ định.
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- Lớp PayrollAdministratorUI:
  + requestReportCreation(): Gửi yêu cầu tạo báo cáo đến ReportController.
  + displayReport(report: Report): Hiển thị báo cáo đã được tạo ra.
  + requestSaveReport(): Gửi yêu cầu lưu báo cáo đến ReportController.
  + displayErrorMessage(): Hiển thị thông báo lỗi cho người dùng.
- Lớp ReportController:
  + report: Đối tượng báo cáo được tạo ra.
  + createReport(reportType: String, startDate: Date, endDate: Date, employeeName: String): Xác thực dữ liệu và gọi ReportGenerator để tạo báo cáo.
  + saveReport(report: Report, fileName: String, location: String): Gọi ReportStorage để lưu báo cáo với tên tệp và vị trí chỉ định.
  + displayError(error: String): Gửi thông báo lỗi đến PayrollAdministratorUI nếu có vấn đề trong quá trình xử lý.
- Lớp ReportGenerator:
  + reportType: Loại báo cáo (e.g., "Total Hours Worked" hoặc "Pay Year-to-Date").
  + startDate: Ngày bắt đầu của báo cáo.
  + endDate: Ngày kết thúc của báo cáo.
  + employeeName: Tên nhân viên hoặc danh sách tên nhân viên.
  + generateReport(): Tạo và trả về một đối tượng Report dựa trên các tiêu chí đầu vào.
  + validateCriteria(): Kiểm tra tính hợp lệ của các tiêu chí. Trả về true nếu hợp lệ, false nếu không.
- Lớp Report:
  + content: Danh sách lưu nội dung chi tiết của báo cáo (ví dụ: giờ làm hoặc thu nhập của từng nhân viên).
  + generationDate: Ngày tạo báo cáo.
  + reportType: Loại báo cáo (e.g., "Total Hours Worked" hoặc "Pay Year-to-Date").
  + startDate: Ngày bắt đầu của báo cáo.
  + endDate: Ngày kết thúc của báo cáo.
  + employeeNames: Danh sách tên nhân viên trong báo cáo.
  + createdBy: sẽ lưu ID hoặc tên của Quản trị viên Nhân sự (người đã tạo báo cáo).
  + getContent(): Trả về nội dung báo cáo.
  + setContent(): Thiết lập nội dung báo cáo.
  + getSummary(): Trả về tóm tắt báo cáo (e.g., loại báo cáo, ngày bắt đầu và kết thúc, và số lượng nhân viên).
- Lớp ReportStorage:
  + fileName: Tên tệp để lưu báo cáo.
  + location: Vị trí lưu trữ báo cáo.
  + saveReport(): Lưu báo cáo vào vị trí chỉ định. Trả về true nếu lưu thành công, false nếu gặp lỗi.
  + validateLocation(): Kiểm tra tính hợp lệ của vị trí lưu. Trả về true nếu hợp lệ, false nếu không.
### e. Mối quan hệ giữa các lớp
- PayrollAdministratorUI là giao diện để Quản trị viên Nhân sự gửi yêu cầu tạo hoặc lưu báo cáo đến ReportController.
- ReportController là lớp điều khiển trung tâm, xử lý yêu cầu từ UI, gọi ReportGenerator để tạo báo cáo và ReportStorage để lưu báo cáo.
- ReportGenerator tạo ra đối tượng Report chứa nội dung báo cáo dựa trên các tiêu chí đầu vào (loại báo cáo, ngày bắt đầu, ngày kết thúc, tên nhân viên), sau đó trả về Report cho ReportController.
- ReportController sau đó giữ đối tượng Report này để hiển thị cho Quản trị viên hoặc chuyển tiếp yêu cầu lưu đến ReportStorage khi cần.
### f. Biểu đồ lớp mô tả lớp phân tích
![ReportAdminitrative](https://www.planttext.com/api/plantuml/png/L8x13S8m34Nldi8BT8UcJOMu8H0316AXIAc37FUGsJWm4YkGjBtqzEJ_REl_Fjy-gnDTvWZmI0jx9mKlhaYAqVWvSCWgJfFSp-Wo6dWcrYhnIkyaEcvJ96bs068DMdPv8gRrjhdnw5faZz6jRheNDJC16Eow-d1e676ZtJc1NO48q1FxrluF003__mC0)

## 2. Ca sử dụng Create Employee Report
### a. Các lớp phân tích
- Lớp Boundary: EmployeeUI
- Lớp Controller: EmployeeReportController
- Lớp entities: ReportGenerator, Report, ReportStorage
### b. Biểu đồ Sequence
![CreateEmployeeReport](https://www.planttext.com/api/plantuml/png/Z5JDYXD14BxtKnHxqiE-G0wocIIx2gk8Hj1ZfzDaHcUwGwSdx1p5moABXnn4H0HZa8M5u8gAE7tmq67Vev_0Lx2w9_zcqJaqpLTVVLLVTJ6_pQ-3WQPAvrbAADDIGIlhfxBWd7HaBhfK5KlaqHsW0wWJ9eLMCbtY3tXVAjseq9Ghpue85phH1LJ18owuebuUOutDc8UQcz13PD8Uzv4MwL9DEtJ0uRwIJpdJTwd0M8O9pSWp3WbPT0Bxjw1UWyYLdpNCHguypw6m5pcmSDMk74leM3mO7gJk-L4DZfoP9g2Jm8pjT8r2Kmt74lEI5GYf_G1xRMTUYnuCd1b1Bt7clOSp6EBrbA6CXCoPjngwpdm1EnPx1F2BVCd36hHLNi19xifFoA0YXe4TinWoEwaKcVs6ufLOI3o4_QhPjdBb1DBGqdzbHlEft4ReXG0TEtFspynWu5viFme4x8K8IbjZRg3IAt5DPIww95HkOCkRSmyZeQ0LwgvDdJGylVaNdJHtML-fpKROG7XQijFgYhdjQV7-JrOhabvTvciPDxJzMM2UDtgpac_Lu7YJD7Jc7QwFTpF4pHZwecXkMdNcar_wPJHd8YQjXPV7E7iGiIkdOjlBR7HrwSo4XMQMdjfn66zdXn5VyZcSh2bksY1XZUS2EX7mhBeo-nLVhlmk8COL_y4ME7OywUESpUdr2wJNsa7ccsJNXhIHEfq_sBm48kS5PbE94njNUq8EyCG_q1y0003__mC0)
### c. Nhiệm vụ của từng lớp phân tích:
- EmployeeUI: Là giao diện người dùng để giao tiếp giữa hệ thống và nhân viên. Hiển thị các form để nhập tiêu chí báo cáo và hiển thị kết quả báo cáo cho nhân viên. Nhận các lệnh từ nhân viên, chẳng hạn như chọn loại báo cáo, nhập ngày bắt đầu và ngày kết thúc, và chọn số mã công việc.
- EmployeeReportController: Điều khiển luồng xử lý của use case. Nhận dữ liệu từ EmployeeUI và xử lý logic cần thiết để tạo báo cáo. Gọi các phương thức từ các lớp thực thể như ReportGenerator để thực hiện công việc tạo báo cáo. Xử lý các điều kiện lỗi và phản hồi lại EmployeeUI khi có thông tin không hợp lệ hoặc thiếu.
- ReportGenerator: Chịu trách nhiệm thu thập dữ liệu và xử lý chúng để tạo báo cáo theo tiêu chí được cung cấp. Truy cập dữ liệu từ cơ sở dữ liệu hoặc từ các nguồn khác để tổng hợp thông tin cần thiết cho báo cáo. Tạo ra các thực thể báo cáo (Report) sau khi xử lý dữ liệu.
- Report: Là thực thể đại diện cho báo cáo đã được tạo ra.Chứa các thông tin về báo cáo như nội dung, loại báo cáo, thời gian bắt đầu và kết thúc, và các thông tin liên quan. Được dùng để truyền dữ liệu báo cáo đã xử lý từ ReportGenerator đến EmployeeReportController và hiển thị trên EmployeeUI.
- ReportStorage: Quản lý việc lưu trữ và quản lý báo cáo. Thực hiện việc lưu báo cáo vào vị trí được chỉ định với tên cụ thể. Xác nhận và phản hồi lại cho EmployeeReportController về trạng thái lưu trữ báo cáo (thành công hoặc thất bại).
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- Lớp EmployeeUI:
  + reportType: Loại báo cáo mà nhân viên chọn.
  + startDate: Ngày bắt đầu cho báo cáo.
  + endDate: Ngày kết thúc cho báo cáo.
  + chargeNumber: Số mã công việc (chỉ có trong báo cáo "Tổng số giờ làm việc cho một dự án").
  + displayReport(): Hiển thị báo cáo cho nhân viên.
  + getReportCriteria(): Nhận tiêu chí báo cáo từ nhân viên.
  + showError(): Hiển thị thông báo lỗi nếu có vấn đề xảy ra.
- Lớp EmployeeReportController:
  + reportGenerator: Thực thể ReportGenerator để tạo báo cáo.
  + reportStorage: Thực thể ReportStorage để lưu báo cáo.
  + employeeUI: Thực thể EmployeeUI để giao tiếp với nhân viên.
  + processReportRequest(): Xử lý yêu cầu tạo báo cáo.
  + generateReport(): Gọi ReportGenerator để tạo báo cáo.
  + saveReport(): Lưu báo cáo vào vị trí chỉ định thông qua ReportStorage.
  + handleError(): Xử lý lỗi và thông báo lại cho giao diện người dùng.
- Lớp ReportGenerator:
  + reportType: Loại báo cáo (“Total Hours Worked,” “Total Hours Worked for a Project”, “Vacation/Sick Leave,” or “Total Pay Year-to Date”).
  + startDate: Ngày bắt đầu báo cáo.
  + endDate: Ngày kết thúc báo cáo.
  + chargeNumber: Mã số công việc (chỉ có trong loại báo cáo dự án).
  + generateTotalHoursReport(): Tạo báo cáo "Tổng số giờ làm việc".
  + generateProjectReport(): Tạo báo cáo "Tổng số giờ làm việc cho một dự án".
  + generateLeaveReport(): Tạo báo cáo "Vacation/Sick Leave".
  + generateTotalPayReport(): Tạo báo cáo "Total Pay Year-to-Date".
- Lớp Report:
  + reportType: Loại báo cáo (“Total Hours Worked,” “Total Hours Worked for a Project”, “Vacation/Sick Leave,” or “Total Pay Year-to Date”).
  + startDate: Ngày bắt đầu của báo cáo.
  + endDate: Ngày kết thúc của báo cáo.
  + content: Nội dung của báo cáo (bao gồm số liệu, tổng hợp, v.v.).
  + generateContent(): Tạo nội dung báo cáo dựa trên các dữ liệu đầu vào.
  + display(): Hiển thị báo cáo cho người dùng.
- Lớp ReportStorage:
  + fileName: Tên của báo cáo.
  + fileLocation: Vị trí lưu báo cáo.
  + saveReport(): Lưu báo cáo vào tệp với tên và vị trí xác định.
  + confirmSave(): Xác nhận báo cáo đã được lưu thành công.
### e. Mối quan hệ giữa các lớp
- EmployeeUI: Giao tiếp trực tiếp với nhân viên, nhận yêu cầu và hiển thị kết quả báo cáo. Kết nối với EmployeeReportController để xử lý logic.
- EmployeeReportController: Xử lý luồng logic của use case, tương tác với ReportGenerator để tạo báo cáo và ReportStorage để lưu báo cáo. Sau đó, nó truyền kết quả cho EmployeeUI.
- ReportGenerator: Chịu trách nhiệm tạo ra báo cáo dựa trên tiêu chí từ EmployeeReportController. Sau khi tạo xong, trả báo cáo cho EmployeeReportController.
- Report: Lưu trữ thông tin báo cáo đã tạo từ ReportGenerator. EmployeeReportController sử dụng báo cáo này để hiển thị hoặc lưu trữ.
- ReportStorage: Quản lý việc lưu trữ báo cáo. EmployeeReportController yêu cầu ReportStorage lưu báo cáo vào vị trí chỉ định.
### f. Biểu đồ lớp mô tả lớp phân tích
![CreateAdministrativeReport](https://www.planttext.com/api/plantuml/png/L8x12SCm34Nlca8BP8SajYczjdG0jH6bu5X1KGwUBOUEr1KQnwMGquFtFaAVzTtEHchB607kigI1D6COfoYP-NP6ch63XoHJYNz_uKdKNBMHjQnwu6GlorZZYHChcUpD7LjH_gYksvAUN4e0wB1fjeDzWSDA_sC0lmCHeEKqbC-_0000__y30000)
## 3. Ca sử dụng Login
### a. Các lớp phân tích
- Lớp Boundary: LoginUI
- Lớp Controller: LoginController
- Lớp entities: Authenticator, User
### b. Biểu đồ Sequence
![Login](https://www.planttext.com/api/plantuml/png/X54nRiCm3Dpr2YAJ3JJ8xg68xMG8q2r8TrOYMWEA591I2x-jGv_KBvIoOQT3WMgGJiVJ7KXzVtxj9I6dVFK6ROeC5o4sBp47Xpp2KtmTmkK4AD0Q6qFYw6Uodo-Uk1GxGo4DQOGsfxS2BHOphVHBfHWNuc3C1BUFq3Pm34bnLYBWbG23WnkAV4HsfYsQhW6Xu7ecLupGIxMe7rPfRRgYxHjuHpyuJFIVleVjRCwKCeVbtH23Cf9zWcgYTaEOpjgWSiy5mYzl0xgcx4C3bacJItDd4b6hDRc-wxHdDyZDupYDyPojLN5L6_92S9hJ_ewuFpqoHwusYteTduvyQN6ZZi6PlMxbSty0003__mC0)
### c. Nhiệm vụ của từng lớp phân tích:
- LoginUI: Giao diện người dùng cho quá trình đăng nhập, nơi người dùng nhập tên và mật khẩu.
- LoginController: Xử lý logic đăng nhập. Kiểm tra tính hợp lệ của tên và mật khẩu, xác thực và đăng nhập người dùng.
- Authenticator: Kiểm tra tính hợp lệ của tên và mật khẩu, xác thực người dùng.
- User: Lưu trữ thông tin người dùng trong hệ thống (thông tin đăng nhập, mật khẩu, vai trò,...).
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- LoginUI: 
  + username: Tên người dùng.
  + password: Mật khẩu.
  + getCredentials(): Nhận tên và mật khẩu từ người dùng.
  + displayError(message: String): Hiển thị thông báo lỗi nếu thông tin đăng nhập không hợp lệ.
  + displayLoginScreen(): Hiển thị giao diện đăng nhập cho người dùng.
- LoginController:
  + authenticator: Đối tượng thực hiện xác thực tên và mật khẩu.
  + processLogin(username: String, password: String): Nhận tên và mật khẩu từ LoginUI, gọi Authenticator để kiểm tra tính hợp lệ và thực hiện đăng nhập.
  + handleLoginError(): Xử lý khi tên hoặc mật khẩu không hợp lệ, yêu cầu người dùng nhập lại hoặc hủy đăng nhập.
- Authenticator:
  + validUsernames: Danh sách tên người dùng hợp lệ.
  + validPasswords: Danh sách mật khẩu hợp lệ (hoặc kiểm tra với cơ sở dữ liệu).
  + validateCredentials(username: String, password: String): Kiểm tra tính hợp lệ của tên người dùng và mật khẩu.
- User:
  + username: Tên đăng nhập của người dùng.
  + password: Mật khẩu của người dùng.
  + role: Vai trò của người dùng (ví dụ: quản trị viên, nhân viên).
  + isValidPassword(password: String): Kiểm tra mật khẩu có đúng với người dùng không.
  + getRole(): Lấy vai trò của người dùng sau khi đăng nhập thành công.
### e. Mối quan hệ giữa các lớp
- LoginUI (Boundary): Tương tác với người dùng, nhận thông tin đăng nhập và hiển thị lỗi khi cần thiết.
- LoginController (Controller): Quản lý quá trình đăng nhập, sử dụng Authenticator để xác thực tên và mật khẩu, sau đó thực hiện đăng nhập hoặc xử lý lỗi.
- Authenticator (Entity): Kiểm tra tính hợp lệ của tên người dùng và mật khẩu, trả về kết quả cho LoginController.
- User (Entity): Đại diện cho người dùng trong hệ thống, chứa thông tin đăng nhập, mật khẩu và vai trò.
### f. Biểu đồ lớp mô tả lớp phân tích
