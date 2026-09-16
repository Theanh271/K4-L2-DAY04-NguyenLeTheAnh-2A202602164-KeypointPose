# Mini guideline - nhóm: ______  |  người gán: ______  |  ngày: ______

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

2. Luật của nhóm bạn
| Tình huống                                        | Luật nhóm bạn chọn                                                                             | Vì sao                                                                   |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| Hông của người mặc quần áo dài                    | Ước lượng vị trí hông theo cấu trúc cơ thể và đặt điểm, nếu còn trong ảnh thì `v=1` khi bị che | Quần áo dài có thể che vị trí hông nhưng vẫn có thể suy ra từ thân người |
| Tai bị tóc hoặc mũ bảo hiểm che một phần          | Vẫn đặt điểm tại vị trí tai ước lượng và chọn `v=1`                                            | Tai vẫn nằm trong khung nhưng bị che một phần                            |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Khớp nằm ngoài ảnh chọn `v=0` và không đặt điểm                                                | Không có bằng chứng về vị trí khớp ngoài khung                           |
| Cổ tay nằm sau tay lái / sau thân mình            | Nếu còn trong ảnh và suy ra được vị trí thì đặt điểm và chọn `v=1`                             | Khớp bị che nhưng vẫn có bằng chứng từ cánh tay và tư thế                |
| Hai người chồng lên nhau                          | Gán riêng 17 điểm cho từng người, không lấy điểm của người này cho người kia                   | Tránh nhầm người và nối sai các khớp                                     |
| Người nhỏ đến mức nào thì không gán nữa           | **...**                                                                                        | Chưa có quy định cụ thể của nhóm trong dữ liệu đã cung cấp               |


3. Ba ca mơ hồ đã gặp
Ca 1 - ảnh train_01, người thứ 1, khớp left_wrist
Mơ hồ ở chỗ nào: Cổ tay bị che nên không nhìn rõ trực tiếp.
Bạn quyết thế nào: Đặt điểm ở vị trí ước lượng và chọn v=1.
Vì sao: Cổ tay vẫn ở trong khung và có thể suy ra từ phần cánh tay.
Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể học rằng khớp bị che thì không cần dự đoán điểm.
Ca 2 - ảnh train_03, người thứ 1, khớp right_wrist
Mơ hồ ở chỗ nào: Cổ tay bị che bởi phần cơ thể/vật phía trước.
Bạn quyết thế nào: Đặt điểm theo vị trí ước lượng và chọn v=1.
Vì sao: Vẫn có bằng chứng từ phần cánh tay và khớp vẫn nằm trong ảnh.
Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể học sai rằng cổ tay bị che là v=0.
Ca 3 - ảnh train_13, người thứ 2, khớp left_shoulder/right_shoulder
Mơ hồ ở chỗ nào: Khó xác định trái/phải khi nhìn người trong ảnh.
Bạn quyết thế nào: Xác định trái/phải theo cơ thể của người, không theo phía của ảnh.
Vì sao: Quy tắc COCO yêu cầu left/right theo cơ thể người.
Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể học sai vị trí trái/phải của keypoint và dễ bị đảo hai bên.
4. Sau khi so visibility report với bạn cùng nhóm
Khớp lệch %v=1 nhiều nhất: ... (bạn ...% / họ ...%)
Nguyên nhân là: ...
Luật mới bổ sung vào mục 2 sau khi thống nhất:
Nếu khớp vẫn nằm trong ảnh nhưng bị che và có thể suy ra vị trí thì phải đặt điểm và chọn v=1; chỉ chọn v=0 khi khớp đã ra ngoài khung ảnh và không còn bằng chứng về vị trí.