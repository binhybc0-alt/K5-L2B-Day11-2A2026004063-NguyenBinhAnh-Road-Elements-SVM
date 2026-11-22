# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Bình Anh              Mã học viên: 2A2026004063
Phiên bản CVAT (Help → About): 2.7
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2
Thời điểm export (ngày giờ trên CVAT): 2026-11-22 09:11 giờ VN    Số lần nộp lại sau Rework: 1

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane`, `road_curb` (polyline); `crosswalk`, `drivable` (polygon); `traffic_light`, `traffic_sign` (rectangle) |
| Thuộc tính và giá trị | Đúng | Đủ các attribute theo Road v1.0 (`position`, `style`, `color`, `kind`, `area_type`, `type`, `facing`, `group`, `edge_zone`) |
| 4 tag ảnh | Đúng | Đủ `camera`, `timeofday`, `weather`, `source` trên cả 12 ảnh `front` và 8 ảnh `fisheye` (20/20 ảnh đủ 4 tag, 0 ảnh trống) |

Cách kết thúc polyline trên bản CVAT này: Nhấn phím `N` hoặc click chuột phải / hoàn tất thao tác vẽ polyline trên CVAT.
Cách đặt tag ảnh trên bản CVAT này: Gán 4 tag (`camera`, `timeofday`, `weather`, `source`) trực tiếp trên khung thông tin/tag của từng frame trong CVAT.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 38 | 5 | 1 | 23 | 27 | 17 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 10 | 12 | 13 | 9 | 7 | 6 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

Nguồn số liệu: `nguyenbinhanh-manifest.json` (revision 2), trường `files[].shapes_by_label`; đã đối chiếu lại trực tiếp với `annotations.xml` trong hai file zip — khớp hoàn toàn.
Tổng: front 111 shape + 48 tag = 159 nhãn; fisheye 57 shape + 32 tag = 89 nhãn.

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | `lane` / `road_curb` / `drivable` | Vẽ thêm `lane` (`L1`/`R1`) giả hay chỉ gán `drivable` và `road_curb` | Chỉ gán `drivable` và `road_curb` (không vẽ `lane`) | Mặt đường không có vạch sơn phân làn rõ ràng, chỉ có vùng chạy xe và mép/lề đường. Xem mục ngoại lệ QC1-02 ở Mục 4 |
| A06_b8c66e31-37045eec.jpg | `lane` (`position`) | Vạch sát xe là `L1` hay `R1`, vạch ngoài là `R2` hay `L2` | `L1` (sát xe, bên trái) + `R2` (vạch ngoài, bên phải) | Ảnh không thấy vạch sơn ở bên phải sát xe nên không gán `R1`; xem mục ngoại lệ QC1-02 ở Mục 4 |
| B01–B08 | `crosswalk` / `drivable` | Gộp chung vùng vạch đi bộ với vùng lái hay tách riêng `crosswalk` và `drivable` | Tách `crosswalk` (polygon) và `drivable` (`area_type="direct"`) | Phân tách rõ vùng vạch qua đường và mặt đường xe chạy theo guideline mục 3 |
| B02_03177_FV.png | `traffic_light` | `edge_zone="false"` hay `edge_zone="true"` cho đèn sát góc | `edge_zone="true"` cho đèn nằm ngoài 80 % bán kính vòng ảnh | Đèn lớn nằm sát vùng rìa/góc khung hình fisheye, tâm hộp nằm ngoài 80 % bán kính |
| B03_04267_RV.png / B04_05535_RV.png | `lane` (`position`) | Camera sau `fisheye_rear` có dùng được `L1`/`R1`/`L2`/`R2` không | Vẫn dùng `L1`/`R1`/`L2`/`R2` | Guideline mục 4: "position L1/R1/L2/R2 chỉ dùng ở fisheye_front và fisheye_rear"; chỉ `fisheye_left`/`fisheye_right` mới bắt buộc `other` |
| B06_04068_MVL.png / B07_01216_MVR.png / B08_05885_MVR.png | `lane` (`position`) | Camera bên hông có cần phân biệt trái/phải không | `position="other"` cho toàn bộ lane | Guideline mục 4: ở `fisheye_left` và `fisheye_right` luôn dùng `position = other` |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Lương Đức Mạnh  Quyết định nhận được: **Rework** (2 lỗi nặng QC1-03)

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 | 2 | Có | Đã sửa xong ở B07 (`fisheye_right` → đổi cả 3 lane sang `position="other"`) |
| QC1-05 | 2 | Có | Đã rà soát; không còn vạch đứt bị tách thành nhiều polyline |
| QC1-11 | 2 | Có | Đã rà soát `edge_zone` và độ cong polyline ở B01/B03 |

### Lần nộp lại (revision 2) — đã sửa gì

So với bản revision 1 (lưu ở `r1/nguyenbinhanh-manifest-r1.json`), các thay đổi đã thực hiện:

| # | Sửa gì | Phạm vi | Mã liên quan |
| --- | --- | --- | --- |
| 1 | Đảo chiều 10 polyline vẽ ngược (đi từ xa về gần) | A06, A09, A12 (3 `road_curb`); B02 ×2, B05 (3 `road_curb`); B06, B07 ×2, B08 (4 `lane`) | QC1-04 |
| 2 | Đổi `position` của lane trên camera bên hông sang `other` | B07 (`fisheye_right`): 3 lane | QC1-03 |
| 3 | Bổ sung vùng `crosswalk` còn thiếu | A06 (1 polygon) | QC1-07 |
| 4 | Bổ sung/bổ trục `lane`, `road_curb`, `drivable`, `traffic_light`, `traffic_sign` cho các ảnh gọn nhãn | A05 (3 shape), B05 (4 shape), B06 (4 shape), B08 (3 shape) | QC1-07, QC1-10 |
| 5 | Kiểm tra lại `edge_zone` trên box sát rìa ảnh fisheye | B01–B08 | QC1-11 |

Kết quả `road_check lint` sau khi sửa: **3 nặng / 2 chính / 0 nhẹ** (bản revision 1: 3 nặng / 11 chính / 0 nhẹ). Còn 10 polyline ngược chiều đã được sửa hoàn toàn, lint không còn cảnh báo nào về chiều vẽ.

### Ngoại lệ QC1-02 — ảnh không có vạch sơn, xin coach/lead xác nhận

`lint` báo 3 cảnh báo mức nặng QC1-02 ("chưa có L1 / R1"). Theo đặc tả bàn giao mục 2, ngoại lệ duy nhất là QC1-02 ở ảnh mà coach đã nhìn và xác nhận không thấy vạch. Em xin coach/lead xác nhận giúp 2 ảnh sau:

| Ảnh | Cảnh báo | Thực tế trong ảnh | Lý do không gán |
| --- | --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | chưa có L1, chưa có R1 | Chỉ có `drivable` (1 polygon), `road_curb` (1 polyline), `traffic_sign` (1 box); **0 lane** | Mặt đường không có vạch sơn phân làn. Chỉ thấy mép/lề đường và một biển. Không có vạch để đặt polyline — vẽ thêm sẽ là nhãn bịa |
| A06_b8c66e31-37045eec.jpg | chưa có R1 | Có 3 lane: `L1` (sát xe, bên trái), `R2` (vạch ngoài, bên phải), 1 lane `other`; có `crosswalk`, `drivable`, 1 `road_curb`, 5 `traffic_light`, 3 `traffic_sign` | Bên phải sát xe không thấy vạch sơn; vạch quan sát được ở bên phải là vạch ngoài cùng nên đã gán `R2`. Vạch sát xe bên trái đã gán `L1` |

Xin coach/lead trả lời giúp: **ở A05 và A06 có thật sự không có vạch sơn ở vị trí `L1`/`R1` không?** Nếu có vạch thì em sẽ bổ sung rồi export lại (revision 3). Nếu không có, em ghi mã ảnh A05, A06 kèm lý do này vào phiếu QC 1 để được miễn lỗi nặng.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | ---: | ---: | --- |
| nguyenbinhanh-front.zip | Có | 8 (`A01_bc5fadac-fa6dd225.jpg`) | 8 (`A02_b3c26aff-63a0d7d6.jpg`) | Có (`front`) |
| nguyenbinhanh-fisheye.zip | Có | 6 (`B01_02688_FV.png`) | 12 (`B02_03177_FV.png`) | Có (`fisheye_front`) |

Cả hai file: `annotations.xml` nằm ngay thư mục gốc zip, không kèm ảnh (`contains_images: false` trong manifest), mở lại được bằng `road_check lint` với 20 ảnh, 0 ảnh trống, 20/20 ảnh đủ 4 tag.

## 6. Ảnh chụp màn hình
1. Tab Labels của project: `![Tab Labels](screenshots/labels.png)`
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển): `![Front sample](screenshots/front_sample.png)`
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong: `![Fisheye polyline](screenshots/fisheye_polyline.png)`
4. Một đoạn XML có `<polyline label="lane">`: `![XML lane polyline](screenshots/xml_lane.png)`

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:
- Lỗi em mắc nhiều nhất là **QC1-04 (chiều vẽ polyline)**: 10 polyline trong bản revision 1 bị vẽ ngược (đi từ xa về gần) — 4 lane ở B06/B07/B08 và 6 road_curb ở A06/A09/A12/B02/B05. Nguyên nhân gốc: khi vẽ trên CVAT, sau khi bấm điểm đầu em hay kéo chuột định hướng trước rồi mới đặt các điểm tiếp theo, nên điểm đầu bị rơi vào cuối đoạn. Ở Ngày 20 em sẽ quy trình lại thành 2 bước: (1) đặt điểm đầu sát xe trước, xác nhận đúng vị trí rồi (2) mới đặt lần lượt các điểm tiếp theo đi ra xa, và trước khi export sẽ chạy một script kiểm tra `y_đầu ≥ y_cuối` cho mọi `lane`/`road_curb`.
- Ngoài ra là **QC1-03 (position)** ở B07: camera `fisheye_right` nhưng còn 1 lane để `L1`. Em đã sửa toàn bộ 3 lane của B07 sang `other`. Điều này củng cố điều em nói ở Ngày 20: phải đọc kỹ quy tắc theo từng loại camera (`front`/`fisheye_front`/`fisheye_rear` mới dùng L1/R1/L2/R2; `fisheye_left`/`fisheye_right` luôn `other`) chứ không áp dụng một công thức chung cho mọi ảnh.
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:
- Nhãn `lane`, `road_curb`, `crosswalk`, `drivable`, `traffic_light`, `traffic_sign` là ground truth để model học nhận diện làn đường, vùng chạy xe an toàn, vạch ngựa vạn và tín hiệu giao thông.
- **Lỗi đã sửa: chiều vẽ polyline ngược ở B08** (1 `lane` bị đảo). Ở B08 (`fisheye_right`), lane đi từ `(206,632)` về `(69,745)` — tức điểm đầu ở xa, điểm cuối ở gần xe. Nếu giữ nguyên và dùng làm GT:
  1. Model học được một "vạch làn" mà hướng đi của nó ngược với hướng chạy của xe. Khi triển khai, hệ thống row-anchor sẽ nội suy theo chiều thời gian ngược, tức dự đoán điểm ở hàng xa (y nhỏ) là điểm ở hàng gần (y lớn) — đảo ngược trục không gian của mục tiêu.
  2. Lỗi này "tự triệt tiêu" khi đánh giá bằng IoU hay khoảng cách trung bình: một polyline vẽ ngược vẫn cho cùng tập điểm, nên IoU vẫn cao. Nhưng khi dùng **điểm đầu làm mốc** (điểm đầu phải là điểm gần xe, là mốc quan trọng nhất theo guideline), thì điểm đầu bị đặt sai — và khoảng cách giữa hai điểm đầu lệch tới nửa chiều dài vạch. Ở hàng 720 (sát xe), một điểm đầu đặt sai làm cả chuỗi điểm trượt khỏi tâm vạch, và sai số này nhân lên khi nội suy lên các hàng phía trên.
  3. Hậu quả trực tiếp với LKA: hệ thống cần biết "vạch này nằm bên trái hay bên phải xe" để quyết định lấy làn nào. Một polyline đảo chiều làm đảo luôn dấu của vector hướng làn, nên thuật toán có thể tính nhầm làn bên trái thành bên phải — đúng lúc cần canh vào làn thì hệ thống lại tránh làn. Lỗi này im lặng (IoU vẫn tốt) nên càng nguy hiểm.
- Vì vậy em hiểu vì sao rubric tính cả điểm "chiều gần ra xa" (tiêu chí *dir*, 8 điểm) tách riêng khỏi "khoảng cách lớn nhất tới GT" (tiêu chí *dev*, 9 điểm): đó là hai loại lỗi khác nhau, một cái nhìn thấy bằng pixel, một cái chỉ thấy được khi dùng điểm đầu làm mốc.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | | | | | |
| x của bạn kia | | | | | |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
