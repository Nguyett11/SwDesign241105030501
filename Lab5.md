# Lab5 Payroll System Subsystem Design
## 1. Distribute subsystem behavior to subsystem elements:
Hệ thống được chia thành 4 hệ thống con chính, mỗi hệ thống con đảm nhiệm các chức năng cụ thể:

**a) Payroll Processing Subsystem**
- Chức năng chính: Tính toán và thực hiện thanh toán lương.
- Thành phần chính:
  - `PayrollController`: Quản lý logic nghiệp vụ liên quan đến tính toán lương.
  - `BankSystemProxy`: Kết nối với ngân hàng để chuyển khoản lương.
  - `PrinterServiceProxy`: In phiếu lương.
  - `PayrollDatabase`: Lưu trữ thông tin lương.
    
**b) Timecard Subsystem**
- Chức năng chính: Quản lý giờ làm việc và trạng thái thẻ chấm công.
- Thành phần chính:
  - `TimecardController`: Xử lý logic nghiệp vụ liên quan đến thẻ chấm công.
  - `TimecardForm`: Giao diện nhập liệu giờ làm việc và trạng thái thẻ.
  - `ProjectManagementDatabase`: Lấy danh sách mã dự án.
    

**c) Employee Management Subsystem**
- Chức năng chính: Quản lý thông tin nhân viên và trạng thái (đang làm việc, bị xóa, nghỉ việc).
- Thành phần chính:
  - `Employee`: Thực thể lưu trữ thông tin nhân viên.
  - `EmployeeDatabase`: Cơ sở dữ liệu nhân viên.
    
**d) Scheduler Subsystem**
- Chức năng chính: Theo dõi thời gian và kích hoạt quy trình tính lương theo lịch.
- Thành phần chính:
  - `SystemClock`: Theo dõi thời gian và kích hoạt quy trình Run Payroll theo thời gian định trước.

## 2. Document subsystem elements
Mô tả chi tiết về các hệ thống con:

### Timecard Subsystem
- Quản lý thông tin giờ làm việc của nhân viên.
- Lấy danh sách mã dự án từ cơ sở dữ liệu.
- Cập nhật trạng thái thẻ chấm công.
### Payroll Processing Subsystem
- Xử lý tính toán lương cho từng nhân viên dựa trên giờ làm việc và trạng thái.
- Thực hiện thanh toán qua ngân hàng hoặc in phiếu lương.
- Lưu thông tin lương vào cơ sở dữ liệu.
### Employee Management Subsystem
- Lưu trữ thông tin nhân viên.
- Cập nhật trạng thái nhân viên (đang làm việc hoặc bị xóa).
- Cung cấp thông tin cho các hệ thống con khác.
### Scheduler Subsystem
- Theo dõi thời gian và kích hoạt quy trình tính lương tự động vào thời gian được định trước.

## 3. Describe subsystem dependencies
Mối quan hệ phụ thuộc giữa các hệ thống con:
- Timecard Subsystem phụ thuộc vào Employee Management Subsystem để lấy thông tin nhân viên.
- Payroll Processing Subsystem phụ thuộc vào:
  - Employee Management Subsystem để lấy danh sách nhân viên.
  - Timecard Subsystem để lấy thông tin giờ làm việc.
- Scheduler Subsystem không phụ thuộc vào các hệ thống con khác nhưng kích hoạt Payroll Processing Subsystem.

## 4. Checkpoints
- **Phân chia hợp lý**: Mỗi hệ thống con có trách nhiệm riêng biệt, với các thành phần được phân bổ rõ ràng và logic.
- **Phụ thuộc rõ ràng**: Mối quan hệ giữa các hệ thống con được thể hiện rõ qua sơ đồ và các phụ thuộc cụ thể.
- **Tính mở rộng**: Các hệ thống con có thể mở rộng hoặc thay đổi mà không ảnh hưởng đến toàn bộ hệ thống.


### Component Diagram
![Diagram](https://www.planttext.com/api/plantuml/png/b9DBJiCm48RtFiKe6rQz00jKqT8TKgLqXx9mdI4ryICQEq24E1aBZiGLS5vAI4AaBZsU-VxVC-EVh--jyvnygHLpkJH0rY4hkCXvXX2Tf4R1AOMuFBlAUTGHV320f_vYPuqdgnHICWuVBEacS2JxWi8_SXDu6etVSy_Ft672FjcWS-HLJO6GBj0vQRAPOfSo4Rpd9e-Rj53wNdMQqdYa6EbL2Xp5MyAoWmTTA5iXmc1rPg7FISQ7PLmiBfYMmUKCqhhTAIlofkG6zbYWIT48YOwnfTR2PdEte0Yt41tG1oa7sFjFmsqKCFD-NKL1pwLoqV-S9PiZqfkb72wsf3N6T7ere5k1W2XuLOzX3R0qwXOIuWt1ALci4YPBKLV7tbAhtoobDC-sxkXuSd-A9oquaSmof05Gj4yAZ6qOTFtLVW400F__0m00)
