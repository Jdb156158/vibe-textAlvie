# 制作与部署

## 影片

来源和分镜见 [treatment.md](../film/treatment.md)，完整提示词见 [PROMPTS.md](PROMPTS.md)。

1. 核对 Lucian 245 / 307 / 327 / 357 / 378 的源码与运行状态，改写中文教学文案。
2. 使用确定性 Canvas draw(t)，保持五张 Bento 卡身份，按章节放大演示。
3. 九帧检查，修复解码末字归位，缩短粒子迁移并增加结果停留；加入 GitHub 图标和地址。
4. Python 合成 120 BPM / 2/4 拍配乐和操作音，章节对齐小节，结尾收束淡出。
5. Playwright 导出 1,200 帧，FFmpeg 编码 H.264 Main / yuv420p + AAC、faststart、每秒关键帧。
6. 抽取实际 MP4 帧并验证完整播放、跳转。详见 [影片 QA](../film/QA.md)。

```sh
cd film
npm install
python3 make_audio.py
npm run stills
npm run render
sh encode.sh
```

需要 Node.js、Python 3 + numpy、Chrome、FFmpeg；非 macOS 请设置 CHROME_PATH。

## 交互网页

网页由原生 HTML / CSS / JavaScript 实现，配色、中文示例和图形与影片一致。实际输入驱动 DOM 字符与 Canvas 粒子，切换控件时清理计时器。影片时间轴仅用于制作与预览。

解码使用固定字格；打字只有一个可取消的任务；故障短暂触发且自动模式默认关闭；感应字重按响应式元素实际位置计算；粒子使用弹簧回归目标字形，静止后停止刷新。减少动态模式直接给出结果。

## GitHub Pages

发布到 main 分支根目录，保留 .nojekyll。网页地址：https://jdb156158.github.io/vibe-textAlvie/ 。
