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
