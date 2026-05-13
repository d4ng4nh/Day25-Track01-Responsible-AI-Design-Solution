# 1-diverge.md

## A. Sự cố thật liên quan

### A1 — Babylon Health / GP at Hand bỏ sót red-flag symptoms

- **Lens:** L1 — Cùng ngành healthcare / medical chatbot; L3 — Nhóm user dễ tổn thương
- **Tổ chức / sản phẩm:** Babylon Health / GP at Hand
- **Năm:** 2018–2021
- **Mô tả:** Babylon Health từng bị nhiều bác sĩ và báo chí chỉ ra các vấn đề an toàn trong symptom checker. Các thử nghiệm độc lập nêu lo ngại rằng ứng dụng có thể xử lý chưa đúng các tình huống red-flag như đau ngực, khó thở hoặc dấu hiệu đau tim.
- **Failure mode:** Escalation failure; under-triage; harmful advice
- **Root cause khả dĩ:** Không nhận diện ổn định các cụm triệu chứng nguy hiểm; thiếu rule escalation rõ khi user mô tả triệu chứng bằng ngôn ngữ đời thường.
- **Vì sao liên quan track:** Chatbot phòng khám của nhóm cũng phải nhận diện “tức ngực + khó thở + tê tay” và không được kéo user vào luồng đặt lịch thông thường.
- **Nguồn:**
  - TechCrunch — *AI chatbot maker Babylon Health attacks clinician in PR over safety concerns*: https://techcrunch.com/2020/02/25/first-do-no-harm/
  - Pulse Today — *Babylon launches 'troll' attack on doctor who tested AI app*: https://www.pulsetoday.co.uk/news/uncategorised/babylon-launches-troll-attack-on-doctor-who-tested-ai-app/
  - The Independent — *Regulator has concerns over symptom checker app*: https://www.independent.co.uk/news/health/nhs-symptom-checker-app-safety-complaints-b1813142.html
- **Mức tin cậy:** ✅ verified

### A2 — NEDA / Tessa chatbot đưa lời khuyên gây hại cho người rối loạn ăn uống

- **Lens:** L1 — Cùng ngành healthcare / mental health chatbot; L3 — Nhóm user dễ tổn thương
- **Tổ chức / sản phẩm:** National Eating Disorders Association / Tessa
- **Năm:** 2023
- **Mô tả:** NEDA phải gỡ chatbot Tessa sau khi có báo cáo chatbot đưa lời khuyên không phù hợp cho người có nguy cơ rối loạn ăn uống, như khuyến nghị hạn chế calo và theo dõi cân nặng.
- **Failure mode:** Harmful advice; failure to escalate; weak guardrails
- **Root cause khả dĩ:** Chatbot trả lời vượt vai trò an toàn; thiếu kiểm duyệt đầu ra; thiếu cơ chế chuyển người thật trong tình huống nhạy cảm.
- **Vì sao liên quan track:** Chatbot phòng khám không được tự đưa lời khuyên y tế, chẩn đoán, kê thuốc hoặc trấn an user sai trong tình huống có rủi ro.
- **Nguồn:**
  - The Guardian — *US eating disorder helpline takes down AI chatbot over harmful advice*: https://www.theguardian.com/technology/2023/may/31/eating-disorder-hotline-union-ai-chatbot-harm
  - AI Incident Database — Tessa incident: https://incidentdatabase.ai/cite/545/
- **Mức tin cậy:** ✅ verified

### A3 — Koko / GPT-3 mental health experiment thiếu minh bạch với user

- **Lens:** L1 — Mental health chatbot; L3 — Nhóm user dễ tổn thương
- **Tổ chức / sản phẩm:** Koko / GPT-3 co-pilot
- **Năm:** 2022–2023
- **Mô tả:** Koko dùng GPT-3 hỗ trợ soạn phản hồi cho khoảng 4.000 người dùng trong bối cảnh hỗ trợ tâm lý. Vấn đề chính là người dùng không được thông báo rõ rằng phản hồi có sự tham gia của AI, gây tranh cãi về consent và trust.
- **Failure mode:** Lack of transparency; trust miscalibration; escalation risk
- **Root cause khả dĩ:** Thiếu minh bạch về vai trò AI; thiếu thiết kế rõ về khi nào phải chuyển người thật trong tình huống tâm lý nhạy cảm.
- **Vì sao liên quan track:** User dùng Zalo/website chính thức của phòng khám có thể tưởng chatbot là nhân viên y tế thật. Cần disclosure rõ và escalation path khi có dấu hiệu nguy hiểm.
- **Nguồn:**
  - Ars Technica — *Controversy erupts over non-consensual AI mental health experiment*: https://arstechnica.com/information-technology/2023/01/contoversy-erupts-over-non-consensual-ai-mental-health-experiment/
  - Business Insider — *Company Using ChatGPT for Mental Health Support Raises Ethical Issues*: https://www.businessinsider.com/company-using-chatgpt-mental-health-support-ethical-issues-2023-1
  - AI Incident Database — Koko report: https://incidentdatabase.ai/reports/2910/
- **Mức tin cậy:** ✅ verified

### A4 — Character.AI bị Pennsylvania kiện vì chatbot giả làm bác sĩ

- **Lens:** L1 — Medical advice chatbot; L2 — Cùng failure mode escalation / harmful advice
- **Tổ chức / sản phẩm:** Character Technologies Inc. / Character.AI
- **Năm:** 2026
- **Mô tả:** Pennsylvania kiện Character.AI, cáo buộc một số chatbot trên nền tảng tự thể hiện như bác sĩ hoặc chuyên gia y tế được cấp phép, có thể khiến user tin rằng họ đang nhận tư vấn y tế chuyên nghiệp.
- **Failure mode:** Misrepresentation; harmful medical advice; failure to route user to qualified professional
- **Root cause khả dĩ:** Kiểm duyệt persona yếu; thiếu chặn vai trò y tế nguy hiểm; thiếu cơ chế chuyển hướng đến chuyên gia thật.
- **Vì sao liên quan track:** Chatbot phòng khám phải giữ ranh giới rõ: không giả làm bác sĩ, không chẩn đoán, không kê đơn, không đưa lời khuyên y khoa vượt phạm vi.
- **Nguồn:**
  - AP News — *Lawsuit accuses chatbot company of impersonating doctors*: https://apnews.com/article/character-ai-chatbots-medical-advice-pennsylvania-46502067ed5b3cd9f9173f194ad30070
  - Reuters — *Pennsylvania sues Character AI, says chatbot poses as doctors*: https://www.reuters.com/legal/litigation/pennsylvania-sues-character-ai-says-chatbot-poses-doctors-2026-05-05/
  - Pennsylvania Governor official statement: https://www.pa.gov/governor/newsroom/2026-press-releases/shapiro-administration-sues-character-ai-over-fake-medical-claim
- **Mức tin cậy:** ✅ verified

### A5 — ChatGPT Health under-triage emergency cases

- **Lens:** L1 — Healthcare AI triage; L3 — Người dùng có nguy cơ bị under-triage
- **Tổ chức / sản phẩm:** OpenAI / ChatGPT Health
- **Năm:** 2026
- **Mô tả:** Một nghiên cứu trên Nature Medicine đánh giá ChatGPT Health trong các kịch bản triage y tế và báo cáo rằng hệ thống under-triage hơn một nửa các ca mà bác sĩ xác định cần chăm sóc khẩn cấp. Mount Sinai cũng tóm tắt rằng công cụ có thể nhận ra dấu hiệu nguy hiểm trong phần giải thích nhưng vẫn đưa lời khuyên trấn an hoặc chờ đợi.
- **Failure mode:** Escalation failure; under-triage; misleading reassurance
- **Root cause khả dĩ:** Hệ thống nhận ra tín hiệu nguy hiểm nhưng không chuyển thành hành động escalation đúng; triage logic không đủ mạnh cho case mơ hồ.
- **Vì sao liên quan track:** Đây là case sát nhất với test set của nhóm: user có dấu hiệu nguy hiểm nhưng AI vẫn có thể khuyên chờ hoặc đặt lịch thay vì đi cơ sở y tế ngay.
- **Nguồn:**
  - Nature Medicine — *ChatGPT Health performance in a structured test of triage recommendations*: https://www.nature.com/articles/s41591-026-04297-7
  - Mount Sinai — *Research Identifies Blind Spots in AI Medical Triage*: https://www.mountsinai.org/about/newsroom/2026/research-identifies-blind-spots-in-ai-medical-triage
  - The Guardian — *ChatGPT Health fails to recognise medical emergencies*: https://www.theguardian.com/technology/2026/feb/26/chatgpt-health-fails-recognise-medical-emergencies
- **Mức tin cậy:** ✅ verified

### A6 — Người dùng cung cấp ít chi tiết hơn khi nghĩ đang nói với AI

- **Lens:** L1 — Healthcare AI triage; L3 — User dễ bị under-triage vì input thiếu; L4 — Liên quan bối cảnh chat/Zalo
- **Tổ chức / sản phẩm:** Nghiên cứu học thuật về symptom reporting với AI
- **Năm:** 2026
- **Mô tả:** Nghiên cứu cho thấy người dùng có xu hướng cung cấp mô tả triệu chứng ít chi tiết hơn khi họ nghĩ rằng thông tin sẽ được đọc bởi AI thay vì bác sĩ. Điều này làm tăng nguy cơ AI thiếu dữ liệu để nhận diện red-flag symptoms.
- **Failure mode:** Input deficiency; triage failure; human-computer interaction failure
- **Root cause khả dĩ:** User không tin AI hiểu được bối cảnh cá nhân; mô tả triệu chứng ngắn, mơ hồ, thiếu chi tiết.
- **Vì sao liên quan track:** Ở bối cảnh Zalo/website phòng khám, user có thể nhắn rất ngắn như “mệt”, “tức ngực nhẹ”, “khó thở chút”, khiến chatbot bỏ sót dấu hiệu nguy hiểm nếu không hỏi follow-up.
- **Nguồn:**
  - University of Würzburg — *Medical Information Provided to AI Is Often Incomplete*: https://www.uni-wuerzburg.de/en/news-and-events/news/detail/news/reis-nature-health/
  - News Medical — *People share incomplete details with AI in symptom reports*: https://www.news-medical.net/news/20260504/People-share-incomplete-details-with-AI-in-symptom-reports.aspx
  - SciTechDaily — *Study Reveals Dangerous Flaw in AI Symptom Checkers*: https://scitechdaily.com/study-reveals-dangerous-flaw-in-ai-symptom-checkers/
- **Mức tin cậy:** ✅ verified

### A7 — Chevrolet dealership chatbot bị prompt injection / thao túng

- **Lens:** L2 — Cùng failure pattern ở ngành khác
- **Tổ chức / sản phẩm:** Chevrolet dealership chatbot
- **Năm:** 2023
- **Mô tả:** User thao túng chatbot của đại lý xe để chatbot đồng ý các điều vượt thẩm quyền, như xác nhận bán xe với giá phi thực tế. Case này không thuộc y tế nhưng minh họa rủi ro chatbot chiều theo user khi thiếu guardrail.
- **Failure mode:** Prompt injection; sycophancy; failure to escalate abnormal request
- **Root cause khả dĩ:** Không có business rule hard stop; không nhận diện yêu cầu bất thường; không chuyển người thật khi vượt thẩm quyền.
- **Vì sao liên quan track:** Trong chatbot y tế, user cũng có thể ép: “đừng bắt tôi gọi cấp cứu, cứ cho tôi đặt lịch mai”. Chatbot phải overrule user pressure khi có red-flag symptoms.
- **Nguồn:**
  - Envive case study — *Chevy dealership AI chatbot*: https://www.envive.ai/post/case-study-chevy-dealerships-ai-chatbot
- **Mức tin cậy:** ⚠️ partial — dùng làm case phụ, không nên dùng làm luận cứ chính