# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Bình Anh              Mã học viên: 2A2026004063
Phiên bản CVAT (Help → About): 2.7
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 04:09 UTC (11:09 giờ VN)    Số lần nộp lại sau Rework: 0

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng| `lane`, `road_curb` (polyline); `crosswalk`, `drivable` (polygon); `traffic_light`, `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng | Đủ các attribute theo Road v1.0 (`position`, `style`, `color`, `kind`, `area_type`, `type`, `facing`, `group`, `edge_zone`) |
| 4 tag ảnh | Đúng | Đủ `camera`, `timeofday`, `weather`, `source` trên cả 12 ảnh `front` và 8 ảnh `fisheye` |

Cách kết thúc polyline trên bản CVAT này: Nhấn phím `N` hoặc click chuột phải / hoàn tất thao tác vẽ polyline trên CVAT.
Cách đặt tag ảnh trên bản CVAT này: Gán 4 tag (`camera`, `timeofday`, `weather`, `source`) trực tiếp trên khung thông tin/tag của từng frame trong CVAT.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 20 | 4 | 0 | 17 | 15 | 11 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 6 | 8 | 7 | 7 | 5 | 4 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | `lane` / `road_curb` / `drivable` | Vẽ thêm `lane` (`L1`/`R1`) giả hay chỉ gán `drivable` và `road_curb` | Chỉ gán `drivable` và `road_curb` (không vẽ `lane`) | Mặt đường không có vạch sơn phân làn rõ ràng, chỉ có vùng chạy xe và mép/lề đường |
| B01_02688_FV.png / B02_03177_FV.png | `crosswalk` / `drivable` | Gộp chung vùng vạch đi bộ với vùng lái hay tách riêng `crosswalk` và `drivable` | Tách `crosswalk` (polygon) và `drivable` (`area_type="direct"`) | Phân tách rõ vùng vạch qua đường và mặt đường xe chạy theo guideline |
| B02_03177_FV.png | `traffic_light` | `edge_zone="false"` hay `edge_zone="true"` cho đèn sát góc | `edge_zone="true"` cho 2 đèn ở góc trên trái/phải, `false` cho đèn phía trong | Hai đèn lớn nằm sát vùng rìa/góc khung hình fisheye |
| B03_04267_RV.png / B04_05535_RV.png | `lane` | Dùng `L1`/`R1`/`R2` hay `other` trên camera `fisheye_rear` | `other` (nếu sửa lại `position` cho camera sau fisheye) | Camera sau `fisheye_rear` có góc nhìn ngược phía sau nên cần rà soát chuẩn `position` |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Lương Đức Mạnh  Quyết định nhận được: Đang chờ phiếu QC 1 từ bạn cùng cặp (tạm đối chiếu qua rà soát XML)
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 | 2 | Có | Đang rà soát / sửa trên CVAT (`B03_04267_RV.png`, `B04_05535_RV.png`) |
| QC1-05 | 2 | Có | Đang rà soát (`A02`, `A08` có nhiều đoạn `R1`) |
| QC1-11 | 2 | Có | Đang rà soát (`B01`, `B03` các box sát rìa/góc) |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | ---: | ---: | --- |
| nguyenbinhanh-front.zip | Có | 8 (`A01_bc5fadac-fa6dd225.jpg`) | 9 (`A02_b3c26aff-63a0d7d6.jpg`) | Có (`front`) |
| nguyenbinhanh-fisheye.zip | Có | 6 (`B01_02688_FV.png`) | 12 (`B02_03177_FV.png`) | Có (`fisheye_front`) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `![Tab Labels](screenshots/labels.png)`
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `![Front sample](screenshots/front_sample.png)`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `![Fisheye polyline](screenshots/fisheye_polyline.png)`
4. Một đoạn XML có `<polyline label="lane">`: `![XML lane polyline](screenshots/xml_lane.png)`

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:
- Các lỗi cần chú ý rà soát kỹ là `QC1-03` (thuộc tính `position` của `lane` trên các góc camera không phải `front`), `QC1-05` (gộp liền mạch vạch đứt thay vì tách đoạn), và `QC1-11` (độ cong polyline và `edge_zone` trên ảnh `fisheye`). Ở Ngày 20, mình sẽ kiểm tra lại toàn bộ thuộc tính theo từng loại camera và rà soát từng frame trước khi export.
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:
- Nhãn `lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign` là dữ liệu ground truth để model học nhận diện làn đường, vùng chạy xe an toàn, vạch đi bộ và tín hiệu giao thông. Nếu gán sai `position` của `lane` (ví dụ để `L1`/`R1` trên camera `fisheye_rear` thay vì `other`), model sẽ học sai tương quan không gian theo góc nhìn camera, dẫn đến dự đoán sai làn hoặc nhầm lẫn vùng làn xe khi triển khai thực tế.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | | | | | |
| x của bạn kia | | | | | |