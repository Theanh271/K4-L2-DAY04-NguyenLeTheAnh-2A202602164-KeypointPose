# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Nguyễn Lê Thế Anh     Ngày: 16/9/20262026


## 1. Nhãn của tôi

| Chỉ số                       |        Giá trị |
| ---------------------------- | -------------: |
| Số ảnh đã gán                |             20 |
| Số skeleton                  |             29 |
| v=2 / v=1 / v=0              | 312 / 106 / 75 |
| Thời gian trung bình mỗi ảnh |            ... |


Ba khớp có %v=1 cao nhất:

1. left_ear – 45%
2. right_ear – 41%
3. left_hip – 31%

Đây cũng là các khớp khá khó gán vì thường bị tóc, quần áo hoặc cơ thể che. Tai khó xác định vị trí khi bị tóc che, còn hông thường không nhìn rõ do quần áo. Tuy nhiên, “hay bị che” không hoàn toàn giống “khó xác định vị trí giải phẫu”.

## 2. Chấm với gold

Chỉ số	Trước rework	Sau rework
OKS trung bình	0.937	0.944
OKS@0.50	1.000	1.000
OKS@0.75	1.000	1.000
Lỗi dao_trai_phai	0	0
Lỗi nham_nguoi	0	0
Lỗi xoa_khop_bi_che	4	0

Tôi đã sửa gì giữa hai lần chạy:

train_01.jpg – người #1 – left_wrist – đặt lại điểm bị che và chuyển sang v=1.
train_03.jpg – người #1 – right_wrist – đặt lại điểm bị che và chuyển sang v=1.
train_08.jpg – người #1 – left_knee – đặt lại điểm bị che và chuyển sang v=1.
train_16.jpg – người #2 – nose – đặt lại điểm bị che và chuyển sang v=1.

Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?
train_13.jpg, người #2. Đây là lỗi xác định trái/phải theo phía của ảnh thay vì theo cơ thể người.

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:
Nếu khớp vẫn nằm trong ảnh nhưng bị che và có thể ước lượng vị trí thì đặt điểm và chọn v=1.
Nếu khớp nằm ngoài khung ảnh và không còn bằng chứng về vị trí thì chọn v=0, không đặt tọa độ.


## 4. Model

Chỉ số	yolo26n-pose gốc	Sau fine-tune	Chênh
pose_mAP50	0.8450	0.8450	0.0000
pose_mAP50-95	0.6853	0.6908	+0.0055
pose_precision	0.9734	0.9792	+0.0058
pose_recall	0.8462	0.8462	0.0000
box_mAP50-95	0.8119	0.8041	-0.0078
Trả lời năm câu hỏi ở cuối notebook

1. pose_mAP50-95 thay đổi bao nhiêu?
Tăng 0.0055, từ 0.6853 lên 0.6908. Vì vậy 20 ảnh giúp model cải thiện nhẹ khả năng xác định vị trí keypoint. Chưa có bằng chứng để kết luận 20 ảnh làm hỏng điều gì.

2. box_mAP và pose_mAP chênh nhau bao nhiêu?
Sau fine-tune, box_mAP50-95 là 0.8041 còn pose_mAP50-95 là 0.6908, chênh 0.1133. Kết quả cho thấy việc tìm box người đạt điểm cao hơn việc xác định chính xác từng khớp.

3. Một ảnh test model đoán sai:
test_04.jpg – lỗi lệch nhẹ. Một số keypoint của người được dự đoán hơi lệch so với vị trí trên ảnh, nhưng model vẫn xác định đúng người.

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model?
test_13.jpg có OKS thấp nhất. Qua quan sát, lỗi chủ yếu nằm ở một số keypoint khó xác định do bị che hoặc tư thế của người. Tôi dựa vào vị trí các khớp trên ảnh và so sánh với kết quả dự đoán để đánh giá.

5. Ảnh bạn gán tệ nhất có cũng là ảnh model đoán tệ nhất không?
Có thể không trùng nhau. Lỗi gán nhãn của tôi chủ yếu liên quan đến việc xác định visibility và vị trí khớp, còn model có thể gặp khó khăn ở các tư thế hoặc vùng bị che khác. Điều này cho thấy những ảnh có người bị che hoặc tư thế khó cần được kiểm tra kỹ hơn.

## 5. Một rule evidence bạn đã dùng

train_01.jpg – người #1 – left_wrist. Cổ tay bị vật/cơ thể che nhưng phần cánh tay và vị trí khớp vẫn có thể quan sát để ước lượng. Khớp vẫn nằm trong khung ảnh nên tôi đặt keypoint tại vị trí ước lượng. Vì bị che nhưng vẫn có bằng chứng vị trí nên chọn v=1, không chọn v=0.