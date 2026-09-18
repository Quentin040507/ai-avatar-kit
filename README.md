# AI 个人形象套件 · Quentin Liu

会挥手打招呼、眼睛跟着鼠标走的个人主页形象 —— 以及**让别人用一张照片复刻同款**的完整提示词。

## 直接看效果

- **完整主页（脱敏演示版）**：[homepage-demo.html](homepage-demo.html)
  - 开场：AI 生成的挥手打招呼动画，播完自动定格
  - 鼠标移动：形象会**转头 + 眼神追踪**光标方向
  - 联系方式已做脱敏替换（占位值）

## 这套形象是怎么做出来的

核心结论：**用一张自己的照片，走「动画电影」风格做图生图**，别走写实、别走 Q 版。

| 步骤 | 做法 |
|---|---|
| 1. 定脸 | 上传半身/正面清晰照 → 图生图，参考强度 ~0.7，风格词：`Pixar-style 3D animated character portrait` + `realistic adult proportions` |
| 2. 三个眼神 | 以定脸图为输入，只改最后一句：`Change ONLY the eye direction: ...to HIS LEFT / RIGHT / DOWN` |
| 3. 开场视频 | 先把人像放到 800×800 白底画布、只占 46% 宽，再图生视频（避免挥手时手被裁） |
| 4. 抠图 | floodfill 去背 → 统一画布 → 底部淡出 → WebP 压到 ~40KB/张 |
| 5. 挂到网页 | `pickGaze()` 按鼠标相对位置选眼神图 + 透视转头 `rotateY(∓9°)` |

完整提示词（中英文双版）、避坑清单、Python 后处理脚本都在 **[AI形象-提示词包.md](AI形象-提示词包.md)** 里，可以直接抄。

## 三个最贵的踩坑经验

1. **别写 `realistic / 写实`** —— 会漂回照片，失去插画感；
2. **别写 `chibi / Q版`** —— 会变成三头身手办；
3. **`Pixar-style` + `realistic adult proportions` 这对组合**才算命中：正常身形、大眼睛、光滑 CG 皮肤，同时保住本人面貌。

另外：生成视频时**务必给输入图留足四周空白**，否则挥手的手会被画面裁掉（这是返工过两次才解决的）。

---

Made by 刘全 Quentin Liu · 香港城市大学 数据科学

---

**在线体验**：https://quentin040507.github.io/ai-avatar-kit/

## ② 个人主页生成器（同学可直接用）

**https://quentin040507.github.io/ai-avatar-kit/make-yours.html**

打开后按引导三步走：上传简历（PDF / 粘贴文字）自动填内容 → 上传照片换成自己的形象 → 点「生成网页」下载单文件 HTML。纯前端、本机处理，不上传服务器。

