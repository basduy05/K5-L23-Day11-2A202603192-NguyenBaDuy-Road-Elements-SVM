# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Bá Duy               Mã học viên: 2A202603192  
Phiên bản CVAT (Help → About): v2.82.0  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 3  
Thời điểm export (ngày giờ trên CVAT): 21/11/2026, 11:39:23 (giờ Việt Nam)    Số lần nộp lại sau Rework: 1 lần  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | Đủ 6 label: lane (polyline), road_curb (polyline), crosswalk (polygon), drivable (polygon), traffic_light (rectangle), traffic_sign (rectangle). |
| Thuộc tính và giá trị | Có | Khớp hoàn toàn với taxonomy: lane có position/style/color/kind; drivable có area_type; traffic_light có color/type/facing/edge_zone; traffic_sign có group/facing/edge_zone. |
| 4 tag ảnh | Có | Cả 28 ảnh có đủ 4 tag: camera, timeofday, weather, source. Tag camera khớp đúng nhóm camera front/fisheye theo tên ảnh. |
Cách kết thúc polyline trên bản CVAT này: Nhấn phím **N** trên bàn phím sau khi click điểm cuối cùng của đường polyline.  
Cách đặt tag ảnh trên bản CVAT này: Chọn công cụ **Tag** ở thanh công cụ bên trái, chọn label tag tương ứng, sau đó mở bảng **Objects → Details** để kiểm tra và chọn đúng giá trị trong thuộc tính select `value`.  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 29 | 14 | 3 | 23 | 30 | 17 |
| front-extra (đã làm 4 / 4) | 4 | 10 | 3 | 2 | 9 | 6 | 9 |
| fisheye | 8 | 2 | 11 | 7 | 3 | 6 | 1 |
| fisheye-extra (đã làm 3 / 4) | 4 | 0 | 3 | 4 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | Vẽ vạch L1/R1 suy đoán theo mép xe đỗ hay bỏ không gán | Bỏ không vẽ lane L1 và R1 | Không suy đoán vạch sơn từ ranh giới xe đỗ hoặc mép vỉa hè khi thực tế mặt đường không có vệt sơn; tuân thủ quy tắc QC1-03 và đang chờ coach xác nhận miễn QC1-02. |
| A06 | lane | Vạch bên phải sát mép đường là lane R1 hay road_curb | Gán lane R1 (dashed white) | Có dấu hiệu vệt sơn phân làn còn sót lại; phân biệt rõ với mép bê tông của vỉa hè. |
| A09 | lane | Hai polyline cùng mang L1 hay phân chia L1 bên trái và R1 bên phải | Vạch trắng đôi bên trái là L1, vạch trắng đứt bên phải là R1 | Xe đang di chuyển trong làn nằm giữa hai vạch này, nên vạch bên trái là L1 và vạch bên phải là R1 theo đúng quy ước vị trí làn đang đi. |
| A10 | lane | Gán chung tất cả vạch là L1 hay phân định theo thứ tự từ xe | Vạch sát trái là L1, vạch sát phải là R1, vạch ngoài cùng bên trái là L2 | Xác định làn xe chủ đang chạy làm chuẩn: L1 và R1 là hai vạch sát xe nhất, L2 là vạch của làn liền kề bên trái. |
| A13 | lane | Dừng vạch tại đoạn sơn nhìn rõ hay kéo dài qua vùng nước mờ kính | Bổ sung vạch L1 vàng liền dừng ở giới hạn nhìn thấy | Vạch tim đường màu vàng bị mờ dần do hạt nước trên kính chắn gió; chỉ vẽ đến điểm xa nhất còn nhận diện được vệt sơn theo quy tắc điểm dừng. |
| B03 | lane | Cung ngang ở vùng bóng tối phía dưới là lane `other` hay bóng đổ | Bỏ cung ngang giả, vẽ lại vạch R1 bám đúng tâm vệt sơn | Vùng bóng đổ ở đáy ảnh không phải vạch sơn. Vạch R1 thật là vạch trắng đứt ở góc phải được vẽ lại chính xác theo cung cong từ (958,631) đến (684,291), gồm 19 điểm. |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Hoàng Nhật Anh  Quyết định nhận được: Rework (bản 1) / Hold (bản 2). Bản 3 đã sửa R1 và chờ tái kiểm  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-01 tag camera | 0 | Đồng ý | Không có lỗi trong mẫu kiểm. Tuy nhiên đã tự rà soát và sửa 6 tag camera MVL/MVR trên toàn bộ Set B. |
| QC1-02 đủ L1, R1 | 0 | Đồng ý | Đã bỏ các vạch suy đoán ở A05, đang chờ coach xác nhận ngoại lệ QC1-02. |
| QC1-03 position | 3 | Đồng ý | Đã sửa: Xóa bỏ 2 vạch suy đoán ở A05; xóa vạch ngang giả ở B03; chuẩn hóa position ở A09 và A10. |
| QC1-07 vùng lái | 2 | Đồng ý | Đã sửa: Mở rộng cả 2 polygon drivable direct và alternative ở A08 bao phủ qua vùng crosswalk tới mép mặt đường trước xe. |
| QC1-08 đèn, màu | 3 | Đồng ý | Đã sửa: Đổi màu đèn hướng về xe ở A08 sang green cho 2 đèn thấy rõ; đèn khuất đổi sang unknown. |
| QC1-09 thuộc tính biển/đèn | 1 | Đồng ý | Đã sửa: Đổi group biển chỉ dẫn “Harlem River Dr” ở A08 thành information; đổi type đèn người đi bộ sang pedestrian. |
| QC1-11 fisheye | 1 | Đồng ý | Đã sửa: Vẽ lại toàn bộ polyline vạch R1 ở B03 theo các đoạn sơn trắng nhìn thấy, từ (958,631) đến (684,291), chờ tái kiểm độ lệch; bật edge_zone B02 và tắt ở B04. |

## 5. Kiểm file export
Bản nộp dùng manifest revision 3. Hai ZIP chỉ chứa `annotations.xml`, kiểm được bằng parser của lab và khớp SHA-256 trong manifest. Lint còn hai cảnh báo QC1-02 ở A05, chờ coach xác nhận không thấy L1/R1. Bản 2 nhận kết luận Hold, bản 3 chờ tái kiểm R1 ở B03 và các ca mơ hồ trong phiếu nhận được. Chỉnh sửa bản 3 thực hiện trong ZIP cục bộ.

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `nguyenbaduy-front.zip` | Có | A01: 9 / 9 | A02: 6 / 6 | Có (16/16 ảnh đủ 4 tag, camera=front) |
| `nguyenbaduy-fisheye.zip` | Có | B01: 3 / 3 | B02: 3 / 3 | Có (12/12 ảnh đủ 4 tag, camera đúng FV/RV/MVL/MVR) |

## 6. Ảnh chụp màn hình

Bốn minh chứng dưới đây đang chờ bổ sung từ project CVAT của bài làm.

1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ, ví dụ A12.
3. Một ảnh fisheye phóng to đoạn polyline cong.
4. Đoạn XML trích từ `nguyenbaduy-front.zip`, bản 3, ảnh A12_c0f978fa-9b4e623f.jpg.

```xml
<polyline label="lane" source="manual" occluded="0" points="391.61,444.31;479.94,395.57" z_order="0">
      <attribute name="position">L1</attribute>
      <attribute name="style">solid</attribute>
      <attribute name="color">white</attribute>
      <attribute name="kind">single</attribute>
    </polyline>
```

Ảnh chụp màn hình XML vẫn chờ bổ sung.

Các câu hỏi cần phản hồi để chốt bài:

- Coach xác nhận A05 không nhìn thấy L1/R1 để miễn hai cảnh báo QC1-02.
- Nhật Anh tái kiểm R1 mới ở B03 trong bản 3 và cập nhật kết luận.
- Coach chốt màu tín hiệu người đi bộ sáng trắng ở A08 trong schema hiện tại, cùng phạm vi nhãn cần có ở B03.


## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Lỗi mắc nhiều nhất là **QC1-01 (nhầm lẫn tag camera MVL và MVR trên ảnh fisheye)** và **QC1-03 (thuộc tính position mặc định của CVAT)**. Cách tránh ở Ngày 20:
- Đối chiếu ngay hậu tố tên file trước khi gắn tag: `MVL` quy định bắt buộc là `fisheye_left`, `MVR` bắt buộc là `fisheye_right`.
- Thiết lập quy trình thao tác chuẩn: ngay sau khi vẽ xong một đối tượng, lập tức mở bảng Details để kiểm tra và chọn đúng thuộc tính, không để thuộc tính mặc định của CVAT (luôn là L1 / solid / white / single).

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Nhãn vạch kẻ đường polyline trực tiếp đi vào huấn luyện các mô hình phát hiện làn (Lane Detection) như Ultra-Fast-Lane-Detection hoặc các kiến trúc anchor-based / row-anchor. Nếu mắc lỗi **QC1-03 (nhầm vạch bên phải thành L1 như ở A09 và A10)**:
- Tại các hàng ảnh (row anchors), mô hình sẽ nhận nhãn giám sát ground truth với hai vạch cùng mang nhãn L1 (cạnh tranh trực tiếp ranh giới bên trái), trong khi nhãn R1 bên phải bị thiếu hoàn toàn.
- Khi huấn luyện, hàm mất mát (loss function) bị phạt sai hướng, khiến mạng nơ-ron học nhầm rằng ranh giới bên phải của làn đường cũng là vạch bên trái.
- Khi triển khai thực tế trên hệ thống hỗ trợ giữ làn (LKA - Lane Keeping Assist), xe sẽ không xác định được tâm làn di chuyển an toàn, có thể đánh lái sai lệch sang phải hoặc cảnh báo sai lệch làn đường, gây mất an toàn nghiêm trọng.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | không có làn | 600.1 | 543.1 | 486.1 |
| x của bạn kia | không có làn | 655.1 | 598.2 | 541.3 | 484.8 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?  
**Trả lời:** Nếu dừng polyline sớm 40 px (từ y=680 lên y=640), hàng **y = 680** sẽ bị đổi thành "không có làn" (đối với bạn kia) hoặc mất luôn đoạn dự đoán giao cắt ở vùng gần xe.

2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?  
**Trả lời:** 
- Ở hàng y = 720: Cả hai đều ghi nhận "không có làn", nên không có tọa độ x để tính độ lệch tại hàng này.
- Ở hàng y = 560: x của chúng tôi là 486.1 px, x của bạn kia là 484.8 px, độ lệch là **1.3 px** (nằm hoàn toàn trong ngưỡng sai số cho phép ≤ 5 px).
- **Lệch ở hàng gần xe (hàng 720 / 680) ảnh hưởng đến LKA nhiều hơn.** Lý do: theo động lực học xe tự hành (slide 25), vùng gần đầu xe quyết định sai số vị trí ngang tức thời (lateral offset) và góc lệch hướng (heading angle). Sai số ở hàng gần xe sẽ khiến bộ điều khiển LKA đưa ra lệnh đánh lái gấp ngay lập tức, trong khi sai số ở hàng xa (hàng 560) chỉ ảnh hưởng đến việc ước lượng trước độ cong (preview curvature) ở cự ly xa.

3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?  
**Trả lời:** 
- Về mặt toán học hình học giải tích thuần túy, giao điểm của đường thẳng tại các hàng y cố định không đổi giá trị tọa độ x.
- `road_check lint` và `road_lab.rowanchor` cảnh báo chiều polyline ngược quy tắc. Hàm nội suy hiện tại vẫn tính được giao điểm khi đảo thứ tự điểm.
