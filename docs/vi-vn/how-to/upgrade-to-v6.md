---
title: "Cách nâng cấp lên v6"
description: Di chuyển từ Funcionário Infinito v4 sang v6
sidebar:
  order: 3
---

Sử dụng trình cài đặt Funcionário Infinito để nâng cấp từ v4 lên v6, bao gồm khả năng tự động phát hiện bản cài đặt cũ và hỗ trợ di chuyển.

## Khi nào nên dùng

- Bạn đang dùng Funcionário Infinito v4 (thư mục `.funcionario-method`)
- Bạn muốn chuyển sang kiến trúc v6 mới
- Bạn có các planning artifact hiện có cần giữ lại

:::note[Điều kiện tiên quyết]
- Node.js 20.12+
- Bản cài đặt Funcionário Infinito v4 hiện có
:::

## Các bước thực hiện

### 1. Chạy trình cài đặt

Làm theo [Hướng dẫn cài đặt](./install-funcionario.md).

### 2. Xử lý bản cài đặt cũ

Khi v4 được phát hiện, bạn có thể:

- Cho phép trình cài đặt sao lưu và xóa `.funcionario-method`
- Thoát và tự xử lý dọn dẹp thủ công

Nếu trước đây bạn đặt tên thư mục Funcionário Infinito khác - bạn sẽ phải tự xóa thư mục đó.

### 3. Dọn dẹp skill IDE cũ

Tự xóa các command/skill IDE cũ của v4 - ví dụ nếu bạn dùng Claude Code, hãy tìm các thư mục lồng nhau bắt đầu bằng `funcionario` và xóa chúng:

- `.claude/commands/`

Các skill v6 mới sẽ được cài tại:

- `.claude/skills/`

### 4. Di chuyển planning artifacts

**Nếu bạn có tài liệu lập kế hoạch (Brief/PRD/UX/Architecture):**

Di chuyển chúng vào `_funcionario-output/planning-artifacts/` với tên mô tả rõ ràng:

- Tên tệp PRD nên chứa `PRD`
- Tên tệp tương ứng nên chứa `brief`, `architecture`, hoặc `ux-design`
- Tài liệu đã chia nhỏ có thể đặt trong các thư mục con đặt tên phù hợp

**Nếu bạn đang lập kế hoạch dở dang:** Hãy cân nhắc bắt đầu lại với workflow v6. Bạn vẫn có thể dùng các tài liệu hiện có làm input - các workflow discovery tiên tiến trong v6, kết hợp web search và chế độ plan trong IDE, cho kết quả tốt hơn.

### 5. Di chuyển công việc phát triển đang dở dang

Nếu bạn đã có các story được tạo hoặc đã triển khai:

1. Hoàn thành cài đặt v6
2. Đặt `epics.md` hoặc `epics/epic*.md` vào `_funcionario-output/planning-artifacts/`
3. Chạy workflow `funcionario-sprint-planning` của Scrum Master
4. Nói rõ với SM những epic/story nào đã hoàn thành

## Bạn nhận được gì

**Cấu trúc thống nhất của v6:**

```text
du-an-cua-ban/
├── _funcionario/               # Thư mục cài đặt duy nhất
│   ├── _config/         # Các tùy chỉnh của bạn
│   │   └── agents/      # Tệp tùy chỉnh agent
│   ├── core/            # Framework core dùng chung
│   ├── bmm/             # Module Funcionário Infinito
│   ├── bmb/             # Funcionário Infinito Builder
│   └── cis/             # Creative Intelligence Suite
└── _funcionario-output/        # Thư mục output (là thư mục docs trong v4)
```

## Di chuyển module

| Module v4 | Trạng thái trong v6 |
| --- | --- |
| `.funcionario-2d-phaser-game-dev` | Đã được tích hợp vào module BMGD |
| `.funcionario-2d-unity-game-dev` | Đã được tích hợp vào module BMGD |
| `.funcionario-godot-game-dev` | Đã được tích hợp vào module BMGD |
| `.funcionario-infrastructure-devops` | Đã bị ngừng hỗ trợ - agent DevOps mới sắp ra mắt |
| `.funcionario-creative-writing` | Chưa được điều chỉnh - module v6 mới sắp ra mắt |

## Các thay đổi chính

| Khái niệm | v4 | v6 |
| --- | --- | --- |
| **Core** | `_funcionario-core` thực chất là Funcionário Infinito | `_funcionario/core/` là framework dùng chung |
| **Method** | `_funcionario-method` | `_funcionario/bmm/` |
| **Config** | Sửa trực tiếp các tệp | `config.yaml` theo từng module |
| **Documents** | Cần thiết lập trước cho bản chia nhỏ hoặc nguyên khối | Linh hoạt hoàn toàn, tự động quét |
