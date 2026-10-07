# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- **Họ và tên:** Đinh Thị Minh Tâm
- **MSSV / mã học viên:** 2A202602433
- **Lớp:** Track 1
- **Ngành đã chọn:** Mobility / Autonomous Driving

## 1. Industry Risk Snapshot

> Các mức Thấp / Trung bình / Cao dưới đây là đánh giá định tính phục vụ bài tập, không phải kết luận phân loại pháp lý.

| Nội dung | Đánh giá | Lý do |
|---|---|---|
| **Harm chính** | **Cao** | Failure của hệ thống có thể dẫn đến va chạm, thương tích hoặc tử vong. Ngoài physical harm còn có thể có thiệt hại tài sản, gián đoạn dịch vụ và suy giảm niềm tin vào hệ thống tự động. |
| **Mức độ high-stakes** | **Cao** | ADS đưa ra hoặc hỗ trợ các quyết định trong môi trường giao thông theo thời gian thực. Một quyết định sai về nhận diện vật thể, dự đoán quỹ đạo hoặc hành động tránh va chạm có thể tạo hậu quả khó đảo ngược. |
| **Dữ liệu nhạy cảm** | **Trung bình – Cao** | Hệ thống có thể xử lý dữ liệu vị trí, lộ trình, camera, lidar/radar, telemetry và dữ liệu hành vi di chuyển. Một số dữ liệu có khả năng tiết lộ vị trí và thói quen của người dùng. |
| **Nhu cầu human review** | **Cao** | Trong thử nghiệm, incident review, edge case và tình huống hệ thống không đủ khả năng xử lý, cần cơ chế con người giám sát hoặc can thiệp. Human review cũng cần thiết ở cấp tổ chức để đánh giá safety metrics, incident reports và quyết định triển khai. |

---

## 2. Case study 1 — Uber ATG self-driving crash tại Tempe, Arizona (2018)

### Brief Case

- **Tổ chức / sản phẩm AI:** Uber Advanced Technologies Group (Uber ATG) — developmental Automated Driving System (ADS).
- **Thời gian, địa điểm / bối cảnh:** 18/3/2018, Tempe, Arizona, Hoa Kỳ. Xe thử nghiệm Volvo XC90 được Uber ATG trang bị ADS đang vận hành trên đường công cộng với một vehicle operator ngồi ở ghế lái.
- **AI được dùng để làm gì:** ADS thực hiện các chức năng nhận biết môi trường, theo dõi các đối tượng trên đường, dự đoán chuyển động và điều khiển xe trong quá trình thử nghiệm tự động.
- **Vấn đề hoặc sự kiện đáng chú ý:** ADS phát hiện người đi bộ trước va chạm nhưng không phân loại chính xác người này là pedestrian và không dự đoán đúng quỹ đạo. Khi hệ thống xác định va chạm sắp xảy ra, tình huống đã vượt quá response specifications của hệ thống phanh. Thiết kế của hệ thống không cho emergency braking tự động kích hoạt để giảm thiểu va chạm mà dựa vào vehicle operator can thiệp. Operator đã nhìn khỏi đường trong thời gian dài và chỉ nhìn trở lại khoảng 1 giây trước va chạm. Người đi bộ tử vong.
- **Số liệu có nguồn:**
  - ADS phát hiện người đi bộ **5,6 giây trước va chạm**.
  - Xe đang di chuyển khoảng **45 mph** khi tiến gần khu vực xảy ra va chạm.
  - Operator nhìn trở lại đường khoảng **1 giây trước impact**.
  - Xe va chạm với người đi bộ ở khoảng **39 mph**.
  - **1 người đi bộ tử vong**.
- **Nguồn:** National Transportation Safety Board (NTSB), Investigation HWY18MH010 — *Collision Between Vehicle Controlled by Developmental Automated Driving System and Pedestrian*, Tempe, Arizona.
- **Phân biệt bằng chứng và nhận định:**
  - **Fact có nguồn:** ADS phát hiện pedestrian 5,6 giây trước impact nhưng không phân loại chính xác hoặc dự đoán đúng đường đi; operator bị mất tập trung; người đi bộ tử vong. NTSB cũng xác định inadequate safety risk assessment, ineffective oversight of vehicle operators và thiếu cơ chế xử lý automation complacency là các yếu tố góp phần.
  - **Analysis của tôi:** Đây không nên được xem đơn thuần là “Model error”. Model/perception có đóng góp vào failure, nhưng safety design và human oversight cũng là những yếu tố quan trọng dẫn tới hậu quả.
  - **Failure mode gần nhất theo taxonomy của slide:** **Over-reliance**. Operator được kỳ vọng giám sát ADS nhưng đã không duy trì sự chú ý cần thiết; NTSB cũng đề cập vấn đề automation complacency.
  - **Layer chính:** **Safety**. Model/perception là contributing layer vì ADS không phân loại và dự đoán chính xác pedestrian, nhưng safety mechanisms và cơ chế human intervention đã không ngăn được hậu quả.

### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| **High-risk moment** | Khoảnh khắc ADS đã phát hiện một đối tượng trên đường nhưng không nhận diện và dự đoán chính xác pedestrian, trong khi operator không theo dõi đầy đủ môi trường lái xe và hệ thống không tự kích hoạt emergency braking để giảm thiểu va chạm. |
| **Stakeholder bị ảnh hưởng** | **Trực tiếp:** người đi bộ và vehicle operator. **Gián tiếp:** Uber ATG, cơ quan quản lý, các road users khác và cộng đồng sử dụng đường công cộng nơi xe tự hành được thử nghiệm. |
| **Failure mode** | **Over-reliance** là mode gần nhất trong taxonomy của slide. Operator phải đóng vai trò giám sát nhưng đã không duy trì sự chú ý. NTSB đồng thời chỉ ra Uber ATG thiếu cơ chế thích hợp để xử lý automation complacency. |
| **Layer bắt đầu lỗi** | **Safety — layer chính.** Hệ thống dựa vào operator để can thiệp và emergency braking không được kích hoạt để giảm thiểu va chạm. **Model — contributing layer:** ADS theo dõi pedestrian nhưng không phân loại và dự đoán đường đi chính xác. Tôi không quy toàn bộ sự cố cho Model vì kết luận của NTSB cho thấy failure mang tính hệ thống rộng hơn. |
| **Harm xảy ra là gì?** | **Harm đã xảy ra:** một người đi bộ bị xe thử nghiệm va chạm và tử vong. Đây là observed harm, không phải harm giả định. Ngoài ra, sự cố còn tạo rủi ro đối với operator và các road users xung quanh. |
| **Harm lens** | **Injury** — tổn hại thể chất nghiêm trọng dẫn đến tử vong. |
| **Severity** | **Critical.** Hậu quả trực tiếp là tử vong, thuộc nhóm hậu quả thể chất đặc biệt nghiêm trọng và không thể đảo ngược. |
| **Scale** | **Low đối với observed harm của riêng sự kiện này:** một pedestrian chịu hậu quả trực tiếp và operator không bị thương. Tuy nhiên, failure liên quan đến quy trình thử nghiệm ADS trên đường công cộng nên potential scale có thể rộng hơn nếu cùng loại weakness xuất hiện ở nhiều lần thử nghiệm. Không có đủ dữ liệu trong case này để định lượng số người có thể bị ảnh hưởng. |
| **Probability** | **Chưa đủ dữ liệu để đánh giá.** Một crash đơn lẻ không cho phép suy ra xác suất failure cho mỗi chuyến đi, mỗi kilomet hay mỗi tình huống pedestrian encounter. Không tự đặt tỷ lệ phần trăm khi nguồn không cung cấp denominator phù hợp. |
| **Frequency** | **Chưa đủ dữ liệu để đánh giá.** NTSB mô tả và điều tra sự kiện cụ thể này nhưng dữ liệu trong case không đủ để xác định failure tương tự xảy ra với tần suất Low / Medium / High trong toàn bộ hoạt động của Uber ATG. |
| **Vì sao?** | NTSB xác nhận pedestrian fatality, thời gian detection 5,6 giây, tốc độ xe và hành vi của operator. NTSB cũng xác định inadequate safety risk assessment, ineffective oversight và thiếu mechanisms addressing automation complacency là contributing factors. Vì vậy tôi đánh giá severity là Critical nhưng không suy luận probability hay frequency từ một sự kiện duy nhất. |

---

## 3. Case study 2 — Cruise driverless vehicle và sự cố pedestrian ngày 2/10/2023

### Brief Case

- **Tổ chức / sản phẩm AI:** Cruise LLC — Cruise Automated Driving System (ADS), bao gồm Collision Detection Subsystem.
- **Thời gian, địa điểm / bối cảnh:** 2/10/2023, trong hoạt động driverless của Cruise trên đường công cộng tại California.
- **AI được dùng để làm gì:** Cruise ADS điều khiển xe không có human driver. Collision Detection Subsystem có nhiệm vụ phát hiện collision và lựa chọn post-collision response, chẳng hạn dừng tại chỗ hoặc pull over khỏi luồng giao thông.
- **Vấn đề hoặc sự kiện đáng chú ý:** Một phương tiện do con người điều khiển trước tiên va chạm với pedestrian và đẩy người này vào đường đi của Cruise AV. Cruise AV phanh nhưng vẫn tiếp xúc với pedestrian. Sau khi ban đầu dừng lại, ADS xác định không chính xác collision là một lateral collision và ra lệnh cho xe thực hiện pull-over thay vì giữ nguyên vị trí. Hành động này khiến pedestrian bị kéo về phía trước.
- **Số liệu có nguồn:**
  - Pedestrian bị Cruise vehicle kéo khoảng **20 feet** trước khi xe dừng hoàn toàn.
  - Safety recall 23E-086 liên quan tới **950 ADS units** sử dụng Collision Detection Subsystem.
  - NHTSA ghi nhận estimated percentage with defect trong recall population là **100%**; con số này mô tả software population thuộc recall, **không có nghĩa 950 xe đều đã gây sự cố**.
  - **2 crash reports** liên quan sự cố ngày 2/10 không mô tả đầy đủ post-crash behavior.
  - Cruise sau đó sửa đổi thêm **4 reports** khác để bổ sung thông tin.
  - NHTSA consent order năm 2024 gồm monetary penalty **1,5 triệu USD**.
- **Nguồn:**
  - National Highway Traffic Safety Administration (NHTSA), *Part 573 Safety Recall Report 23E-086*, 7/11/2023.
  - NHTSA, *Consent Order with Cruise After Company Failed to Fully Report Crash Involving Pedestrian*, 30/9/2024.
  - California Department of Motor Vehicles, *DMV Statement on Cruise LLC Suspension*, 24/10/2023.
- **Phân biệt bằng chứng và nhận định:**
  - **Fact có nguồn:** Một human-driven vehicle va chạm với pedestrian trước và đẩy người này vào đường đi của Cruise AV. Cruise ADS sau đó inaccurately characterized collision as a lateral collision và ra lệnh pull over; pedestrian bị kéo khoảng 20 feet trước khi xe dừng hoàn toàn. Safety recall 23E-086 bao phủ 950 ADS units.
  - **Fact có nguồn về governance:** NHTSA xác định hai crash reports không cung cấp đầy đủ post-crash details. California DMV đình chỉ deployment permit và driverless testing permit của Cruise ngày 24/10/2023.
  - **Analysis của tôi:** Case thể hiện đồng thời technical safety failure và governance/transparency problem. Tuy nhiên Harm Map dưới đây tập trung vào **high-risk moment của ADS ngay sau collision**, thay vì trộn hai failure thành một.
  - **Failure mode gần nhất theo taxonomy của slide:** **Escalation failure**. Sau một tình huống collision đặc biệt nghiêm trọng, hệ thống vẫn lựa chọn và thực hiện một post-collision maneuver không phù hợp thay vì chuyển sang trạng thái an toàn là giữ xe đứng yên.
  - **Layer chính:** **Safety**. **Model** là contributing layer vì ADS đã inaccurately characterized collision.

### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| **High-risk moment** | Sau khi Cruise AV đã va chạm và ban đầu dừng lại với pedestrian ở vị trí thấp phía dưới/ở đường đi của xe, Collision Detection Subsystem phải quyết định post-collision response. Hệ thống lại lựa chọn pull-over thay vì giữ xe stationary. |
| **Stakeholder bị ảnh hưởng** | **Trực tiếp:** pedestrian nằm trong đường đi của Cruise AV. **Gián tiếp:** các road users xung quanh, Cruise, cơ quan quản lý và cộng đồng nơi driverless vehicles được vận hành. |
| **Failure mode** | **Escalation failure** là mode gần nhất trong taxonomy của slide. Đây không phải escalation theo nghĩa chatbot chuyển cuộc trò chuyện cho nhân viên, mà là failure tương đương trong bối cảnh autonomous driving: khi tình huống đã vượt sang trạng thái safety-critical sau collision, hệ thống tiếp tục một automated maneuver thay vì chuyển sang safe state phù hợp. |
| **Layer bắt đầu lỗi** | **Safety — layer chính:** post-collision protection không đưa xe về phản ứng an toàn phù hợp trong tình huống này. **Model — contributing layer:** hồ sơ recall cho biết ADS inaccurately characterized collision as a lateral collision, từ đó ra lệnh pull-over. |
| **Harm xảy ra là gì?** | **Observed event:** pedestrian bị Cruise vehicle kéo khoảng 20 feet sau khi xe ban đầu đã dừng. Nguồn chính thức cho biết post-collision response này có thể làm tăng risk of injury. Tôi không khẳng định mức độ thương tích bổ sung cụ thể do đoạn kéo này gây ra vì nguồn được sử dụng không định lượng riêng phần injury đó. |
| **Harm lens** | **Injury** — physical harm đối với pedestrian và nguy cơ làm tăng mức độ injury sau collision. |
| **Severity** | **High.** Sự kiện liên quan trực tiếp đến pedestrian ở dưới/ở đường đi của một phương tiện và xe tiếp tục chuyển động sau collision. Tôi không xếp Critical vì các nguồn đang sử dụng không cung cấp đủ dữ liệu để quy riêng mức thương tích nghiêm trọng nhất cho hành vi pull-over của Cruise. |
| **Scale** | **Low đối với observed event:** một pedestrian trực tiếp liên quan đến case ngày 2/10. **Medium đối với potential system exposure:** recall bao phủ 950 ADS units có cùng Collision Detection Subsystem. Tuy nhiên 950 units bị recall không đồng nghĩa 950 sự cố đã xảy ra. |
| **Probability** | **Chưa đủ dữ liệu để định lượng.** Recall report mô tả đây là tình huống có thể xảy ra trong một số circumstances và tài liệu chronology mô tả scenario được xem là hiếm, nhưng không cung cấp denominator đủ để tính probability cho mỗi chuyến đi hoặc collision. |
| **Frequency** | **Chưa đủ dữ liệu để đánh giá nhất quán Low / Medium / High từ riêng case này.** Có ít nhất một incident xác nhận liên quan trực tiếp đến defect, nhưng số ADS units trong recall chỉ phản ánh population cần remedy, không phải số lần failure đã xảy ra. |
| **Vì sao?** | NHTSA recall xác nhận logic post-collision có thể khiến Cruise AV pull over thay vì đứng yên và xác nhận ADS inaccurately characterized collision trong sự cố 2/10. NHTSA sau đó xác nhận pedestrian bị kéo khoảng 20 feet. Vì hậu quả liên quan trực tiếp tới physical safety, severity được đánh giá High. Tuy nhiên không có đủ denominator để tự suy ra probability hoặc frequency. |

---

## 4. Nhận xét chung sau hai case

Hai case cho thấy rủi ro của AI trong autonomous driving không chỉ đến từ độ chính xác của model.

- Trong **Uber ATG**, perception limitation xảy ra cùng với safety design, human oversight và automation complacency.
- Trong **Cruise**, việc nhận định sai đặc điểm collision ảnh hưởng đến post-collision response, trong khi incident reporting và transparency sau sự cố cũng trở thành một vấn đề governance.
- Vì đây là hệ thống high-stakes, chỉ cải thiện model accuracy là chưa đủ. Hệ thống còn cần fail-safe behavior, human oversight phù hợp, incident monitoring, transparent reporting và quy trình đánh giá safety trước và sau deployment.
- Severity, probability và frequency cần được đánh giá độc lập. Một case có hậu quả Critical không đồng nghĩa failure đó có probability hoặc frequency cao.

## 5. Nguồn tham khảo

1. **National Transportation Safety Board (NTSB).** Investigation HWY18MH010 — *Collision Between Vehicle Controlled by Developmental Automated Driving System and Pedestrian*, Tempe, Arizona, March 18, 2018.
2. **National Highway Traffic Safety Administration (NHTSA).** Part 573 Safety Recall Report 23E-086 — Cruise LLC, submitted November 7, 2023.
3. **National Highway Traffic Safety Administration (NHTSA).** *NHTSA Announces Consent Order with Cruise After Company Failed to Fully Report Crash Involving Pedestrian*, September 30, 2024.
4. **California Department of Motor Vehicles.** *DMV Statement on Cruise LLC Suspension*, October 24, 2023.