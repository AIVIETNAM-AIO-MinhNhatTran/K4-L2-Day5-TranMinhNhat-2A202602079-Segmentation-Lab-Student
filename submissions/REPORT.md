# Báo cáo Day 5

- Mã học viên theo lớp: 2A202602079
- Ngày / CVAT local: 2026-09-17 / CVAT local
- Công cụ đã dùng: Brush và Polygon; kiểm tra mask và export từ CVAT

## 1. Bài đã nộp

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

## 2. Một quyết định trước khi dùng gợi ý

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, một xe máy trong vùng đường phố.
- Class và quy tắc tôi dùng để chọn biên: `motorcycle`; chỉ lấy phần xe nhìn thấy, bám theo biên thân xe và không lấy phần nền đường.
- Nếu dùng gợi ý sau đó: không dùng gợi ý tự động; tôi kiểm tra từng mask và tách các vật cùng lớp thành object riêng.

## 3. Một lỗi tôi tìm thấy và sửa

- Task/ảnh/vùng: `medium_instance`, các ảnh `000000373353.jpg`, `000000181542.jpg` và `000000458325.jpg`.
- Lỗi thuộc loại: sai lớp.
- Bằng chứng tôi nhìn thấy: file export có các category `road`, `sidewalk`, `building`, `vegetation`, `sky` và `traffic light`, trong khi `medium_instance/classes.json` yêu cầu sáu class instance `person`, `bicycle`, `car`, `motorcycle`, `bus`, `truck`.
- Quy tắc và hành động sửa: chưa sửa được trong CVAT; cần mở lại task Medium, chọn đúng taxonomy instance, kiểm tra lại class/object rồi Save và export lại.
- Sau sửa đã Save và export lại chưa? Chưa. ZIP hiện tại vẫn là bản có lỗi taxonomy; đã ghi nhận để sửa trước khi nộp chính thức.

Kết quả tự đánh giá sau export: Easy `16.7/20`, Medium `13.2/32`, Hard `1.8/30`, tổng ba tier `31.7/82`. Đây là điểm tự đánh giá, không phải điểm chính thức; chưa có kết quả trước/sau khi sửa lỗi Medium.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `cp1_holes`, vùng cửa sổ/khoảng trống của vật | Cắt lỗ ra khỏi mask hoặc giữ lỗ bên trong mask | Cửa sổ/khoảng hở vẫn nằm trong mask | Giữ vùng bên trong mask, không tạo lỗ riêng. |
| `cp2_slice`, hai xe cùng lớp đứng sát nhau | Gộp thành một object hoặc tách thành hai instance | Nhìn thấy khe/biên riêng giữa hai xe | Tách thành hai object riêng. |
| `cp4_curb`, ranh road-sidewalk ở mép bó vỉa | Gán toàn bộ vùng màu asphalt cho road hoặc phân theo chức năng sử dụng | Ranh được xác định theo bó vỉa và chức năng road/sidewalk, không chỉ theo màu | Chọn ranh theo mặt bó vỉa; phần lối đi là sidewalk, phần xe chạy là road. |