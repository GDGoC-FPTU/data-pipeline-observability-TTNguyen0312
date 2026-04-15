# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600228
**Name:** Nguyễn Trọng Tiến
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200. | 10 | Return the item of the highest price |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 10 | Return the item of the highest price |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent trả lời sai khi dùng Garbage Data vì dữ liệu đầu vào chưa qua xử lý, chứa nhiều vấn đề ảnh hưởng trực tiếp đến chất lượng đầu ra:

1. **Duplicate IDs:** ID `1` xuất hiện hai lần (Laptop và Banana) — vi phạm tính toàn vẹn của dữ liệu, gây nhầm lẫn cho agent khi xử lý hoặc tra cứu theo ID.

2. **Wrong data types:** Sản phẩm "Broken Chair" có giá là `"ten dollars"` (chuỗi ký tự) thay vì số nguyên/thực. Khi agent cố tính toán hoặc so sánh giá, trường này sẽ gây lỗi hoặc bị bỏ qua, làm méo mó kết quả.

3. **Outlier nghiêm trọng:** "Nuclear Reactor" với giá `999999` là một giá trị bất thường (outlier) trong danh sách sản phẩm thông thường. Agent không có khả năng tự phát hiện outlier, nên nó chọn đây là "best choice" vì đây là mức giá cao nhất (thuật của agent tìm item có giá trị "price" cao nhất).

4. **Null values:** Bản ghi "Ghost Item" thiếu cả `id` lẫn `category`, khiến agent không thể phân loại hoặc xử lý đúng sản phẩm này.

5. **Dữ liệu không liên quan:** "Banana" (trái cây, giá $2) lẫn trong danh sách electronics/furniture, sai ngữ cảnh nghiệp vụ, làm nhiễu loạn logic lựa chọn của agent.

Tóm lại, agent hoạt động đúng logic của nó (chọn sản phẩm giá cao nhất), nhưng vì bộ dữ liệu rác không được làm sạch trước, đầu ra trở nên vô nghĩa và không đáng tin cậy.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** (Dong y hay khong? Giai thich ngan gon.)

**Đồng ý.** Qua thí nghiệm này, có thể thấy rõ rằng dù agent được thiết kế với logic đúng đắn và prompt rõ ràng, kết quả đầu ra vẫn hoàn toàn sai lệch khi dữ liệu đầu vào kém chất lượng. Do prompt dù tốt đến mấy cũng chỉ là chuỗi hướng dẫn, giúp agent hiểu và làm đúng nhiệm vụ, nhưng không thể đảm bảo đầu ra luôn đúng nếu đầu vào (bộ dữ liệu tham chiếu) không chính xác, sai, thiếu, hoặc bị nhiễu, trong khi nếu dữ liệu được sạch thì agent sẽ luôn đảm bảo được kết quả đầu ra đáng tin cậy dù prompt chỉ ở mức cơ bản

Do đó, trong một hệ thống AI/data pipeline thực tế, đảm bảo chất lượng dữ liệu (data quality) phải là ưu tiên hàng đầu, trước cả việc tối ưu hóa prompt.
