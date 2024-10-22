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
     ![UMLPackage](https://www.planttext.com/api/plantuml/png/h98zRiCm38LtdO8Ny0Ko56cS5WcGmMYH0n0oOmZHZqlIWr3qP1rwf5wXYeiwHfoncWI-nu_YWxu_lzQYo3e4RuoSNGHEGiQeKq_Ge3rZHm8Lr1v5OEkmOmp6zByAD4n2KL5TYWVCn03l1i2ExgCGxwCIdz3ILDrXR3t92xqD9FgSE9YFAt0pY8iaSaYTimlYAthaNACT_3Xo4cecL7eAlK-PIER4BIe-MdjX_XTkWq9Bc2QUMlRnb2QbmSp9-vsJOidpSYZPZTOoO1bbLJtSosC5BVKKMoWFlYDVkcvtdhVSQd_-wr9pTpdhSYt_umS00F__0m00)

## 2. Cơ chế phân tích
###  Danh sách các cơ chế phân tích trong hệ thống Payroll:
###  a. Cơ chế xác thực và phân quyền: 
     - Hệ thống Payroll lưu trữ thông tin nhạy cảm, bao gồm thông tin cá nhân và bảng lương của nhân viên. 
     - Do đó, cần đảm bảo rằng chỉ những người dùng được ủy quyền (như quản lý, nhân viên phòng nhân sự, và nhân viên kế toán) mới có thể truy cập vào các phần dữ liệu hoặc thực hiện các hành động nhất định.
###  b. Cơ chế quản lý dữ liệu nhân viên
     - Hệ thống cần quản lý toàn bộ thông tin liên quan đến nhân viên như hợp đồng lao động, giờ làm việc, chế độ phúc lợi và thông tin ngân hàng, thông tin này thay đổi theo thời gian (lương, thăng chức, điều chỉnh hợp đồng). 
     - Do đó cần một cơ chế để theo dõi và cập nhật dữ liệu.
## 3. Phân tích ca sử dụng Select Payment

## 4. Phân tích ca sử dụng Maintain Timecard

## 5. Hợp nhất kết quả phân tích
