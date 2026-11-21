# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lương Đức Mạnh (luongducmanh / MANH610)        Người kiểm (học viên): Nguyễn Bình Anh (nguyenbinhanh)
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): luongducmanh-front.zip, luongducmanh-fisheye.zip (+ luongducmanh-front-extra.zip, luongducmanh-fisheye-extra.zip), revision 1
Số ảnh kiểm: 20 (+ 8 ảnh thêm, ghi riêng: 28 ảnh tổng)   Số nhãn đã kiểm (shape + tag): 233 (121 shape + 112 tag)

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 112 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 28 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 32 | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 44 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 32 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 32 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 19 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 23 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 23 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 23 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 28 | 0 | chính |
| QC1-12 file | lỗi file | 4 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | B03_04267_RV.png | lane (R1, R2) | nặng | Camera fisheye_rear nhưng dùng position R1/R2 thay vì other |
| 2 | QC1-03 | B04_05535_RV.png | lane (L1) | nặng | Camera fisheye_rear nhưng dùng position L1 thay vì other |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | Đường thực tế không có vạch sơn phân làn, chỉ có road_curb/drivable — xác nhận miễn thiếu L1/R1? | |
| A06 / A08 / A12 | Cảnh báo lint thiếu L1/R1 ở các ảnh này là thiếu vạch thật hay không có vạch? | |
| B11_07282_RV.png | Ảnh không có shape nào (0 shape) — xác nhận ảnh trống/không có đối tượng hay bỏ sót? | |
| A12, B01, B02, B05–B10, B12 | Không có polygon drivable trong XML — có cần bổ sung vùng lái không? | |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 0 / 233 nhãn = 0.00 %   Lỗi nhẹ: 0   Ca chờ lead: 4
Quyết định (Release / Hold / Rework): Rework
Lý do (theo luật của phiếu): Có 2 lỗi nặng QC1-03 (position L1/R1/R2 trên camera fisheye_rear ở B03, B04) và có các ca cần rà soát lại.