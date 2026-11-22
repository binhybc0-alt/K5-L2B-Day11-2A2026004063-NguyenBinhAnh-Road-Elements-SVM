# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lương Đức Mạnh (luongducmanh)        Người kiểm (học viên): Nguyễn Bình Anh (nguyenbinhanh)
Ngày: 2026-11-22                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): luongducmanh-front.zip, luongducmanh-fisheye.zip, revision 1
Số ảnh kiểm: 20 (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 184 (104 shape + 80 tag)

> Các mục kiểm dưới đây được đếm bằng script trên `annotations.xml` của đúng 2 file export trên (đọc trực tiếp từ zip). Những mục cần GT để kết luận (độ lệch tâm vạch ≤ 5 px, IoU vùng lái, sát vỏ hộp đèn/biển, màu đèn, `facing`) thì không có GT nên ghi ở mục *Ca mơ hồ* hoặc để trống — người kiểm và lead mới quyết định.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 80 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 26 | 13 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 10 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 10 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 10 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 10 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 19 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 15 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 15 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 10 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 41 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Tổng số mục kiểm 248 (shape + tag của 20 ảnh). Các mã QC1-02 và QC1-04 đã đếm trực tiếp; QC1-03/05/06/07/08/09/10/11 cần GT nên số mục kiểm ghi theo số shape của nhóm tương ứng, còn số lỗi để trống cho người kiểm.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05_b2576c8c-2de20b8a.jpg | lane | nặng | Không có lane nào (chỉ `drivable` + `road_curb`) → thiếu L1 và R1. Cần coach xác nhận ảnh không có vạch sơn |
| 2 | QC1-02 | A06_b8c66e31-37045eec.jpg | lane | nặng | Không có lane nào (có `crosswalk`, `drivable`, 4 `traffic_light`, 5 `traffic_sign`) → thiếu L1 và R1. Cần coach xác nhận |
| 3 | QC1-02 | A08_c0deebc1-16cfa791.jpg | lane | nặng | Chỉ có `R1` + `R2`, thiếu L1 |
| 4 | QC1-02 | A12_c0f978fa-9b4e623f.jpg | lane | nặng | Không có lane nào → thiếu L1 và R1 |
| 5 | QC1-02 | B01_02688_FV.png | lane | nặng | Camera `fisheye_front` nhưng không có lane nào → thiếu L1 và R1 |
| 6 | QC1-02 | B02_03177_FV.png | lane | nặng | Camera `fisheye_front` nhưng không có lane nào → thiếu L1 và R1 |
| 7 | QC1-02 | B03_04267_RV.png | lane | nặng | Camera `fisheye_rear`, có `R1`+`R2` nhưng thiếu L1 |
| 8 | QC1-02 | B04_05535_RV.png | lane | nặng | Camera `fisheye_rear`, chỉ có `L1` → thiếu R1 |
| 9 | QC1-04 | B05_05780_MVL.png | lane | chính | Polyline vẽ ngược chiều: điểm đầu có `y` nhỏ hơn điểm cuối → đi từ xa về gần, phải vẽ từ gần xe ra xa |

Ghi chú về QC1-02: theo đặc tả bàn giao, QC1-02 ở ảnh mà coach đã nhìn và xác nhận không thấy vạch thì được miễn. Vì vậy 8 mục đầu là **ngoại lệ cần coach/lead xác nhận**, không tự kết luận là lỗi của bạn Lương Đức Mạnh. Riêng A05, A06, A12 (mặt đường không có vạch sơn phân làn rõ) và B01/B02 (fisheye_front không thấy vạch) khả năng cao được miễn.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | Đường thực tế không có vạch sơn phân làn (chỉ có `drivable` + `road_curb`) — xác nhận miễn thiếu L1/R1? | |
| A06_b8c66e31-37045eec.jpg | Ảnh có `crosswalk` + 4 đèn + 5 biển nhưng 0 lane — xác nhận không có vạch sơn? | |
| A08_c0deebc1-16cfa791.jpg | Chỉ thấy vạch bên phải (`R1`,`R2`), bên trái không có vạch — thiếu L1 là thật hay bỏ sót? | |
| A12_c0f978fa-9b4e623f.jpg | 0 lane nhưng có `crosswalk` + 2 đèn + 2 biển — xác nhận không có vạch sơn? | |
| B01_02688_FV.png, B02_03177_FV.png | Camera `fisheye_front` không gán lane nào — ảnh có vạch sơn không? | |
| B03_04267_RV.png, B04_05535_RV.png | Camera `fisheye_rear` chỉ thấy vạch một bên — bên kia có vạch không? | |
| Toàn bộ 20 ảnh | `drivable` và `crosswalk` có IoU ≥ 0.85 / 0.75 so với GT không, và có tràn ra ngoài vùng GT không? Cần GT để kết luận | |
| Toàn bộ 20 ảnh | Hộp đèn/biển có sát vỏ (IoU ≥ 0.75) không, `color`/`facing`/`type`/`group`/`edge_zone` có đúng không? Cần GT + quan sát | |

## Quyết định
Lỗi nặng: 8 (tất cả là QC1-02 chờ xác nhận miễn)   Lỗi chính: 1 / 248 nhãn = 0.40 %   Lỗi nhẹ: 0   Ca chờ lead: 8
Quyết định (Release / Hold / Rework): **Hold**
Lý do (theo luật của phiếu): Chưa có lỗi nặng nào được xác nhận là lỗi thật — 8 cảnh báo QC1-02 đều thuộc loại ngoại lệ có thể được miễn nếu coach xác nhận ảnh không có vạch sơn, và quyết định miễn hay không thuộc việc của người kiểm/lead chứ không phải script. Lỗi chính chỉ có 1 (B05 vẽ ngược chiều), tỉ lệ 0.40 % ≤ 5 %. Theo đặc tả, checker không bao giờ ra Hold vì không biết ca mơ hồ, nên phiếu để **Hold** trong lúc chờ lead trả lời 8 câu hỏi ở mục *Ca mơ hồ*. Nếu lead xác nhận miễn cả 8 mục QC1-02 thì lô này **Release**; nếu phát hiện ảnh có vạch mà bỏ sót thì **Rework** (bổ sung lane + sửa B05 rồi export lại, revision 2).

---

### Ghi chú từ người kiểm

- Đã kiểm bằng script trên `annotations.xml`: 20 ảnh đủ 4 tag, `camera` đúng với tên file ở cả 20 ảnh; `position` của 4 lane trên camera bên hông (`B05`–`B08`, `fisheye_left`/`fisheye_right`) đều là `other` — đúng guideline mục 4; không có ảnh trống; hai file export mở lại được và `annotations.xml` nằm ở thư mục gốc.
- Việc người kiểm đã trải qua trong lô của mình, nêu ở đây để đối chiếu: bản revision 1 của em cũng từng có 1 lane ở `B07` để `position=L1` dù camera là `fisheye_right` (QC1-03) và 10 polyline vẽ ngược chiều (QC1-04). Sau khi sửa, `lint` của em còn 3 nặng / 2 chính; 3 nặng đều là QC1-02 ở A05/A06 và đã ghi xin coach xác nhận miễn. Nếu em cần tham khảo cách xử lý: đảo chiều polyline thì đảo thứ tự các cặp `x,y` trong `points` (giữ nguyên file zip, `annotations.xml` ở thư mục gốc), và `position` trên camera bên hông thì đổi hết sang `other`.
- Lỗi QC1-04 ở B05: polyline `lane` có điểm đầu `(905.77,219.15)` và điểm cuối `(1105.88,412.06)` — điểm đầu nằm **xa** hơn điểm cuối, tức đang đi từ xa về gần. Cần đảo lại thứ tự điểm.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
