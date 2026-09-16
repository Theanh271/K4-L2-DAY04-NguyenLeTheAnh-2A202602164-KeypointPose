# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 14.41 khớp có v > 0 mỗi người
- Tổng: v=2 312 | v=1 106 | v=0 75

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 20 | 3 | 6 | 10% |
| 1 | left_eye | 19 | 6 | 4 | 21% |
| 2 | right_eye | 18 | 6 | 5 | 21% |
| 3 | left_ear | 10 | 13 | 6 | 45% |
| 4 | right_ear | 12 | 12 | 5 | 41% |
| 5 | left_shoulder | 25 | 4 | 0 | 14% |
| 6 | right_shoulder | 27 | 2 | 0 | 7% |
| 7 | left_elbow | 22 | 5 | 2 | 17% |
| 8 | right_elbow | 24 | 3 | 2 | 10% |
| 9 | left_wrist | 17 | 7 | 5 | 24% |
| 10 | right_wrist | 19 | 6 | 4 | 21% |
| 11 | left_hip | 19 | 9 | 1 | 31% |
| 12 | right_hip | 20 | 8 | 1 | 28% |
| 13 | left_knee | 18 | 4 | 7 | 14% |
| 14 | right_knee | 19 | 4 | 6 | 14% |
| 15 | left_ankle | 12 | 7 | 10 | 24% |
| 16 | right_ankle | 11 | 7 | 11 | 24% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
