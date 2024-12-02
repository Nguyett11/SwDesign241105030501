# Lab5 Payroll System Subsystem Design 

## 1. Phân phối hành vi của hệ thống con đến các thành phần:
### Hệ thống được chia thành 4 hệ thống con chính, mỗi hệ thống con đảm nhiệm một chức năng cụ thể:
#### a) Payroll Processing Subsystem (Hệ thống xử lý lương)
- Chức năng chính: Tính toán và thực hiện thanh toán lương cho nhân viên.
- Thành phần chính:
  + PayrollController: Quản lý logic nghiệp vụ liên quan đến tính toán lương.
  + BankSystemProxy: Kết nối với hệ thống ngân hàng để thực hiện chuyển khoản lương.
  + PrinterServiceProxy: Hỗ trợ in phiếu lương.
  + PayrollDatabase: Lưu trữ thông tin chi tiết về bảng lương.
#### b) Timecard Subsystem (Hệ thống quản lý thẻ chấm công)
- Chức năng chính: Quản lý giờ làm việc của nhân viên và trạng thái thẻ chấm công.
- Thành phần chính:
  + TimecardController: Xử lý logic nghiệp vụ liên quan đến thông tin chấm công.
  + TimecardForm: Giao diện nhập liệu về giờ làm việc và trạng thái thẻ.
  + ProjectManagementDatabase: Hỗ trợ truy xuất danh sách mã dự án để liên kết thông tin chấm công.
#### c) Employee Management Subsystem (Hệ thống quản lý nhân viên)
- Chức năng chính: Quản lý thông tin cá nhân và trạng thái làm việc của nhân viên.
- Thành phần chính:
  + Employee: Lớp thực thể đại diện cho thông tin nhân viên.
  + EmployeeDatabase: Cơ sở dữ liệu lưu trữ thông tin nhân viên.
#### d) Scheduler Subsystem (Hệ thống lập lịch)
- Chức năng chính: Theo dõi thời gian và tự động kích hoạt quy trình tính lương theo lịch định sẵn.
- Thành phần chính:
  + SystemClock: Theo dõi thời gian hệ thống và kích hoạt quy trình “Run Payroll” vào thời điểm đã định.
    
## 2. Mô tả chi tiết các hệ thống con:
- Timecard Subsystem
  + Quản lý thông tin giờ làm việc của nhân viên.
  + Liên kết với cơ sở dữ liệu quản lý dự án để lấy danh sách mã dự án.
  + Cập nhật trạng thái thẻ chấm công.
- Payroll Processing Subsystem
  + Tính toán bảng lương dựa trên giờ làm việc và trạng thái của nhân viên.
  + Thực hiện thanh toán qua ngân hàng hoặc in phiếu lương.
  + Lưu trữ thông tin về lương trong cơ sở dữ liệu.
- Employee Management Subsystem
  + Lưu trữ và quản lý thông tin nhân viên.
  + Cập nhật trạng thái nhân viên (đang làm việc, nghỉ việc, bị xóa).
  + Cung cấp thông tin nhân viên cho các hệ thống con khác khi cần.
- Scheduler Subsystem
  + Theo dõi thời gian và tự động kích hoạt quá trình tính lương vào thời gian được định trước.

## 3. Mô tả mối quan hệ phụ thuộc giữa các hệ thống con:
- Timecard Subsystem: Phụ thuộc vào Employee Management Subsystem để truy xuất thông tin nhân viên.
- Payroll Processing Subsystem:
  + Phụ thuộc vào Employee Management Subsystem để lấy danh sách nhân viên.
  + Phụ thuộc vào Timecard Subsystem để lấy thông tin giờ làm việc của từng nhân viên.
- Scheduler Subsystem: Hoạt động độc lập nhưng đóng vai trò kích hoạt Payroll Processing Subsystem theo lịch định sẵn.

## 4. Kiểm tra chất lượng hệ thống:
- Phân chia hợp lý: Các hệ thống con được xác định với trách nhiệm rõ ràng, không chồng chéo.
- Mối quan hệ phụ thuộc rõ ràng: Mối quan hệ giữa các hệ thống con được xác định và mô tả chi tiết, đảm bảo tính minh bạch.
- Khả năng mở rộng: Thiết kế linh hoạt cho phép mở rộng hoặc thay đổi từng hệ thống con mà không gây ảnh hưởng lớn đến hệ thống tổng thể.


### Component Diagram
![Diagram](https://www.planttext.com/api/plantuml/png/b9DBJiCm48RtFiKe6rQz00jKqT8TKgLqXx9mdI4ryICQEq24E1aBZiGLS5vAI4AaBZsU-VxVC-EVh--jyvnygHLpkJH0rY4hkCXvXX2Tf4R1AOMuFBlAUTGHV320f_vYPuqdgnHICWuVBEacS2JxWi8_SXDu6etVSy_Ft672FjcWS-HLJO6GBj0vQRAPOfSo4Rpd9e-Rj53wNdMQqdYa6EbL2Xp5MyAoWmTTA5iXmc1rPg7FISQ7PLmiBfYMmUKCqhhTAIlofkG6zbYWIT48YOwnfTR2PdEte0Yt41tG1oa7sFjFmsqKCFD-NKL1pwLoqV-S9PiZqfkb72wsf3N6T7ere5k1W2XuLOzX3R0qwXOIuWt1ALci4YPBKLV7tbAhtoobDC-sxkXuSd-A9oquaSmof05Gj4yAZ6qOTFtLVW400F__0m00)
