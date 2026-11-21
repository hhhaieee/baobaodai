# 百宝袋（星星夜剧插件仓库）

这是「星星夜剧」App 的「百宝袋」在线插件仓库。把插件信息登记到 `index.json` 后，
App 内「模块 › 百宝袋」即可拉取并安装。

## 使用方式

1. 把插件打包成两个文件：`manifest.json` 与 `main.js`。
2. 将这两个文件放到一个 GitHub 仓库的某个 tag（例如 `v1.0.0`）下。
3. 在 `index.json` 的 `modules` 数组里追加一条记录，填写插件的 id、名称、版本、
   所在仓库（`owner/repo`）、tag，以及 `manifest.json` / `main.js` 的 SHA-256 校验值。
4. 提交后，App 内「模块 › 百宝袋」刷新即可看到。**同一个 id 只会显示最新版本**，
   因此上传新版本时直接新增一条更高 `version` 的记录即可，旧版本无需删除。

## index.json 字段说明

```json
{
  "format": 1,
  "modules": [
    {
      "id": "example",
      "name": "示例插件",
      "version": "1.0.0",
      "description": "插件说明",
      "api": 1,
      "adult": false,
      "repo": "owner/repo",
      "tag": "v1.0.0",
      "sha256": {
        "manifest.json": "64位SHA-256十六进制",
        "main.js": "64位SHA-256十六进制"
      }
    }
  ]
}
```

- `format` 固定为 `1`。
- `id` 只能是小写字母、数字、`-`、`_`，且以字母或数字开头，最长 32 位。
- `version` 使用三段式 `x.y.z`。
- `repo` 填写 `owner/repo`，不含 `https://github.com/` 前缀。
- `tag` 必须是 `v` + 三段式版本号（如 `v1.0.0`）。
- `sha256` 为两个文件的 SHA-256 值，App 下载后据此校验完整性。
