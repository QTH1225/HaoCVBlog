# 内容维护入口

网站内容现在直接从 Markdown 生成，无需修改 JavaScript 数组。本文件是维护说明，不会显示在网站上。

| 要修改的内容 | 文件 |
| --- | --- |
| 主页显示栏目与顺序 | [home.md](home.md) |
| 姓名、联系方式 | [profile.md](profile.md) |
| 教育背景与课程 | [education.md](education.md) |
| 技能 | [skills.md](skills.md) |
| 荣誉与奖项 | [honors-and-awards.md](honors-and-awards.md) |
| 论文 | [publications.md](publications.md) |
| 科研项目 | `projects/` 中每个项目一份 `.md` |
| 开源项目 | `open-source-projects/` 中每个项目一份 `.md` |
| 工作经历 | `work-experience/` 中每段经历一份 `.md` |
| 课外活动 | `extracurricular-activities/` 中每项活动一份 `.md` |
| 笔记 | 项目根目录的 `notes/` 中每篇一份 `.md` |

荣誉奖项在 `honors-and-awards.md` 中分三组维护：`## Scholarships`（奖学金）、`## Honors`（荣誉，含优秀毕业设计）、`## Competition Awards`（竞赛奖项）。每组保留 `Name`、`Date` 两列表头；首页各显示前三条，展开页显示全部。

联系方式在 [profile.md](profile.md) 中维护。删除某个联系方式字段的整行即可隐藏；要添加第五项或更多链接，在末尾的 `---` 后追加 `## Contacts`，下面每行写 `- [LinkedIn](https://www.linkedin.com/in/your-handle/)` 这样的 Markdown 链接。支持 HTTP(S)、`mailto:` 和 `tel:`。窄屏会根据文字宽度均衡换行，空间足够时三项同一行、四项 2＋2、五项 3＋2，末行居中。

编辑 [home.md](home.md) 即可控制主页显示哪些栏目，以及它们的先后顺序：删除一行就不显示该栏目，加回一行即可恢复，上下移动整行即可排序。只写需要显示的栏目，不必保留全部标识；重复或未知标识会停止构建并报告文件名。当前配置为：

```markdown
- education
- skills
- projects
- open-source-projects
- honors-and-awards
- publications
- notes
```

`projects` 对应科研项目，`open-source-projects` 对应开源项目。可选的 `work-experience` 和 `extracurricular-activities` 已从当前配置移除。删除配置行只移除主页栏目，原有内容及分类、详情页仍保留。栏目内条目排序由各篇文件的 `order` 控制；主页 NOTES 的打印隐藏规则不受位置影响。

可以先试改 [公路碳足迹项目](projects/highway-carbon-footprint.md)：

1. `title` 是项目名称，`dates` 是右侧时间，`order` 越小越靠前。
2. `## Summary` 下的列表用于主页和 View all 分类列表。
3. 其他内容是详情页正文，可以自由增减章节、图片、公式和链接。
4. 保存后在项目根目录运行 `npm run build`，再刷新预览。通过 `npm run dev` 启动服务时，保存内容会自动构建。

新增科研项目可复制 `templates/project.md` 到 `content/projects/my-project.md`，开源项目放到 `content/open-source-projects/my-project.md`；工作经历和活动分别有 `templates/work-experience.md`、`templates/activity.md`。模板不会自动出现在网站中，复制到对应内容目录才会生成页面。

科研项目和开源项目的首页摘要均按 `order` 最多显示三项，View all 分类页保留各自的全部项目。

文件名就是页面地址中的 id，使用小写英文、数字和连字符。网站统一使用英文，文档中的字段名请保留，字段值与正文可替换。

图片都使用 `![Image description](assets/images/your-image.png)`。行内公式使用 `$...$`，独立公式使用 `$$...$$`。更多字段、完整格式及运行命令见根目录[中文说明](../README.zh-CN.md)或 [English README](../README.md)。

PDF 放到 `assets/documents/`，正文写作 `[Open PDF](assets/documents/pdf-link-test.pdf)`，也可以使用完整 HTTPS 地址链接外部 PDF。路径从 `assets/` 开始，无需手写 `../../`。[测试笔记](../notes/media-math-test.md)第 7 节提供了可点击示例。只更新附件时运行 `npm run build` 后刷新。
