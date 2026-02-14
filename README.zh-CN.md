# AI 代码审查器

AI 代码审查器是一个 GitHub Action，它利用 OpenAI 的 GPT-4 API 为您的拉取请求提供智能反馈和建议。这个强大的工具通过自动化代码审查过程，帮助提高代码质量并节省开发人员的时间。

## 功能

- 使用 OpenAI 的 GPT-4 API 审查拉取请求。
- 提供智能评论和建议以改进您的代码。
- 过滤掉与指定排除模式匹配的文件。
- 易于设置并集成到您的 GitHub 工作流程中。

## 设置

1. 要使用此 GitHub Action，您需要一个 OpenAI API 密钥。如果您没有，请在 [OpenAI](https://beta.openai.com/signup) 注册一个 API 密钥。

2. 将 OpenAI API 密钥作为 GitHub Secret 添加到您的仓库中，名称为 `OPENAI_API_KEY`。您可以在[此处](https://docs.github.com/en/actions/reference/encrypted-secrets)找到有关 GitHub Secrets 的更多信息。

3. 在您的仓库中创建一个 `.github/workflows/main.yml` 文件并添加以下内容：

```yaml
name: AI Code Reviewer

on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: AI Code Reviewer
        uses: your-username/ai-code-reviewer@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # GITHUB_TOKEN 默认存在，因此您只需保持原样，无需将其添加为 secret，否则会报错。 [更多详情](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          OPENAI_API_MODEL: "gpt-4" # 可选：默认为 "gpt-4"
          exclude: "**/*.json, **/*.md" # 可选：用逗号分隔的排除模式
```

4. 将 `your-username` 替换为您的 GitHub 用户名或组织名称，即 AI Code Reviewer 仓库所在的位置。

5. 如果您想忽略某些文件模式不进行审查，请自定义 `exclude` 输入。

6. 提交更改到您的仓库，AI Code Reviewer 将开始处理您未来的拉取请求。

## 工作原理

AI Code Reviewer GitHub Action 检索拉取请求的差异，过滤掉排除的文件，并将代码块发送到 OpenAI API。然后，它根据 AI 的响应生成审查评论并将其添加到拉取请求中。

## 贡献

欢迎贡献！请随时提交问题或拉取请求以改进 AI Code Reviewer GitHub Action。

请让维护者生成最终包 (`yarn build` & `yarn package`)。

## 许可证

本项目采用 MIT 许可证。有关更多信息，请参阅 [LICENSE](LICENSE) 文件。