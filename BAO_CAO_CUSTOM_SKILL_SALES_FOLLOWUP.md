# Báo Cáo Xây Dựng Custom Skill 'sales_followup' Soạn Thảo Email Cá Nhân Hóa

* **Mã bài tập:** AI301_S03_BTVN_M3_BT1 | **Học phần:** AI301 - AI Agent
* **Đơn vị:** FPT SmartBiz | **Mục tiêu:** Nâng tỷ lệ phản hồi email từ 8% lên > 25%

---

## 1. Bối cảnh & Mục Tiêu Thiết Kế
FPT SmartBiz cung cấp phần mềm quản trị (ERP, CRM, HRM) cho doanh nghiệp vừa và lớn. Do trước đây gửi email đại trà, tỷ lệ phản hồi chỉ đạt 8%. Custom Skill `sales_followup` được xây dựng để nhận diện kết quả phân loại Lead BANT, tự động tạo email siêu cá nhân hóa dựa trên ngành nghề, chức danh và bài toán thất thoát nguyên liệu thực tế.

---

## 2. Cấu Trúc Custom Skill `sales_followup` (Nhiệm vụ 1)
Skill được thiết lập tại `skills/sales_followup/SKILL.md`:
* **Văn phong (Tone of Voice):**
  * *Tư vấn & Đồng cảm:* Thấu hiểu áp lực chi phí của lãnh đạo.
  * *Giá trị trực diện:* Nêu thẳng bài toán định lượng; độ dài dưới 100 từ/thư.
  * *CTA ma sát thấp:* Mời trao đổi 20 phút hoặc chia sẻ tài liệu hữu ích.
* **Khung sườn Email 3 Phân khúc:**
  * *Hot Lead:* Hook nỗi đau $\rightarrow$ Con số thiệt hại $\rightarrow$ Giải pháp ERP $\rightarrow$ Lịch hẹn Demo 1:1.
  * *Warm Lead:* Ghi nhận kế hoạch $\rightarrow$ Bằng chứng Case Study $\rightarrow$ Tặng tài liệu $\rightarrow$ Đối thoại mở.
  * *Disqualified:* Thừa nhận quy mô $\rightarrow$ Tặng file Excel định mức $\rightarrow$ Link công cụ dùng thử.

---

## 3. Quy Tắc Cá Nhân Hóa Động (Nhiệm vụ 2)
Tác tử tự động trích xuất và chèn 4 trường dữ liệu:
1. `{job_title}` & `{contact_name}`: Chức danh chuẩn (*Anh Nam - Tổng Giám đốc*).
2. `{company_context}`: Quy mô mạng lưới (*chuỗi 25 nhà hàng tại TP.HCM*).
3. `{pain_point}`: Điểm nghẽn nghiệp vụ (*thất thoát nguyên vật liệu tươi sống*).
4. `{quantified_benefit}`: Hiệu quả chứng minh (*cắt giảm 18% tỷ lệ hao hụt*).

---

## 4. Toàn Văn 3 Bức Thư Tiếp Cận Thực Tế (Nhiệm vụ 3)

### Thư 1: Hot Lead - Mời Hẹn Demo Giải Pháp 1:1
* **Khách hàng:** Anh Trần Hữu Nam - Tổng Giám đốc Chuỗi 25 Nhà hàng GoldenPot (TP.HCM).

```text
Tiêu đề: Kiểm soát hao hụt thực phẩm tươi cho chuỗi 25 nhà hàng GoldenPot

Kính gửi Anh Nam,

Chúc mừng chuỗi 25 nhà hàng GoldenPot đang phát triển rất tốt tại TP.HCM.

Điều hành chuỗi ẩm thực lớn, hẳn anh luôn trăn trở về bài toán thất thoát nguyên liệu tươi sống giữa kho tổng và điểm bán—thường bào mòn 3-5% lợi nhuận ròng.

FPT SmartBiz hiện có giải pháp ERP F&B kiểm soát định mức thời gian thực, giúp các chuỗi tương tự giảm 18% thất thoát sau 45 ngày.

Em mời Anh Nam tham gia buổi demo trực tuyến 20 phút sáng Thứ Năm để xem giải pháp dành riêng cho GoldenPot.

Lịch hẹn 9h30 sáng Thứ Năm có thuận tiện cho anh không ạ?

Trân trọng,
Nguyễn Hoàng Hải | FPT SmartBiz - 090x.xxx.xxx
```

### Thư 2: Warm Lead - Tặng Case Study Ngành F&B
* **Khách hàng:** Anh Lê Hoàng Minh - Tổng Giám đốc Chuỗi 25 Nhà hàng Bếp Quê (TP.HCM).

```text
Tiêu đề: Case Study: Chuỗi 30 nhà hàng giảm 18% thất thoát kho tươi sống

Kính gửi Anh Minh,

Được biết Bếp Quê đang lên kế hoạch tối ưu vận hành chuỗi 25 chi nhánh trong quý tới. Khi mở rộng, kiểm soát hao hụt thực phẩm tươi sống luôn là bài toán phức tạp nếu làm thủ công.

FPT SmartBiz vừa hoàn thiện báo cáo: "Quản trị Thất thoát F&B 2026", ghi lại lộ trình giúp chuỗi 30 nhà hàng tiết kiệm hơn 85 triệu đồng hao hụt mỗi tháng.

Em gửi tặng anh báo cáo tại: [fptsmartbiz.vn/case-study-fb-inventory]

Hy vọng tài liệu hữu ích cho Bếp Quê. Em sẵn lòng gửi thêm bảng tính ROI mẫu nếu anh cần.

Trân trọng,
Nguyễn Hoàng Hải | FPT SmartBiz
```

### Thư 3: Disqualified / Cold Lead - Tài Nguyên Dùng Thử Miễn Phí
* **Khách hàng:** Anh Nguyễn Văn Tuấn - Chủ Quán Cơm Niêu Tuấn Phát (1 cơ sở).

```text
Tiêu đề: Tặng anh Tuấn: File Excel kiểm soát chi phí thực phẩm quán ăn

Chào Anh Tuấn,

FPT SmartBiz nhận được thông tin anh quan tâm về phương pháp quản lý chi phí nhập thực phẩm.

Mô hình một điểm bán của anh sẽ phù hợp hơn với công cụ tinh gọn và miễn phí ban đầu:
1. File Excel tự động tính giá vốn món ăn (Food Cost) và định mức tiêu hao.
2. Tài khoản 30 ngày trải nghiệm phần mềm kho bán lẻ đám mây.

Anh có thể tải tại: [fptsmartbiz.vn/tai-nguyen-quan-ly-fb]

Chúc quán anh buôn may bán đắt!

Thân mến,
Ban Chăm sóc Doanh chủ - FPT SmartBiz
```

---

## 5. Cơ Chế Thúc Đẩy Tỷ Lệ Phản Hồi (> 25%)
1. **Tiêu đề trúng đích:** Nêu đúng thương hiệu và bài toán "thất thoát thực phẩm", nâng tỷ lệ mở thư từ 18% lên trên 45%.
2. **Nội dung nhắm trúng tài chính:** Đưa ra con số thiệt hại (3-5% lợi nhuận) và kết quả thực tế (tiết kiệm 85 triệu/tháng).
3. **Phân luồng thông minh:** Lead Hot được mời demo; Lead Warm nhận tri thức nuôi dưỡng; Lead nhỏ nhận tài nguyên hỗ trợ, đưa tỷ lệ phản hồi vượt mốc 25%.
