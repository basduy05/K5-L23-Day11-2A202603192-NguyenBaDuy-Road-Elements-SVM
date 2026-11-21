# Phiếu QC 1 — Road v1.0 · Kiểm lại bản 2

Lô được kiểm: Hoàng Nhật Anh  
Người kiểm: Nguyễn Bá Duy  
Ngày: 21/11/2026  
Phiên bản guideline: Road v1.0  
File được kiểm: `hoangnhatanh-front.zip` và `hoangnhatanh-fisheye.zip`, khớp SHA-256 trong `hoangnhatanh-manifest.json` bản 2, tạo lúc `2026-11-21T04:32:33+00:00`.

Kiểm lại trên cùng 6 ảnh của phiếu bản 1 để so sánh trực tiếp. Mẫu gồm A01, A04, A09, B01, B05, B07 và 0 ảnh thưởng. Đối chiếu XML với ảnh gốc và ảnh chồng nhãn.

| Ảnh | Shape | Tag |
| --- | ---: | ---: |
| A01 | 12 | 4 |
| A04 | 15 | 4 |
| A09 | 18 | 4 |
| B01 | 5 | 4 |
| B05 | 19 | 4 |
| B07 | 10 | 4 |
| **Tổng** | **79** | **24** |

**Số nhãn đã kiểm: 103.** Một nhãn có thể được kiểm theo nhiều mã. Mỗi cặp polyline cùng biểu diễn một vạch đôi được tính là một lỗi hình học.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | Sai thuộc tính / bỏ sót | 6 tag camera | 0 | Nặng |
| QC1-02 đủ L1, R1 | Bỏ sót | 6 vị trí ở 3 ảnh front | 0 | Nặng |
| QC1-03 position | Sai thuộc tính / thừa | 19 lane | 1 | Nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | Sai phạm vi | 19 lane | 4 | Chính |
| QC1-05 vạch đứt, che | Sai phạm vi / sai thuộc tính | 19 lane | 0 | Chính |
| QC1-06 style, color, kind | Sai thuộc tính | 19 lane | 0 | Chính |
| QC1-07 vùng lái | Sai phạm vi / bỏ sót / thừa | 10 drivable | 1 | Chính |
| QC1-08 đèn, màu | Bỏ sót / sai phạm vi / sai thuộc tính | 12 đèn | 0 | Nặng / chính |
| QC1-09 facing, type, group, biển phụ | Sai thuộc tính | 25 đèn và biển | 0 | Chính |
| QC1-10 hình in, đủ biển | Bỏ sót / sai phạm vi | 13 biển đã gán và rà 6 ảnh | 0 | Chính |
| QC1-11 fisheye | Sai phạm vi / sai thuộc tính | 34 shape fisheye | 0 | Chính |
| QC1-12 file | Lỗi file / hình | 2 ZIP và 103 nhãn | 2 | Nhẹ |

Ở A09, vạch R1 đã được vẽ nhưng gán sai `position`. Phiếu ghi lỗi này một lần ở QC1-03.

## Danh sách lỗi còn lại

Số sau dấu `#` là thứ tự shape trong XML **bản 2** của từng ảnh, bắt đầu từ 0 và bỏ qua tag.

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả và cách sửa |
| ---: | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | `lane#4`, `lane#6` | Chính | Hai polyline cùng biểu diễn vạch đôi trắng L2. Dùng một polyline ở giữa hai nét, giữ `kind=double`. |
| 2 | QC1-12 | A01 | `drivable#11` | Nhẹ | Hai điểm (452.40, 539.57) liền nhau trong polygon. Bỏ điểm trùng. |
| 3 | QC1-04 | A04 | `lane#10`, `lane#14` | Chính | Vạch vàng đôi L1 vẫn có hai polyline. Dùng một polyline ở giữa hai nét, giữ `kind=double`. |
| 4 | QC1-04 | A04 | `lane#8`, `lane#9` | Chính | Hai polyline cùng biểu diễn vạch đôi trắng R2. Dùng một polyline ở giữa hai nét. |
| 5 | QC1-03 | A09 | `lane#3` | **Nặng** | Vạch trắng đứt sát bên phải làn xe vẫn mang `position=L1`. Sửa thành `R1`. |
| 6 | QC1-04 | A09 | `lane#4`, `lane#5` | Chính | Hai nét của vạch trắng đôi bên trái vẫn được vẽ riêng. Dùng một polyline ở tâm cặp vạch và đặt `kind=double`, `position=L1`. |
| 7 | QC1-07 | A09 | `drivable#1` | Chính | Polygon bên phải vạch đứt vẫn mang `area_type=direct` và kéo xuống phần thân xe. Xác định vùng làn kế bên, cắt theo phần mặt đường nhìn thấy trước thân xe. |
| 8 | QC1-12 | B07 | `lane#3` | Nhẹ | Hai điểm (96.54, 736.62) liền nhau. Bỏ điểm trùng. |

## Các lỗi đã sửa từ bản 1

| Ảnh | Kết quả |
| --- | --- |
| A04 | Cụm đèn tại khoảng (604, 271) đã đổi `red` thành `green`. |
| B01 | Hai box đèn đã chuyển sang `facing=back` và `color=unknown`. Polygon thừa dọc ray tàu đã được bỏ, polygon zebra được giữ. Đoạn curb ngắn hai điểm được hỏi ở bản 1 cũng đã được bỏ. |
| B05 | Cả hai lane camera bên trái đã dùng `position=other`. Biển phụ dưới biển cấm đi ngược chiều đã đổi thành `supplementary` và tắt `edge_zone`. |
| B07 | Cả bốn lane camera bên phải đã dùng `position=other`. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp |
| --- | --- | --- |
| B05 | `road_curb#5` chỉ có ba điểm. Cần kiểm ở kích thước gốc xem hình đã bám cung mép đường trong ngưỡng 5 px chưa. | Chờ xác nhận. Chưa tính lỗi. |

## Quyết định

**Rework.** Mẫu bản 2 còn **1 lỗi nặng**, **5 lỗi chính / 103 nhãn = 4,85%**, **2 lỗi nhẹ** và **1 ca chờ lead**. Lỗi nặng A09 đủ để trả sửa theo quy tắc QC 1.

Ưu tiên sửa A09, sau đó gộp các polyline vạch đôi còn trùng ở A01 và A04 và bỏ điểm lặp ở A01, B07. Lint toàn lô bản 2 giảm từ 59 xuống 44 cảnh báo (8 nặng, 21 chính, 15 nhẹ). Kết quả trong phiếu tính trên 6 ảnh đối chiếu trực quan.
