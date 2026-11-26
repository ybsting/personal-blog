# 个人博客

一个使用 Astro 构建的个人博客。

运行命令：

```
npm run dev
```

个人博客网址：https://personal-blog.1300948078.workers.dev/

- 项目整体结构：

```text
                    index.astro
                         │
                         ▼
                  BaseLayout.astro
                         │
                ┌────────┴────────┐
                ▼                 ▼
         HomeCover.astro    PostList.astro
                                  │
                     ┌────────────┼────────────┐
                     ▼            ▼            ▼
                 PostItem     PostItem     PostItem
                     │            │            │
                     └────────────┼────────────┘
                                  │
                                  ▼
                         content/posts/*.md
```