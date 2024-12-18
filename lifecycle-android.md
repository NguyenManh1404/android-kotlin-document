# Lifecycle Android

Link: https://developer.android.com/codelabs/basic-android-kotlin-training-activity-lifecycle?hl=vi

## Vòng đời của một Activity

- Activity là một thành phần quan trọng trong Android, chịu trách nhiệm hiển thị giao diện và tương tác với người dùng. Một Activity trải qua các trạng thái sau:
- Vòng đời hoạt động là một tập hợp các trạng thái mà qua đó một hoạt động di chuyển. Vòng đời hoạt động bắt đầu khi hoạt động được tạo lần đầu tiên và kết thúc khi hoạt động bị huỷ.
- Khi người dùng di chuyển giữa các hoạt động, bên trong và bên ngoài ứng dụng, mỗi hoạt động sẽ di chuyển giữa các trạng thái trong vòng đời hoạt động.
- Mỗi trạng thái trong vòng đời hoạt động đều có một phương thức gọi lại tương ứng mà bạn có thể ghi đè trong lớp Activity. Tập hợp cốt lõi các phương thức vòng đời là: onCreate()onStart()onPause()onRestart()onResume()onStop()onDestroy()
- Để thêm hành vi xảy ra khi hoạt động chuyển đổi sang trạng thái vòng đời, ghi đè phương thức gọi lại của trạng thái.

- Các trạng thái chính

  - Created: Activity được tạo ra.
  - Started: Activity hiển thị lên màn hình nhưng chưa tương tác.
  - Resumed: Activity ở trạng thái foreground (trước màn hình) và sẵn sàng nhận tương tác.
  - Paused: Activity bị che một phần, không còn nhận tương tác trực tiếp.
  - Stopped: Activity bị che toàn bộ, không còn hiển thị lên màn hình.
  - Destroyed: Activity bị phá hủy, giải phóng tài nguyên.

- Sơ đồ vòng đời
  ![Alt text](image/activity_lifecycle.png)

- **Các phương thức vòng đời:**

  1. onCreate()

  - Gọi khi Activity được khởi tạo lần đầu.
  - Dùng để thiết lập layout, khởi tạo các thành phần, binding dữ liệu, hoặc khôi phục trạng thái nếu Activity bị xoá trước đó.

  2. onStart():

  - Gọi khi Activity sắp hiển thị trên màn hình.
  - Activity ở trạng thái visible nhưng chưa nhận tương tác.

  3. onResume():

  - Gọi khi Activity sẵn sàng tương tác với người dùng.
  - Thường được sử dụng để khởi động animation hoặc cập nhật giao diện.

  4. onPause():

  - Gọi khi Activity bị che bởi một Activity khác (ví dụ: popup, cuộc gọi).
  - Dùng để tạm dừng các tài nguyên không cần thiết (âm thanh, video...).

  5. onStop():

  - Gọi khi Activity bị che hoàn toàn hoặc chuyển về background.
  - Dùng để lưu dữ liệu hoặc giải phóng tài nguyên nặng.

  6. onRestart():

  - Gọi khi Activity được khởi động lại từ trạng thái Stopped.

  7. onDestroy():

  - Gọi khi Activity bị phá huỷ hoàn toàn.
  - Dùng để giải phóng tài nguyên (hủy các callback, thread...).
