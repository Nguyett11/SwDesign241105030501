# LAB2 PHÂN TÍCH CÁC CA SỬ DỤNG TRONG PAYROLL SYSTEM

## A. Phân tích các ca sử dụng trong hệ thống Payroll System
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
![login](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3XTNKdvfNafYKQM2JtvwPbwefq9YiO8ZLt9-NabHVWv4q1d2oKaj0aawSQNcbMIML2eubfPaW9Z9YINvO1bdc4neCKIf2nUNeuAkBb2B4uXoXb0kNCvWIe6Boo4rBmNa2W00003__mC0)
## 4. Ca sử dụng Maintain Employee Information
### a. Các lớp phân tích
- Lớp Boundary: PayrollAdministratorInterface, EmployeeInformationForm
- Lớp Controller: MaintainEmployeeController
- Lớp entities: Employee
### b. Biểu đồ Sequence
![MaintainEmployeeInformation](https://www.planttext.com/api/plantuml/png/v5OzRzD06DxlLxpAGZ8Wzaf1ZKAX4IBA4A4odXstFjK-1-UCwfa98IGG0mCBeQeg1JgLoHuwNF_8_OB-1TwpJU9pxDQ2RaHAx7llUTxFvnpVf5Ux2q534VaUeRO8GkXCQ1m6dWU3cSyuMuYGeha3T06J0I5M4F4P3UCrpe2Dk732Gsex6NwzAh7s_BaNn8upueT1w5F10luKRpAylY5sm0NwXSuBohZ0xn_6CD_md3oPpP8uN31HyftjuuAG1p1rvSe7xihl7DumkUAato-CuypuKXkXtoUJ0JnylCaPTc3eglG3XywMZmxPm92pIGL9h-Gg0bibvr4jiOIjH2iHXIj_yICGZ1kP6q5riv2rprJwbYD3fU_1qei8V9NyQ7IIyP2FvMA54I8mvjdyBhXHupELNh0cXbaXZW49KvKi0x1KSihXo6LbF6QRVcMtz6KQ8WqyzC1WzCIWTh71txWBjawafySzLCd5735u4TMfvtlZVA_ry0sFzIMtbKChLwq4OlR135yTR0LREvumYk4aGdXJNcXs0dH5DA5QOtb2hKHnFzf5sZiS_WB5IEzDld3zIPxgpgqdLTinOvIrkcwfw6ELN0bu7MdBjfmFv2MjoZYpjPPlrKDRhMxp_WTXDbHr8fTsFcoEzvUqfgxRqDlJEQX2weg__YYNg8OPLXzL98f79USLLTz9G4rR-fJL1FiRPL9FmFEYeVAdhuzmSXQRp-Ro4NcavTGZW9_cuCRZe1YN9V5_mrFf5mRTSSdxSH5SfP-HeVFjuMl0BCziNwNdSLOgTFyfSEOYwvkhNUOHTl4NNvT-0m00__y30000)
### c. Nhiệm vụ của từng lớp phân tích:
- PayrollAdministratorInterface:
  + Cung cấp giao diện để Quản trị viên tiền lương lựa chọn thao tác muốn thực hiện (thêm, cập nhật, hoặc xóa nhân viên).
  + Hiển thị các tùy chọn và yêu cầu Quản trị viên cung cấp thông tin liên quan (ví dụ: ID nhân viên khi cập nhật hoặc xóa).
  + Quản lý việc hiển thị thông báo lỗi hoặc xác nhận khi cần thiết (ví dụ: khi không tìm thấy nhân viên hoặc khi Quản trị viên xác nhận xóa).
- EmployeeInformationForm: 
  + Hiển thị biểu mẫu để Quản trị viên nhập thông tin nhân viên (bao gồm tên, địa chỉ, lương, số an sinh xã hội, và các thông tin khác).
  + Thu thập thông tin từ Quản trị viên và chuyển tiếp cho lớp Controller để xử lý (khi thêm hoặc cập nhật nhân viên).
  + Cung cấp giao diện để chỉnh sửa thông tin nhân viên khi thực hiện thao tác cập nhật.
- MaintainEmployeeController:
  + Xử lý các yêu cầu từ PayrollAdministratorInterface (chọn thao tác thêm, cập nhật, hoặc xóa nhân viên).
  + Khi thao tác là thêm hoặc cập nhật, yêu cầu EmployeeInformationForm thu thập thông tin nhân viên từ Quản trị viên.
  + Sau khi nhận thông tin, MaintainEmployeeController sẽ xử lý và thực hiện các thay đổi cần thiết trong lớp Employee (thêm, cập nhật, hoặc xóa).
  + Quản lý các thông báo và trạng thái kết quả (thành công hoặc lỗi) sau khi hoàn thành thao tác.
  + Cung cấp các thông tin phản hồi (ví dụ: trả lại ID nhân viên khi thêm mới hoặc kết quả xóa khi thao tác hoàn tất).
- Employee:
  + Lưu trữ thông tin về nhân viên như tên, địa chỉ, loại nhân viên, lương, và các dữ liệu liên quan khác.
  + Cung cấp các phương thức để tạo mới, cập nhật và xóa thông tin nhân viên từ cơ sở dữ liệu.
  + Khi thao tác là xóa, sẽ đánh dấu nhân viên là đã bị xóa trong hệ thống (thay vì xóa hoàn toàn).
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- PayrollAdministratorInterface:
  + selectedAction: Lưu trữ thao tác mà Quản trị viên chọn (thêm, cập nhật, xóa nhân viên).
  + employeeId: ID của nhân viên khi Quản trị viên thực hiện cập nhật hoặc xóa.
  + chooseAction(): Cho phép Quản trị viên chọn thao tác (thêm, cập nhật, xóa).
  + displayEmployeeForm(): Hiển thị biểu mẫu thông tin nhân viên.
  + showMessage(String message): Hiển thị thông báo cho Quản trị viên (ví dụ: thông báo lỗi hoặc thành công).
  + getEmployeeDetails(): Thu thập thông tin nhân viên từ Quản trị viên.
- EmployeeInformationForm:
  + employeeName: Tên của nhân viên.
  + employeeType: Loại nhân viên (giờ, lương cố định, hoa hồng).
  + salaryOrHourlyRate: Lương hoặc mức lương theo giờ.
  + displayForm(): Hiển thị biểu mẫu nhập thông tin nhân viên.
  + getInput(): Thu thập thông tin từ Quản trị viên và trả về dưới dạng đối tượng.
- MaintainEmployeeController:
  + action: Hành động mà Quản trị viên muốn thực hiện (thêm, cập nhật, xóa).
  + employee: Đối tượng nhân viên để thao tác (thêm, cập nhật, xóa).
  + handleAddEmployee(): Xử lý thêm mới nhân viên vào hệ thống.
  + handleUpdateEmployee(): Xử lý cập nhật thông tin nhân viên.
  + handleDeleteEmployee(): Xử lý xóa nhân viên khỏi hệ thống.
  + validateEmployeeData(): Kiểm tra tính hợp lệ của thông tin nhân viên (trước khi thêm hoặc cập nhật).
- Employee:
  + employeeId: ID của nhân viên.
  + name: Tên nhân viên.
  + employeeType: Loại nhân viên (giờ, lương cố định, hoa hồng).
  + salary: Lương của nhân viên (dành cho nhân viên lương cố định).
  + hourlyRate: Mức lương theo giờ (dành cho nhân viên làm theo giờ).
  + commissionRate: Mức hoa hồng (dành cho nhân viên hoa hồng).
  + status: Trạng thái nhân viên (đã xóa hay không).
  + createEmployee(): Tạo bản ghi nhân viên mới.
  + updateEmployee(): Cập nhật thông tin nhân viên.
  + deleteEmployee(): Đánh dấu nhân viên là đã xóa.
  + getEmployeeById(String employeeId): Truy xuất thông tin nhân viên theo ID.
  + validateData(): Kiểm tra tính hợp lệ của thông tin nhân viên.
### e. Mối quan hệ giữa các lớp
- PayrollAdministratorInterface: Giao tiếp trực tiếp với Quản trị viên tiền lương. Gửi yêu cầu và nhận phản hồi từ MaintainEmployeeController. Hiển thị biểu mẫu và thông báo cho người dùng.
- EmployeeInformationForm: Được PayrollAdministratorInterface gọi để hiển thị biểu mẫu thông tin nhân viên. Gửi thông tin nhân viên đã nhập tới MaintainEmployeeController.
- MaintainEmployeeController: Xử lý các yêu cầu từ PayrollAdministratorInterface (thêm, cập nhật, xóa nhân viên). Tương tác với Employee để thực hiện thao tác trên dữ liệu (thêm, cập nhật, xóa). Cập nhật kết quả và phản hồi lại cho PayrollAdministratorInterface.
- Employee: Là thực thể dữ liệu, lưu trữ thông tin nhân viên. MaintainEmployeeController thao tác trên Employee để thêm, cập nhật hoặc xóa thông tin nhân viên.
### f. Biểu đồ lớp mô tả lớp phân tích
![maintainEmployee](https://www.planttext.com/api/plantuml/png/L90nRW9134Lxdy8Nu0AfM1Q8A2Abo0NCxi1QclMWMI_IdY27e4hAI8Y6YYaezYHp0gwG6KK1KLYodj__XM_XEksKlFQj1LYxNcho0xxJu9srHTsoSAUUrFcLgF4RgWnIXyN3NRGxwmPZLh9nlYLb9ykqP6i6bHDDJVX6B9hcNox_k3K-UoKOKTP7LuPpW08d4opn1L-P72h7otK7ipkCuSYepNYMRJeAIZD-2-vv_14eipLFraUJe-DNXViO3enr32Uq7CDd_nI0gP4wV-4N003__mC0)
## 5. Ca sử dụng Maintain Purchase Order
### a. Các lớp phân tích
- Lớp Boundary:  CommissionedEmployeeInterface, PurchaseOrderForm
- Lớp Controller: MaintainPurchaseOrderController
- Lớp entities: PurchaseOrder
### b. Biểu đồ Sequence
![MaintainPurchaseOrder](https://www.planttext.com/api/plantuml/png/l5IzRjim4Dxv53UcGFe26GBRSf86QDeE6TAHaTcGY4Iw56NKOz6fA39axX8dA0guyDG21QGX0uEy1vyWhv2Z5FzGbJ9MW21GzttVVNT7yg6yxMM6QfEd2Q6nKHeYbQOYouIIRBINZXCrPOoGKvNB4TNJrl2XD4n_e343ca5_ZNsNwvZJZBtL8wRtbKvzV41Y9OrM2HnH8Gs-0IogWmdJ7XmH9eqm3IaV6HBIPWLUxa8VTY3YhhoGO3XLOEmiXgrZRkVfDaIkM8n1SloORJYnl-aBqlUi25a7hbm8cDfv3h4hVkO1tnKprSwFbbdVRpBj7ta6HaYukxoVIU3s2jTRXyDWpPKh_iQRw9WB_BhYrZmP6w3mA-7ABxuSLtw3Kx_88NN5hwuyPB2qz8PNXZjWZSexK8Gc1ghwWz-0JrNw40N-2QE_yhkeGCDbbcFjYXkOkF8pX7rOQrN3ov6ERVmnRi2mEGfxRwybJ8ITIyAIZ0KZwJRu6lMcWPZXJ662JeiTtV3mzi5Cx1KwTELNoI73Xj8DYOesQAamo69lQc9eFIZm6LUh8axyZgtmqcTPaV4qZUff-etxFtlLTFNfsVojxbghypfrLNMQjYkXCQLpVxRWO-wzhyut8JrKyRVW8m000F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
- CommissionedEmployeeInterface:
  + Cho phép nhân viên có hoa hồng chọn thao tác họ muốn thực hiện (thêm, cập nhật, hoặc xóa đơn hàng).
  + Hiển thị thông báo và yêu cầu nhập thông tin liên quan đến đơn hàng (ví dụ: ID đơn hàng, thông tin khách hàng, sản phẩm, v.v.).
  + Hiển thị các thông báo lỗi hoặc xác nhận (ví dụ: đơn hàng không tồn tại, không phải của nhân viên này, hoặc đơn hàng đã đóng).
- PurchaseOrderForm:
  + Hiển thị biểu mẫu để nhân viên nhập thông tin chi tiết về đơn hàng (ví dụ: khách hàng, sản phẩm, địa chỉ thanh toán, ngày mua).
  + Thu thập dữ liệu từ nhân viên và chuyển tiếp cho Controller để xử lý.
-  MaintainPurchaseOrderController:
  + Xử lý các yêu cầu từ CommissionedEmployeeInterface (thêm, cập nhật, xóa đơn hàng).
  + Khi thao tác là Create, yêu cầu PurchaseOrderForm thu thập thông tin đơn hàng từ nhân viên.
  + Kiểm tra tính hợp lệ của thông tin đơn hàng (ví dụ: đảm bảo đơn hàng không bị đóng, là của nhân viên này).
  + Tương tác với PurchaseOrder (lớp thực thể) để tạo, cập nhật, hoặc xóa đơn hàng.
  + Trả về kết quả thành công hoặc lỗi cho CommissionedEmployeeInterface.
- PurchaseOrder:
  + Quản lý và xử lý dữ liệu liên quan đến đơn hàng, bao gồm việc tạo, cập nhật, xóa và truy vấn thông tin.
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- CommissionedEmployeeInterface: 
  + selectedAction: Lưu trữ hành động mà nhân viên chọn (Tạo, Cập nhật, Xóa đơn hàng).
  + employeeId: ID của nhân viên đang thực hiện thao tác.
  + selectAction(): Cho phép nhân viên chọn thao tác (Tạo, Cập nhật, Xóa).
  + displayOrderForm(): Hiển thị biểu mẫu để nhân viên nhập thông tin đơn hàng.
  + displayMessage(String message): Hiển thị thông báo thành công hoặc lỗi cho nhân viên.
  + getEnteredOrderInfo(): Lấy thông tin đơn hàng mà nhân viên đã nhập vào biểu mẫu.
- PurchaseOrderForm: 
  + orderId: ID của đơn hàng cần cập nhật hoặc xóa.
  + customerName: Tên khách hàng.
  + billingAddress: Địa chỉ thanh toán của khách hàng.
  + products: Danh sách các sản phẩm trong đơn hàng.
  + orderDate: Ngày tạo đơn hàng.
  + collectOrderDetails(): Thu thập thông tin chi tiết về đơn hàng từ nhân viên.
  + displayOrderDetails(PurchaseOrder order): Hiển thị chi tiết đơn hàng để nhân viên xem và chỉnh sửa.
  + getOrderDetails(): Trả về thông tin đơn hàng mà nhân viên đã nhập.
- MaintainPurchaseOrderController:  
  + currentAction: Hành động hiện tại mà nhân viên đang thực hiện (Tạo, Cập nhật, Xóa).
  + currentEmployeeId: ID của nhân viên thực hiện thao tác.
  + orderService: Dịch vụ hoặc đối tượng giúp xử lý các thao tác liên quan đến đơn hàng (tạo, cập nhật, xóa).
  + handleCreateOrder(): Xử lý thao tác tạo đơn hàng mới.
  + handleUpdateOrder(): Xử lý thao tác cập nhật thông tin đơn hàng.
  + handleDeleteOrder(): Xử lý thao tác xóa đơn hàng.
  + validateOrderInfo(): Kiểm tra tính hợp lệ của thông tin đơn hàng (đảm bảo thông tin hợp lệ trước khi tạo hoặc cập nhật).
  + getOrderById(): Lấy thông tin đơn hàng từ ID.
  + confirmDeletion(): Xác nhận việc xóa đơn hàng từ nhân viên.
- PurchaseOrder: 
  + orderId: ID của đơn hàng.
  + customerName: Tên khách hàng.
  + customerBillingAddress: Địa chỉ thanh toán của khách hàng.
  + products: Danh sách các sản phẩm trong đơn hàng.
  + orderDate: Ngày tạo đơn hàng.
  + status: Trạng thái đơn hàng (Mở, Đã đóng).
  + commissionedEmployeeId: ID của nhân viên có hoa hồng đã tạo đơn hàng.
  + createOrder(): Tạo đơn hàng mới và lưu vào hệ thống.
  + updateOrder(): Cập nhật thông tin đơn hàng.
  + deleteOrder(): Xóa đơn hàng khỏi hệ thống.
  + getOrderById(String orderId): Lấy thông tin đơn hàng bằng ID.
  + validateOrder(): Kiểm tra tính hợp lệ của đơn hàng (còn mở, là của nhân viên hiện tại, v.v.).
  + closeOrder(): Đóng đơn hàng sau khi hoàn thành giao dịch.
### e. Mối quan hệ giữa các lớp
- CommissionedEmployeeInterface gửi yêu cầu từ nhân viên (chọn thao tác và cung cấp thông tin đơn hàng) đến MaintainPurchaseOrderController, nơi xử lý các thao tác như tạo, cập nhật, và xóa đơn hàng.
- MaintainPurchaseOrderController yêu cầu PurchaseOrderForm hiển thị biểu mẫu cho nhân viên nhập thông tin đơn hàng hoặc hiển thị thông tin đơn hàng cần cập nhật.
- MaintainPurchaseOrderController tương tác với PurchaseOrder để tạo, cập nhật, hoặc xóa đơn hàng trong hệ thống.
- PurchaseOrderForm thu thập thông tin từ nhân viên và cung cấp cho PurchaseOrder để tạo hoặc cập nhật thông tin đơn hàng.
### f. Biểu đồ lớp mô tả lớp phân tích
![MaintainPurchaseOrder](https://www.planttext.com/api/plantuml/png/N8wn3G8n34LxJ-45ReUxou54WM25a1WHAR6HunGt6mKZiG842WJ5ro_UqzT_tEvZDQ_MIWOuIUFeTKKdfQHQap35JRbcMObsRAHd7mXznUdh7fk6Ywzqq4Yw5IsTpn24JINZtYUsLtuqzu6PjCiEY2tPtrGd2y24mu0EONutk5uB0ep4iPz-0W00__y30000)
## 6. Ca sử dụng Run Payroll
### a. Các lớp phân tích
- Lớp Boundary:  PayrollInterface, BankSystemInterface
- Lớp Controller: RunPayrollController
- Lớp entities: Employee, Payroll
### b. Biểu đồ Sequence
![RunPayroll](https://www.planttext.com/api/plantuml/png/X9F1Jjmm48RlVefvWQht7YeskwlI6oezqAF9fciBxnWvOuJFFN3Wn1kGLbLLf1Kz9weukE8z_0HzXOx3Xi22IYwHnj_y_--Pv6ztirEJTEHNHWXPadMm9uEpnamMAusw9YUvACIXzRYGBWp7xv4gzrcM5SWQ9kDn8V5eFzHKhHuHXIWj4ZV21uyRYUbTnLGk4rDH8MaAC5yT6nkglcqs53SjkJONuhc8yEejJE0D5Acz9lXpaTeV7agLsYR0OMg_uHBCxQ_R1fTYajafiv_Y5JCzUPgwDPZuUvkTPdR6x4Vd0vpwr7udMAJk6enEtPa7LF4hmecELtW7ppFCjdPRQdul5TUeW6niS3ZafFQfLBxFBjjyGI2LkdCWny9CaugDtjONqX3igOrWRlXPyakENl6IVNpe1O-KpUq2-EdD2ZPxnrFGiDJIvZkUbmfmcJEfUCa66Is6sHt4fkJ4gLtZmmPHcRfwCSMnqgczyKFqrniTac7CCxkVunRDtyH2Z8lPjHmEg5_CSylB-pZuttQVJFan16eq46A7pVFFyWy00F__0m00)
### c. Nhiệm vụ của từng lớp phân tích:
- PayrollInterface: Cung cấp giao diện để hệ thống hiển thị trạng thái và kết quả khi chạy bảng lương. Đây là lớp mà người dùng (chẳng hạn như Payroll Administrator) tương tác để xem báo cáo, xác nhận thanh toán, và thực hiện các thao tác liên quan đến bảng lương.
- BankSystemInterface: Cung cấp giao diện để kết nối và truyền dữ liệu đến hệ thống ngân hàng để xử lý thanh toán qua chuyển khoản trực tiếp.
-  RunPayrollController: lớp điều khiển chính trong ca sử dụng Run Payroll, chịu trách nhiệm xử lý các bước như tính toán lương, in phiếu lương, gửi giao dịch ngân hàng, v.v.
- Employee: Đại diện cho một nhân viên trong hệ thống, bao gồm các thông tin cá nhân và thông tin thanh toán.
- Payroll: Lớp đại diện cho bảng lương, bao gồm thông tin liên quan đến việc tính toán lương của tất cả nhân viên trong mỗi chu kỳ bảng lương.
### d. Một số thuộc tính và phương thức của các lớp phân tích:
- PayrollInterface:
  + payrollStatus: Trạng thái của việc chạy bảng lương (hoàn thành, lỗi, đang chờ).
  + employeeList: Danh sách nhân viên đã nhận thanh toán.
  + displayPayrollStatus(): Hiển thị trạng thái bảng lương.
  + displayEmployeePaymentDetails(): Hiển thị chi tiết thanh toán của từng nhân viên.
-BankSystemInterface:
  + transactionStatus: Trạng thái giao dịch với hệ thống ngân hàng.
  + sendBankTransaction(): Gửi giao dịch ngân hàng.
  + retryBankTransaction(): Thử lại giao dịch nếu hệ thống ngân hàng không sẵn sàng.
- RunPayrollController:
  + payrollDate: Ngày bảng lương được chạy.
  + employeeList: Danh sách nhân viên cần được thanh toán.
  + calculatePay(): Tính toán lương cho từng nhân viên dựa trên thông tin từ thẻ chấm công, đơn hàng và thông tin nhân viên.
  + processPayment(): Xử lý thanh toán cho nhân viên, bao gồm in phiếu lương hoặc gửi giao dịch ngân hàng.
  + checkBankSystemStatus(): Kiểm tra trạng thái hệ thống ngân hàng và xử lý nếu hệ thống không khả dụng.
  + deleteEmployee(): Xóa nhân viên đã bị đánh dấu xóa sau khi bảng lương đã được xử lý.
- Employee:
  + employeeId: Mã số nhân viên.
  + name: Tên nhân viên.
  + salary: Lương cơ bản của nhân viên (nếu là nhân viên lương cố định).
  + hourlyRate: Mức lương theo giờ (nếu là nhân viên lương theo giờ).
  + benefits: Các phúc lợi (Bảo hiểm, nghỉ phép, v.v.).
  + paymentMethod: Phương thức thanh toán (chuyển khoản, lấy phiếu lương, v.v.).
  + status: Trạng thái của nhân viên (đang làm việc, đã nghỉ việc, v.v.).\
  + calculatePay(): Tính toán lương cho nhân viên.
  + generatePaycheck(): Tạo phiếu lương cho nhân viên.
  + sendPayment(): Gửi thanh toán cho nhân viên qua chuyển khoản ngân hàng.
- Payroll:
  + payrollDate: Ngày chạy bảng lương.
  + employeePayments: Danh sách các khoản thanh toán cho nhân viên.
  + runPayroll(): Chạy bảng lương cho tất cả nhân viên.
  + generateReports(): Tạo báo cáo về bảng lương.
  + processPayments(): Xử lý thanh toán cho nhân viên.
### e. Mối quan hệ giữa các lớp
- PayrollInterface (Giao diện với người dùng) giao tiếp với RunPayrollController để yêu cầu xử lý bảng lương.
- RunPayrollController truy xuất và tính toán dữ liệu từ Employee và tạo đối tượng Payroll.
- RunPayrollController gửi giao dịch đến BankSystemInterface nếu phương thức thanh toán là chuyển khoản.
- RunPayrollController tạo phiếu lương nếu phương thức thanh toán là phiếu lương/nhận tay.
- PayrollInterface hiển thị kết quả cho người dùng sau khi bảng lương hoàn tất.
### f. Biểu đồ lớp mô tả lớp phân tích
![RunPayroll](https://www.planttext.com/api/plantuml/png/L8x13S8m34Nldi8BT8SsQG_S44nWMYCX4WSbpY6pzS18h413Wn2d9xt_l-NN-koJKjJi7S0bP5ae5ZnIYS6vWoZ7AysCb73unORaVYv9sVyr3Cn1T1lYAKixONVZEDQ61HQzQS79Frme_9cDNzacrKq00tOTMWJJQ2l77LlSioprwJS0003__mC0)

## Code Java mô phỏng ca sử dụng Maintain Timecard
    package Demo.MaintainTimecard;
    public class DemoMaintainTimecard {
       public static void main(String[] args){
       
          EmployeeUI employeeUI = new EmployeeUI();
          employeeUI.showTimecard(timecard);
          employeeUI.selectChargeNumber();
          employeeUI.displayError(messageStr);
          employeeUI.acknowledgeSubmission();

          TimeCardController tc = new TimeCardController();
          tc.retrieveOrCreateTimecard(employee: Employee);
          tc.getChargeNumbers();
          tc.enterHours(date, hours, chargeNumber);
          tc.validateHours(timecard);
          tc.
       }
    }

    class EmployeeUI {
       //View Timecard
       public void showTimecard(timecard: Timecard) {
       }
       //Select chargeNumber
       public void selectChargeNumber(){
       }
       //Show error message
       public void displayError(message: String){
       }
       //Request confirm 
       public boolean confirmSubmission(){
       }
       //Confirm submit Timecard and no edit
       public void acknowledgeSubmission(){
       }    
    }

    class TimeCardController {
       // Get currently TimeCard of employee or create new TimeCard 
       public void retrieveOrCreateTimecard(employee: Employee){
       }
       // Get list NumberCharge from DB
       public void getChargeNumbers(){
       }
       // Employee can enter hours work
       public void enterHours(date: Date, hours: Double, chargeNumber: String){
       }
       // Check valid hours work
       public void validateHours(timecard: Timecard){
       }
       // Submit TimeCard
       public void submitTimecard(){
       }
       // Handle error
       public void handleDatabaseError(){
       }
    }

    class Employee{
       private int employeeID;
       private date startDate;
       private List<TimecardEntry> entries;
       private string status;
       private date submitedDate;
       // Add a new entry for hours worked.
       public void addEntry(date: Date, hours: Double, chargeNumber: String){
       }
       // Mark submited Timecard
       public void markAsSubmitted(date: Date){
       }
       // Check if the timesheet is editable.
       public boolean isEditable(){
       }

    class TimeCard {
       private int employeeID;
       private string name;
       private double maxHoursPerWeek; 
       private boolean isHourly;
       //Check if employee can extra hours work
       public boolean canWorkOvertime(){
       }
       //Get employee info
       public string getEmployeeDetails(){
       }
    }       
    }
