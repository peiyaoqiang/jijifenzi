# Notes: 做题平台改造

## 当前任务
- 题目内容来源：`知识点.txt`
- 需要题型：选择题、填空题、简答题
- 约束：题目和答案不要做太强变形；简答题直接按标准答案作答；点击“显示答案”后可直接查看答案

## 初始判断
- 很可能是前端静态页面 + 静态 JS 题库
- 更稳妥的方式是把 `知识点.txt` 整理成结构化题库，而不是在浏览器里临时解析文本

## 已完成
- 在 `coverage-data.js` 追加固定题库 `window.questionBank`，共 48 题。
- 保留 `window.knowledgePoints` 作为知识库展示数据来源。
- `index.html` 改为基于固定题库筛选、组卷、提交、错题复习。
- 每题新增“显示答案”按钮，可直接查看标准答案与完整知识点。
- 简答题取消关键词命中判定，改为直接展示标准答案，提交时只做参考对照。

## 验证
- `node -e "global.window={}; require('./coverage-data.js'); console.log(window.knowledgePoints.length, window.questionBank.length);"` 输出 `100 48`
- `node -e "const fs=require('fs'); const html=fs.readFileSync('index.html','utf8'); const m=html.match(/<script>\s*([\s\S]*)<\/script>\s*<\/body>/); new Function(m[1]);"` 通过，说明 `index.html` 内联脚本语法正常
