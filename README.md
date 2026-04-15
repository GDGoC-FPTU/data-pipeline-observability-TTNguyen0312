[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573951&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** trongtiennew@gmail.com | 26ai.tiennt@vinuni.edu.vn
**Name:** Nguyễn Trọng Tiến

---

## Mo ta

(Mo ta ngan gon bai lab va nhung gi ban da lam)
Bài lab này xây dựng một ETL pipeline tự động để xử lý dữ liệu sản phẩm, đồng thời so sánh kết quả agent đưa ra khi truy xuất dữ liệu sạch và dữ liệu rác.

Các bước đã thực hiện:
- Viết solution.py (ETL pipeline), bao gồm:
    - **Extract:** Viết function đọc dữ liệu thô từ json
    - **Validate:** Lọc bỏ các item có giá (price) <= 0 hoac thiếu category.
    - **Transform:** Chuẩn hóa các category Title Case, tính `discounted_price` (giảm 10% theo công thức), thêm timestamp `processed_at`.
    - **Load:** Xuất dữ liệu sạch ra file `processed_data.csv`.
- Chạy file generate_garbage.py để tạo bộ dữ liệu rác
- **Stress Test:** Chạy agent simulation với hai bộ dữ liệu (clean vs garbage) để so sánh kết quả và phân tích tác động của chất lượng dữ liệu đối với đầu ra của agent.
- Viết báo cáo.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Mo ta cach ban chay thi nghiem Clean vs Garbage data
```
- Chạy python solution.py để tạo bộ dữ liệu sạch (processed_data.csv)
- Chạy python generate_garbage.py để tạo bộ dữ liệu rác (garbage_data.csv)
- Khi đã có đủ hai bộ dữ liệu, chạy python agent_simulation.py để xem so sánh.
- Ghi lại kết quả vào experiment_report.md


---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

(Tom tat ket qua: bao nhieu records da xu ly, bao nhieu bi loai, v.v.)
Khi chạy solution.py, có tổng cộng 5 records đã được xử lý, trong đó có 3 records valid, 2 records lỗi:
Validation complete. Valid: 3, Errors: 2
