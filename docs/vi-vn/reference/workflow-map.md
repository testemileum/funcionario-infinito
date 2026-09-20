---
title: "Sơ đồ workflow"
description: Tài liệu trực quan về các giai đoạn, quy trình và đầu ra của Funcionário Infinito
sidebar:
  order: 1
---

Funcionário Infinito (BMM) là một module trong hệ sinh thái Funcionário Infinito, tập trung vào các thực hành tốt nhất của kỹ nghệ ngữ cảnh và lập kế hoạch. AI agent hoạt động hiệu quả nhất khi có ngữ cảnh rõ ràng và có cấu trúc. Hệ thống BMM xây dựng ngữ cảnh đó theo tiến trình qua 4 giai đoạn riêng biệt. Mỗi giai đoạn, cùng với nhiều quy trình tùy chọn bên trong nó, tạo ra các tài liệu làm đầu vào cho giai đoạn kế tiếp, nhờ vậy agent luôn biết phải xây gì và vì sao.

Lý do và các khái niệm nền tảng ở đây đến từ các phương pháp Agile đã được áp dụng rất thành công trong toàn ngành như một khung tư duy.

Nếu có lúc nào bạn không chắc nên làm gì, skill `funcionario-help` sẽ giúp bạn giữ đúng hướng hoặc biết bước tiếp theo. Bạn vẫn có thể dùng trang này để tham chiếu, nhưng `funcionario-help` mang tính tương tác đầy đủ và nhanh hơn nhiều nếu bạn đã cài Funcionário Infinito. Ngoài ra, nếu bạn đang dùng thêm các module mở rộng Funcionário Infinito hoặc các module bổ sung khác, `funcionario-help` cũng sẽ mở rộng theo để biết mọi thứ đang có sẵn và đưa ra lời khuyên tốt nhất tại thời điểm đó.

Lưu ý quan trọng cuối cùng: mọi quy trình dưới đây đều có thể chạy trực tiếp bằng công cụ bạn chọn thông qua skill, hoặc bằng cách nạp agent trước rồi chọn mục tương ứng trong menu agent.

<iframe src="/workflow-map-diagram.html" title="Sơ đồ Workflow Map của Funcionário Infinito" width="100%" height="100%" style="border-radius: 8px; border: 1px solid #334155; min-height: 900px;"></iframe>

<p style="font-size: 0.8rem; text-align: right; margin-top: -0.5rem; margin-bottom: 1rem;">
  <a href="/workflow-map-diagram.html" target="_blank" rel="noopener noreferrer">Mở sơ đồ trong tab mới ↗</a>
</p>

## Giai đoạn 1: Phân tích (tùy chọn)

Khám phá không gian vấn đề và xác nhận ý tưởng trước khi cam kết đi vào lập kế hoạch. [**Tìm hiểu từng công cụ làm gì và nên dùng khi nào**](../explanation/analysis-phase.md).

| Quy trình | Mục đích | Tạo ra |
| ------------------------------- | -------------------------------------------------------------------------- | ------------------------- |
| `funcionario-brainstorming` | Động não ý tưởng dự án với sự điều phối của người dẫn dắt brainstorming | `brainstorming-report.md` |
| `funcionario-deep-recon` | Xác thực giả định hoặc lựa chọn giữa các phương án — soạn prompt cho công cụ nghiên cứu chuyên sâu của bạn, xử lý báo cáo của nó, hoặc nghiên cứu ngay tại đây; thị trường, miền nghiệp vụ, kỹ thuật, cạnh tranh, tiếng nói người dùng, học thuật; đã kiểm chứng, có trích dẫn, có thể làm mới | Báo cáo hoặc bản tóm tắt nghiên cứu + bản tóm tắt HTML tùy chọn |
| `funcionario-product-brief` | Ghi lại tầm nhìn chiến lược — phù hợp nhất khi concept của bạn đã rõ | `product-brief.md` |
| `funcionario-prfaq` | Working Backwards — stress-test và rèn sắc concept sản phẩm của bạn | `prfaq-{project}.md` |

## Giai đoạn 2: Lập kế hoạch

Xác định cần xây gì và xây cho ai.

| Quy trình | Mục đích | Tạo ra |
| --------------------------- | ---------------------------------------- | ------------ |
| `funcionario-prd` | Xác định yêu cầu (FR/NFR) | `PRD.md` |
| `funcionario-ux`            | Thiết kế trải nghiệm người dùng khi UX là yếu tố quan trọng | `DESIGN.md`, `EXPERIENCE.md` |
| `funcionario-spec`          | Chưng cất mọi đầu vào ý định (brief, PRD, bản ghi, ghi chú) thành hợp đồng `SPEC.md` súc tích + các tệp đi kèm — chốt CÁI GÌ trước CÁCH LÀM | `SPEC.md` + tệp đi kèm trong `{output_folder}/specs/spec-{slug}/` |

## Giai đoạn 3: Định hình giải pháp

Quyết định cách xây và chia nhỏ công việc thành các story.

| Quy trình | Mục đích | Tạo ra |
| ----------------------------------------- | ------------------------------------------ | --------------------------- |
| `funcionario-architecture` | Làm rõ các quyết định kỹ thuật | `architecture.md` kèm ADR |
| `funcionario-create-epics-and-stories` | Phân rã yêu cầu thành các phần việc có thể triển khai | Các file epic chứa các story |
| `funcionario-sprint-planning` | Cổng kiểm tra mức độ sẵn sàng trước khi triển khai, sau đó theo dõi story và xem trạng thái sprint | PASS/CONCERNS/FAIL + `sprint-status.yaml` |

## Giai đoạn 4: Triển khai

Mọi đầu vào triển khai đều hội tụ vào `funcionario-build`. Workflow này nhận ý định trực tiếp, issue, đặc tả hoặc story đã lập kế hoạch, rồi chọn mức làm rõ, lập kế hoạch, triển khai và review phù hợp.

| Quy trình | Mục đích | Tạo ra |
| -------------------------- | ------------------------------------------------------------------------ | -------------------------------- |
| `funcionario-build` | Biến ý định trực tiếp hoặc story đã lập kế hoạch thành mã nguồn đã triển khai và review | `spec-*.md` + mã nguồn |
| `funcionario-code-review` | Kiểm tra chất lượng phần triển khai | Được duyệt hoặc yêu cầu thay đổi |
| `funcionario-correct-course` | Xử lý thay đổi lớn giữa sprint | Kế hoạch cập nhật hoặc định tuyến lại |
| `funcionario-retrospective` | Review sau khi hoàn tất epic | Bài học rút ra |

### Đầu vào trực tiếp và đã lập kế hoạch

Công việc rõ ràng có thể đi thẳng vào `funcionario-build`. Sáng kiến lớn hơn có thể chuẩn bị PRD, UX, kiến trúc, epic, story, kiểm tra mức sẵn sàng và kế hoạch sprint trước. Các artifact này bổ sung ngữ cảnh, không chọn một workflow triển khai khác.

## Quản lý ngữ cảnh

Mỗi tài liệu sẽ trở thành ngữ cảnh cho giai đoạn tiếp theo. PRD cho architect biết những ràng buộc nào quan trọng. Tài liệu kiến trúc chỉ cho dev agent những mẫu cần tuân theo. File story cung cấp ngữ cảnh tập trung và đầy đủ cho việc triển khai. Nếu không có cấu trúc này, agent sẽ đưa ra quyết định thiếu nhất quán.

### Bối cảnh dự án

:::tip[Khuyến nghị]
Hãy tạo `project-context.md` để bảo đảm AI agent tuân theo quy tắc và sở thích của dự án. File này hoạt động như một bản hiến pháp cho dự án của bạn, nó dẫn dắt các quyết định triển khai xuyên suốt mọi quy trình. File tùy chọn này có thể được tạo ở cuối bước tạo kiến trúc, hoặc cũng có thể được sinh trong dự án hiện hữu để ghi lại những điều quan trọng cần giữ đồng bộ với quy ước đang có.
:::

**Cách tạo:**

- **Thủ công** — Tạo `_funcionario-output/project-context.md` với stack công nghệ và các quy tắc triển khai của bạn
- **Tự sinh** — Chạy `funcionario-generate-project-context` để sinh tự động từ architecture hoặc codebase

[**Tìm hiểu thêm về project-context.md**](../explanation/project-context.md)
