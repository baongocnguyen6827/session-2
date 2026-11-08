# Báo Cáo Chấm Điểm Sales Lead Tự Động Theo Khung BANT
**Đơn vị:** FPT SmartBiz | **Hệ thống:** Sales Lead Qualification Agent

### 1. Bối cảnh & Mục tiêu
FPT SmartBiz cung cấp phần mềm quản trị (ERP, CRM, HRM) cho khối doanh nghiệp vừa và lớn tại Việt Nam. Để tối ưu hóa quy trình sàng lọc và tiết kiệm thời gian cho đội ngũ Sales, hệ thống AI Agent được thiết lập nhằm tự động chấm điểm khách hàng tiềm năng theo khung BANT thang 100.

---

### 2. Thiết lập Ma trận Điểm số (Nhiệm vụ 1)
Tiêu chí chấm điểm chuẩn hóa được lưu tại `references/bant_scoring_matrix.json`:
* **Ngân sách (Budget - 30đ):** $\ge$ 200 triệu (30đ); 50 đến < 200 triệu (20đ); < 50 triệu (5đ).
* **Quyền hạn (Authority - 30đ):** C-Level / Chủ tịch / Giám đốc (30đ); Trưởng phòng / Quản lý (20đ); Nhân viên (5đ).
* **Nhu cầu (Need - 20đ):** Cấp bách hoặc rõ ràng (20đ); Đang tìm hiểu / tham khảo (10đ).
* **Thời gian (Timeline - 20đ):** Triển khai trong 1 tháng (20đ); trong 3 tháng (10đ); Chưa rõ (0đ).

---

### 3. Kịch bản Prompting Chuẩn Hóa (Nhiệm vụ 2)
```text
Bạn là AI Agent chấm điểm Lead tại FPT SmartBiz theo khung BANT (100đ):
- Budget: >=200tr (30đ), 50-<200tr (20đ), <50tr (5đ)
- Authority: C-Level/Giám đốc (30đ), Trưởng phòng (20đ), Nhân viên (5đ)
- Need: Cấp bách/rõ ràng (20đ), Đang tìm hiểu (10đ)
- Timeline: Trong 1 tháng (20đ), 3 tháng (10đ), Chưa rõ (0đ)
Phân loại: Hot Lead (>=80đ), Warm Lead (50-79đ), Cold Lead (<50đ).
Đầu ra:
Tổng điểm: [Điểm] / 100
Phân loại: [Hot / Warm / Cold Lead]
Đánh giá chi tiết:
- Ngân sách: [Điểm]đ. Lý do: [Giải thích]
- Quyền hạn: [Điểm]đ. Lý do: [Giải thích]
- Nhu cầu: [Điểm]đ. Lý do: [Giải thích]
- Thời gian: [Điểm]đ. Lý do: [Giải thích]
Đề xuất hành động: [Gợi ý cho Sales FPT SmartBiz]
```

---

### 4. Mã Nguồn Script Tự Động Hóa (`scripts/score_lead.py`)
```python
def score_lead(budget, role, need_urgent, months):
    b = 30 if budget >= 200e6 else (20 if budget >= 50e6 else 5)
    a = 30 if role == "c_level" else (20 if role == "manager" else 5)
    n = 20 if need_urgent else 10
    t = 20 if months <= 1 else (10 if months <= 3 else 0)
    score = b + a + n + t
    tier = "Hot Lead" if score >= 80 else ("Warm Lead" if score >= 50 else "Cold Lead")
    return score, tier
```

---

### 5. Kết Quả Thử Nghiệm 3 Leads Mẫu (Nhiệm vụ 3)

| Mã Lead | Khách hàng | Người liên hệ | B | A | N | T | Tổng | Phân loại | Đề xuất hành động |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **LEAD-001** | May mặc An Phú | CEO | 30 | 30 | 20 | 20 | **100** | **Hot Lead** | Senior AE gọi điện trong 2h, xếp lịch demo 1-1 |
| **LEAD-002** | MP Minh Long | Trưởng phòng KD | 20 | 20 | 20 | 10 | **70** | **Warm Lead** | Gửi tài liệu CRM, tư vấn và hỗ trợ lập tờ trình |
| **LEAD-003** | Thời trang GenZ | Thực tập IT | 5 | 5 | 10 | 0 | **20** | **Cold Lead** | Đưa vào email marketing tự động nuôi dưỡng |

---

### 6. Đánh Giá Mức Độ Hợp Lý
* **Tối ưu nguồn lực:** Phân loại chính xác giúp Sales tập trung vào khách hàng tiềm năng cao (LEAD-001 đạt 100đ), tránh lãng phí thời gian cho các lead chỉ khảo sát giá (LEAD-003).
* **Tính thực tế:** Khách hàng LEAD-002 (70đ) phản ánh đúng đặc thù Warm Lead: có ngân sách và nhu cầu cụ thể nhưng cần lộ trình quý và thẩm định thêm.
* **Tính mở rộng:** Mô hình dễ dàng tích hợp vào CRM hoặc mở rộng ngưỡng ngân sách theo từng gói dịch vụ.
