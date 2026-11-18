# Contract: Marketplace và plugin manifest

Theo mẫu đang chạy của `studio-director` (research R2). Mọi `version` phải bằng nhau và bằng mục mới
nhất trong `CHANGELOG.md`.

## `.claude-plugin/marketplace.json` (repo root)

```json
{
  "$schema": "https://anthropic.com/claude-code/marketplace.schema.json",
  "name": "image-prompt-packs",
  "description": "<1 câu>",
  "owner": {"name": "SEO Konic Team"},
  "plugins": [{
    "name": "image-prompt-pack",
    "source": "./plugins/image-prompt-pack",
    "description": "<1 câu>",
    "category": "productivity"
  }]
}
```

## `.agents/plugins/marketplace.json` (repo root)

```json
{
  "name": "image-prompt-packs",
  "interface": {"displayName": "Image Prompt Packs"},
  "plugins": [{
    "name": "image-prompt-pack",
    "source": {"source": "local", "path": "./plugins/image-prompt-pack"},
    "policy": {"installation": "AVAILABLE", "authentication": "ON_INSTALL"},
    "category": "Productivity"
  }]
}
```

## `plugins/image-prompt-pack/.claude-plugin/plugin.json`

Bắt buộc: `$schema` (`https://json.schemastore.org/claude-code-plugin-manifest.json`), `name`
(`image-prompt-pack`), `displayName`, `version`, `description`, `author`, `keywords`,
`"skills": "./skills/"`.

## `plugins/image-prompt-pack/.codex-plugin/plugin.json`

Bắt buộc: `name`, `version`, `description`, `author`, `keywords`, `"skills": "./skills/"`, và
`interface` gồm `displayName`, `shortDescription`, `longDescription` (tiếng Việt được), `developerName`,
`category` (`Productivity`), `capabilities` (`["Read", "Write"]`), `defaultPrompt` (2–3 câu ví dụ
tiếng Việt).

## Bất biến kiểm bằng máy

- Cả 4 file là JSON hợp lệ.
- `name` plugin giống nhau ở 4 file; `name` marketplace giống nhau ở 2 file marketplace.
- `version` ở 2 `plugin.json` bằng nhau và có trong tiêu đề mục mới nhất của `CHANGELOG.md`.
