# Problem Discovery Report — MyCabin & DeliveryNote Reader

**Ngày lập:** 11/11/2026  
**Phạm vi:** Scan problem → ưu tiên vấn đề → 2 Problem Cards → quy trình nháp → phản biện  
**Nguyên tắc bằng chứng:** **[Theo mô tả]** = thông tin có trong đề bài, chưa phải kết quả khảo sát; **[Giả thuyết]** = nhận định cần kiểm chứng; **[Đề xuất]** = mục tiêu/thiết kế để nhóm thử nghiệm. Không coi KPI đề xuất là số liệu đã đo.

## 1. Scan problem

**Bốn lăng kính:** **Lặp lại** · **Tốn thời gian** · **Cần đọc, tổng hợp nhiều thông tin** · **Pain từ người khác**.

| # | Lăng kính | Job Story: Khi… tôi muốn… để… | Ai chịu ảnh hưởng? | Dấu hiệu thật (thời gian, tần suất, số người, bằng chứng) |
|---:|---|---|---|---|
| 1 | **Lặp lại**; **Tốn thời gian**; **Pain từ người khác** | **MyCabin:** Khi tôi bắt đầu lái một chiếc xe dùng chung và cấu hình khoang lái đã bị người trước thay đổi, tôi muốn khôi phục nhanh hồ sơ của mình, để đỡ thao tác lặp lại và tập trung vào việc lái xe. | Người lái trong gia đình/đội xe; người sử dụng trước và sau; đơn vị vận hành nếu có. | **[Theo mô tả]** Cần chỉnh lại ghế, gương, điều hòa, nhạc, bản đồ khi đổi người lái. **Chưa có bằng chứng định lượng** về số lần đổi người lái/tuần, số phút chỉnh mỗi lượt hay tỷ lệ người thấy phiền. **Cần đo:** nhật ký ≥20–30 lần đổi tài xế, thời gian từ lúc lên xe đến khi sẵn sàng chạy, số thao tác thủ công và phỏng vấn người dùng. |
| 2 | **Lặp lại**; **Tốn thời gian**; **Cần đọc, tổng hợp nhiều thông tin**; **Pain từ người khác** | **DeliveryNote Reader:** Khi tôi nhận phiếu giao hàng có mẫu và cách ghi khác nhau, tôi muốn chuyển toàn bộ dòng hàng thành dữ liệu chuẩn có thể kiểm tra nguồn, để không phải nhập từng dòng bằng tay và hạn chế sai sót cho kho/kế toán. | Thủ kho, kế toán, người kiểm duyệt, quản lý kho và bộ phận mua hàng. | **[Theo mô tả]** Khối khách sạn/nghỉ dưỡng nhận **hàng trăm phiếu/tháng**; phiếu có viết tắt, đơn vị không đồng nhất, chữ viết tay/chữ ký đè bảng. Đây là **quy mô được nêu trong đề**, chưa được xác minh tại một cơ sở. **Cần đo:** số phiếu/tháng, số dòng/phiếu, phút nhập và soát/phiếu, số lỗi phát hiện khi đối soát, tỷ lệ scan/ảnh/PDF text. |

**Nhận xét scan:** Cả hai đều có tác vụ lặp lại; **DeliveryNote Reader** có luồng xử lý dữ liệu và chỉ số chất lượng rõ hơn, còn **MyCabin** có điểm mạnh ở trải nghiệm cá nhân hóa nhưng phải chứng minh được *context-aware agent* tạo giá trị hơn preset đơn giản.

## 2. Problem Cards + quy trình nháp

### Bảng ưu tiên

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---:|---|---|---|
| **1** | **DeliveryNote Reader — nhập và chuẩn hóa dòng hàng từ phiếu giao hàng** | Job rõ, đầu vào/đầu ra hữu hạn, có thể xây golden set và chấm theo trường/dòng; human review giúp kiểm soát sai sót; không phải tích hợp hệ thống tồn kho thật. Phù hợp làm MVP và nghiên cứu hiệu quả IDP. | Dữ liệu tổng hợp có đại diện được tài liệu thực tế không? OCR chữ viết tay và bảng phức tạp đạt bao nhiêu? Mức giảm thời gian sau khi tính cả bước duyệt? |
| **2** | **MyCabin — khôi phục hồ sơ và gợi ý cấu hình theo ngữ cảnh** | Demo trực quan, có nhận diện on-device, trạng thái đa người dùng và chính sách an toàn; có tiềm năng minh họa agent học sở thích. | Pain đủ lớn không? Preset/chọn hồ sơ thủ công có giải quyết gần hết không? Có dữ liệu đủ đa dạng để kiểm tra nhận nhầm và đánh giá agent thực sự? Độ trễ trên thiết bị đích? |

**Giải thích thứ hạng:** Xếp theo khả năng *chứng minh lợi ích và đánh giá đầu-cuối* của MVP, **không** khẳng định DeliveryNote quan trọng hơn mọi bối cảnh. Nếu mục tiêu cuộc thi ưu tiên **AI Agent on-edge và cá nhân hóa tương tác**, MyCabin có thể được ưu tiên sau khi xác nhận giá trị so với preset.

### Problem Card #1 — DeliveryNote Reader

| Trường | Nội dung |
|---|---|
| **Job Story** | Khi nhận phiếu giao hàng từ nhiều nhà cung cấp với mẫu khác nhau, tôi muốn trích xuất **đủ từng dòng hàng** thành tên hàng, đơn vị, số lượng và bằng chứng trên trang, để nhanh chóng kiểm tra trước khi đưa sang bước đối chiếu tồn kho. |
| **Actor** | **Chính:** thủ kho nhập liệu và duyệt ngoại lệ. **Phối hợp:** kế toán kiểm tra bản ghi; quản lý kho theo dõi lỗi và năng suất. |
| **Thời điểm / bối cảnh** | Lúc tiếp nhận hàng; phiếu có thể là PDF text layer, scan, ảnh chụp, nhiều trang, bảng ngắt trang, có ghi tay hoặc chữ ký đè. |
| **Quy trình hiện tại (3–7 bước)** | (1) Nhận phiếu. (2) Mở/đọc thông tin và bảng hàng. (3) Gõ từng dòng vào file/hệ thống. (4) Chuẩn hóa tên hàng, đơn vị theo kinh nghiệm/danh mục. (5) Soát số lượng và lỗi đánh máy. (6) Chuyển danh sách đã kiểm tra cho kế toán/khâu đối chiếu tiếp theo. **[Giả thuyết quy trình]** Cần quan sát thực địa để xác nhận. |
| **Bottleneck (bước nào, mất bao nhiêu phút)** | Chủ yếu bước **(2)–(5)**: đọc bảng, nhận diện chữ viết tắt/viết tay, chuẩn hóa đơn vị và soát lại. **Phút/phiếu: chưa đo**; đề xuất bấm giờ theo loại phiếu, đo cả *thời gian duyệt đầu ra AI* để so sánh công bằng. |
| **Impact (nếu không giải thì sao)** | Nhập liệu tốn công, tăng độ trễ chuẩn bị dữ liệu, dễ sai số lượng/đơn vị hoặc bỏ sót dòng, kéo theo công việc sửa lỗi ở bước sau. **Mức tổn thất cụ thể: chưa có số liệu.** |
| **Success metric (baseline → target)** | **Thời gian hoàn thành/phiếu:** median thủ công chưa đo → **giảm ≥40%** kể cả duyệt (**[Đề xuất]**). **Row-level exact match:** chưa đo → **≥85%** *trước duyệt trên tập thử nghiệm theo phân tầng* (**[Đề xuất]**, cần điều chỉnh theo độ khó). **Confident-wrong:** chưa đo → **≤1%** số dòng được hệ thống tự đánh dấu đủ tin cậy, có ghi rõ mẫu số (**[Đề xuất]**). **Silent omission:** ghi nhận mọi sai lệch số dòng nghi ngờ, mục tiêu **0 trường hợp bỏ sót không gắn cảnh báo trên test set**. **Chi phí:** đo US$/trang và p95 thời gian xử lý; chưa ấn định nếu chưa biết cấu hình. |
| **Phương án không dùng AI** | Thống nhất biểu mẫu đầu vào với nhà cung cấp; dùng file Excel/Google Form/CSV mẫu; PDF text extraction + quy tắc regex cố định cho vài biểu mẫu ổn định; kiểm tra checklist và danh mục hàng hóa. |
| **Giả thuyết về AI (nếu có)** | Pipeline rẽ nhánh: PDF text → đọc trực tiếp; scan/ảnh → OCR + định vị bảng; mô hình hiểu bố cục **chỉ xác định vùng, hàng và trường**; code lấy nguyên văn từ kết quả nhận dạng, kiểm tra Pydantic/quy tắc và chỉ chuyển vùng bất định cho thủ kho. So sánh với parser quy tắc thuần túy. |
| **Cảm nhận nhanh** | **Workflow + AI extraction + HITL**. **Chưa cần agent tự chủ** cho MVP; chỉ nên gọi là *agent* nếu có lập kế hoạch chọn công cụ, khôi phục khi lỗi và được đánh giá so với workflow tĩnh. |

**Quy trình nháp hiện tại (as-is):**

```text
Nhà cung cấp giao hàng + phiếu (giấy/PDF/ảnh)
        ↓
Thủ kho mở phiếu, đọc phần đầu và từng dòng hàng
        ↓
Gõ tên hàng / đơn vị / số lượng vào bảng nhập liệu
        ↓
Tự chuẩn hóa tên viết tắt và quy đổi đơn vị nếu cần
        ↓
Đối chiếu lại với phiếu → sửa sai / hỏi nhà cung cấp
        ↓
Xuất danh sách đã kiểm tra cho bước đối chiếu tồn kho
```

**Luồng MVP đề xuất (to-be, tách biệt với hiện trạng):**

```text
PDF/ảnh/scan
    ↓
Phát hiện loại tài liệu ── PDF text ──→ Trích xuất text + tọa độ
    │
    └── Scan/ảnh ────────────────→ OCR + định vị bảng/dòng
                                        ↓
                                 Chuẩn hóa cấu trúc dòng
                                        ↓
                          Code kiểm tra số học/đơn vị,
                        gắn evidence box + confidence
                                        ↓
                         Đối chiếu số dòng phát hiện
                                        ↓
                      Có nghi ngờ? ── Có ──→ Thủ kho duyệt
                           │                         │
                         Không                       ↓
                           └──────────────→ Kế toán xem/xuất CSV, JSON
                                         (chưa đối chiếu tồn kho)
```

**Ranh giới MVP cần giữ:** chỉ xử lý **phiếu công khai hoặc tự sinh**, không dùng chứng từ thật; đọc và chuẩn bị dữ liệu, **không** thực hiện đối chiếu tồn kho; giữ ảnh/vùng nguồn bên cạnh từng trường; dùng code để chuẩn hóa đơn vị, số học và đối chiếu số dòng. Tạo **golden set 50–150 phiếu** có nhãn từng dòng, các trường và trường hợp không đọc được, phân tách bố cục chưa từng thấy để đánh giá khả năng tổng quát hóa. Cần báo cáo `n`, sai số theo kiểu phiếu, field accuracy, row exact match, row recall, confident-wrong, tỷ lệ qua thẳng không duyệt, thời gian và US$/trang.

### Problem Card #2 — MyCabin

| Trường | Nội dung |
|---|---|
| **Job Story** | Khi bắt đầu sử dụng xe chung với người khác, tôi muốn xe nhận đúng danh tính và khôi phục các lựa chọn cá nhân, đồng thời đề xuất tinh chỉnh theo ngữ cảnh mà tôi có thể chấp nhận/từ chối, để chuẩn bị lái nhanh mà vẫn an toàn. |
| **Actor** | **Chính:** người lái đã đăng ký. **Phối hợp:** người dùng chưa đăng ký/khách, người quản trị hồ sơ; hành khách khi ngữ cảnh thay đổi. |
| **Thời điểm / bối cảnh** | Khi lên xe/trước khi xe di chuyển, hoặc khi thời tiết/giờ/ngữ cảnh chuyến đi thay đổi. Camera/âm thanh có thể nhiễu, offline; cơ cấu ghế/gương chỉ **giả lập**. |
| **Quy trình hiện tại (3–7 bước)** | (1) Người lái lên xe. (2) Nhận thấy cấu hình của người trước. (3) Điều chỉnh ghế/gương. (4) Chỉnh điều hòa, nhạc và hệ thống dẫn đường. (5) Bắt đầu hành trình, đôi khi tiếp tục tinh chỉnh. **[Giả thuyết quy trình]** Cần quan sát và phỏng vấn trên xe dùng chung. |
| **Bottleneck (bước nào, mất bao nhiêu phút)** | Bước **(3)–(4)**: nhiều thao tác nhỏ; thêm rủi ro phân tâm nếu tiếp tục chỉnh khi xe đang chạy. **Phút/lượt: chưa đo**, đo trên từng cặp người lái và số thao tác, không suy diễn từ mô tả. |
| **Impact (nếu không giải thì sao)** | Bất tiện khi đổi người lái, trải nghiệm thiếu nhất quán; có khả năng phân tâm nếu thao tác trong khi chạy. Chưa có chứng cứ rằng việc này gây tai nạn hoặc tạo tổn thất tài chính định lượng. |
| **Success metric (baseline → target)** | **Thời gian sẵn sàng lái:** chưa đo → **giảm ≥50%** so với tự chỉnh (**[Đề xuất]**). **Độ chính xác nhận diện & chống nhận nhầm:** đo recognition accuracy, **FAR/FRR và unknown-user rejection** theo từng điều kiện sáng/ồn → mục tiêu sẽ chốt sau pilot; không lấy độ chính xác tổng để thay FAR. **Độ trễ:** đo p50/p95 từ nhận diện đến hiển thị cấu hình → **p95 ≤2 s trên thiết bị demo** (**[Đề xuất]**). **Offline:** 100% luồng nhận diện–preset–duyệt cơ bản chạy khi ngắt mạng. **An toàn:** 100% lệnh mô phỏng cơ khí qua rule guard + HITL trước áp dụng; **0 lệnh trái chính sách trong bộ ca kiểm thử**. **Giá trị agent:** acceptance rate của gợi ý theo ngữ cảnh và thời gian so với preset tĩnh; mục tiêu phải đặt sau đo baseline. |
| **Phương án không dùng AI** | Chọn hồ sơ bằng nút/tài khoản/PIN/chìa khóa; lưu preset ghế, gương, điều hòa, nhạc; lịch trình và quy tắc IF–THEN theo giờ/thời tiết; yêu cầu xác nhận mọi thao tác cơ khí. |
| **Giả thuyết về AI (nếu có)** | Face recognition hoặc speaker verification **on-device** giúp truy xuất đúng hồ sơ; recommender nhẹ học từ quyết định chấp nhận/từ chối theo giờ/thời tiết/người đồng hành; một agent có state chọn **đề xuất**, gọi tool mô phỏng và ghi preference memory; **code guard** quyết định lệnh được phép, không giao an toàn cho LLM. |
| **Cảm nhận nhanh** | **Workflow + Rule Guard + AI recognition** cho chức năng cơ bản; **Agent** chỉ có giá trị tăng thêm ở gợi ý theo ngữ cảnh/học sở thích và cần A/B test với preset tĩnh. |

**Quy trình nháp hiện tại (as-is):**

```text
Người A lái xe, để lại cấu hình A
         ↓
Người B lên xe dùng chung
         ↓
Người B tự chỉnh ghế/gương → điều hòa → nhạc/bản đồ
         ↓
Người B kiểm tra thấy phù hợp, bắt đầu lái
         ↓
Lần sau lại phải chỉnh nếu người khác đã đổi cấu hình
```

**Luồng MVP đề xuất (to-be, tách biệt với hiện trạng):**

```text
Camera / mic on-device
         ↓
Nhận diện + đánh giá ngưỡng tin cậy / anti-spoof cơ bản
         ↓
Tin cậy thấp hoặc người lạ? ── Có ──→ Chọn hồ sơ/PIN thủ công
         │                                      │
       Không                                    │
         └──────────────┬───────────────────────┘
                        ↓
                 Nạp preset cá nhân
                        ↓
          Thu thập ngữ cảnh được phép sử dụng
                        ↓
            Đề xuất tinh chỉnh (có lý do)
                        ↓
       Guard xác định: trạng thái xe/quyền/giới hạn
                        ↓
       Cơ khí: bắt buộc HITL → áp dụng trên mô phỏng
       Phi cơ khí: áp dụng theo quyền & xác nhận phù hợp
                        ↓
             Ghi feedback tối thiểu on-device
```

**Ranh giới MVP cần giữ:** mô phỏng ghế/gương và trạng thái xe thay vì điều khiển CAN thật; **không tự di chuyển cơ cấu cơ khí khi chưa xác nhận**; mẫu sinh trắc được mã hóa tại thiết bị và có cơ chế xóa/thu hồi; chế độ **offline**; thiết lập quy trình consent; đo RAM/VRAM, CPU/GPU, p95 latency và nếu có lượng tử hóa thì so sánh Q4–Q8 **trên cùng tập đánh giá**, không chỉ so kích thước file. Không suy ra khả năng chạy trên ECU/Jetson sản xuất từ benchmark trên laptop.

### Card muốn pitch nhất

- **Card số:** **#1 — DeliveryNote Reader** (theo tiêu chí *đủ rõ để xây MVP, kiểm chứng tác động và công bố benchmark*).
- **Vì sao:** Đầu vào/đầu ra xác định được, có baseline thủ công, measurable quality/cost/time, dễ tách phần AI cần thiết khỏi rule; giao diện review chứng minh phối hợp người–máy. Có thể làm rõ điểm khác biệt ở **không bỏ sót dòng hàng âm thầm, evidence từng dòng, calibrated abstention và thích ứng bố cục mới** thay vì chỉ demo OCR.
- **Câu hỏi muốn nhóm phản biện:** (1) Trên tập bố cục chưa từng thấy, hệ thống có giảm **thời gian tổng cộng gồm cả duyệt** không? (2) Cơ chế nào phát hiện dòng bị OCR bỏ qua, thay vì chỉ nhận diện sai những dòng đã thấy? (3) Lợi ích còn bao nhiêu nếu so với PDF parser + regex + form mẫu, không dùng LLM? (4) Benchmark tổng hợp có đủ giá trị thực tế khi chưa được dùng chứng từ thật không?

**Phương án pitch nếu tiêu chí chấm tập trung vào edge/agent:** Có thể chọn **#2 — MyCabin**, nhưng cần chứng minh *agent theo ngữ cảnh tốt hơn preset + luật* qua thí nghiệm đối chứng và chỉ sử dụng phần cứng/mô phỏng đúng quyền kiểm soát.

### AI đã phản biện card thế nào

| Điểm yếu AI chỉ ra | Đồng ý? | Đã sửa gì |
|---|---|---|
| **DeliveryNote:** “Hàng trăm phiếu/tháng” là số trong đề, chưa phải pain được xác nhận bằng phỏng vấn hay đo thời gian. | **Có.** | Gắn nhãn **[Theo mô tả]**, để baseline thời gian/lỗi là **chưa đo**; bổ sung kế hoạch khảo sát thực địa và đo cả thời gian duyệt. |
| **DeliveryNote:** Golden set 50–150 phiếu tự sinh có thể làm kết quả quá đẹp, thiếu handwriting và layout lạ. | **Có.** | Yêu cầu nhãn theo dòng, phân tầng độ khó, giữ layout chưa thấy làm test, báo cáo `n` theo nhóm; không suy diễn độ chính xác trên phiếu thật. |
| **DeliveryNote:** OCR có thể **bỏ mất cả dòng** mà confidence của dòng đã trích vẫn cao. | **Có, rất quan trọng.** | Thêm bước đếm dòng/nghi ngờ thiếu dòng, vùng nguồn và cơ chế chuyển những trường hợp không khớp cho người duyệt; đo *row recall* và *silent omission* riêng. |
| **DeliveryNote:** Chưa chứng minh LLM/agent tốt hơn phương án rule-based rẻ hơn. | **Có.** | Bổ sung baseline PDF text + regex + template; định nghĩa MVP là **workflow + AI extraction + HITL**, chỉ thêm agent nếu có lợi ích có thể đo. |
| **MyCabin:** Khôi phục preset không nhất thiết cần AI Agent; chọn hồ sơ thủ công có thể đủ. | **Có.** | Tách **preset cơ bản** và **gợi ý ngữ cảnh**; đánh giá thêm tỷ lệ chấp nhận/công sức so với preset tĩnh, thay vì coi nhận diện là đóng góp agent. |
| **MyCabin:** Sinh trắc bị nhận nhầm, giả mạo hoặc dùng sai mục đích; lệnh cơ khí là nhạy cảm về an toàn. | **Có, rất quan trọng.** | Thêm unknown-user rejection, fallback thủ công, lưu template mã hóa on-device, quyền xóa dữ liệu, hard-coded safety guard và HITL cho **mọi** lệnh cơ khí mô phỏng. |
| **MyCabin:** Benchmark laptop GPU không đại diện phần cứng ô tô; lượng tử hóa có thể làm giảm nhận diện. | **Có.** | Yêu cầu báo rõ thiết bị, RAM/VRAM, p95 latency, offline, Q4/Q8 cùng tập dữ liệu và không khẳng định production-ready. |
| **Cả hai:** KPI mục tiêu đang là giả thuyết; không nên dùng như kết quả đã chứng minh. | **Có.** | Đánh dấu **[Đề xuất]**, để baseline là **chưa đo** và nêu rõ phép đo trước/sau cùng điều kiện. |

---

## Dữ liệu tối thiểu cần thu thập để chốt problem–solution fit

| Chủ đề | Quan sát/phỏng vấn tối thiểu | Baseline cần ghi | Tiêu chí quyết định tiếp tục |
|---|---|---|---|
| **DeliveryNote Reader** | Phỏng vấn thủ kho/kế toán; thử với vài loại phiếu **được phép dùng**, hoặc mô phỏng hợp pháp nếu không tiếp cận chứng từ thật; phân tích lỗi theo nhóm layout. | Thời gian nhập+soát/phiếu, số dòng/phiếu, sai sót, tỷ lệ phiếu khó, thời gian duyệt đầu ra mô hình. | Giảm được tổng thời gian với chất lượng sau duyệt đạt yêu cầu; không có lỗi bỏ sót âm thầm trong benchmark; sai lệch và chi phí minh bạch. |
| **MyCabin** | Quan sát nhiều lần chuyển tài xế trên xe dùng chung có đồng ý; phỏng vấn xem phiền hà thật hay chỉ là điểm “nice-to-have”; thí nghiệm trong nhiều điều kiện ánh sáng/ồn. | Thời gian chỉnh và số tương tác/lượt, frequency đổi người, độ chính xác preset thủ công; acceptance rate của gợi ý tĩnh. | Người dùng thật thấy ích lợi đo được; nhận diện có cơ chế từ chối người lạ; mọi thao tác cơ khí đi qua xác nhận và guard; gợi ý ngữ cảnh có uplift so với rule/preset. |

**Kết luận:** **Ưu tiên pitch DeliveryNote Reader** nếu cần một đề tài IDP có benchmark chặt và thành quả đo được trong MVP. **Giữ MyCabin làm lựa chọn mạnh** khi muốn thể hiện AI on-edge, personal memory và agent có tương tác, với điều kiện chứng minh pain và uplift so với cấu hình preset không AI.
