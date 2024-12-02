# Coding conventions
***Hướng dẫn này cung cấp cách tổ chức mã và phong cách mã cho các dự án sử dụng Kotlin, giúp mã dễ đọc và duy trì.***

## Configure style in IDE
- Hai IDE phổ biến nhất cho Kotlin là IntelliJ IDEA và Android Studio, cung cấp hỗ trợ mạnh mẽ cho việc định dạng mã. Bạn có thể thiết lập chúng để tự động căn chỉnh mã theo phong cách mã đã quy định, giúp đảm bảo sự nhất quán và dễ đọc cho mã nguồn.
- Để áp dụng hướng dẫn phong cách mã cho Kotlin trong IntelliJ IDEA hoặc Android Studio, bạn có thể thực hiện như sau:

    1. Vào Settings/Preferences > Editor > Code Style > Kotlin.
    2. Nhấn vào Set from....
    3. Chọn Kotlin style guide để IDE tự động định dạng mã theo phong cách chuẩn của Kotlin.
    4. Điều này giúp giữ cho mã của bạn nhất quán và tuân theo các quy ước mã hóa của Kotlin.

## Source code organization﻿
**Directory structure**

- Trong các dự án Kotlin thuần túy, cấu trúc thư mục nên theo cấu trúc gói (package), nhưng bỏ qua gói gốc chung. Ví dụ, nếu mã nằm trong gói org.example.kotlin và các gói con, các tệp thuộc gói này nên đặt trực tiếp dưới thư mục nguồn. Các tệp trong org.example.kotlin.network.socket sẽ đặt ở thư mục con network/socket của thư mục nguồn.

- Điều này giúp giữ cho dự án có cấu trúc rõ ràng và dễ quản lý.

**Source file names**
- Trong dự án Kotlin, nếu một tệp chứa một lớp hoặc interface duy nhất, tên tệp nên trùng với tên của lớp đó và thêm đuôi .kt. Nếu tệp có nhiều lớp hoặc chỉ có các khai báo cấp cao, chọn tên mô tả nội dung tệp, dùng CamelCase (ví dụ: ProcessDeclarations.kt).


## Naming rules
- Tên lớp và đối tượng: Dùng PascalCase (viết hoa chữ cái đầu mỗi từ), ví dụ: MainActivity, UserManager.
- Tên hàm và biến: Dùng camelCase (viết thường chữ cái đầu tiên, viết hoa chữ cái đầu của từ tiếp theo), ví dụ: fetchData(), userName.

- Hằng số: Viết hoa tất cả, phân cách từ bằng dấu gạch dưới, ví dụ: MAX_USER_LIMIT, API_KEY.

## Formatting

- Thụt lề: Sử dụng khoảng trắng, không dùng tab.
- Dấu ngoặc nhọn: Đặt dấu ngoặc mở ở cuối dòng khai báo, dấu ngoặc đóng ở dòng mới, ngang với khai báo ban đầu.

```kt
if (elements != null) {
    for (element in elements) {
        // ...
    }
}

```
- Các funtion, logic riêng nên cách nhau một hàng cho dễ nhìn.
- Loại bỏ dấu ***,*** ở các phần tử cuối cùng trong list.