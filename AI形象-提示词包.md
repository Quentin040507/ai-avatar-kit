# AI 形象复刻提示词包 v1

> 这套东西的效果：**上传一张自己的照片 → 生成一个"皮克斯动画主角"质感的数字形象 → 放进个人主页会跟着鼠标转头/转眼珠**。
> 全程不需要炼 LoRA、不需要 PS，只要会用即梦或任意支持图生图的工具。

---

## 0. 这套效果长什么样

风格定位：**不是 Q 版，不是写实照片**。是"正常成年身形 + 略大的眼睛 + 光滑 CG 皮肤"的动画电影主角感——比照片年轻精致，但五官发型还是本人。

- 看得出来是你（保留了眉眼、脸型、发型）
- 脸又不会老、不会有毛孔痘印（CG 皮肤）
- 眼神灵动（这也是后面能做"鼠标追踪"的前提）

---

## 1. 第一步：选一张什么样的照片（很重要）

| 要求 | 说明 |
|---|---|
| 正面、半身或大头照 | 侧脸/全身会让 AI 乱猜脸型 |
| 光线均匀、背景干净 | 背景杂乱会污染的人物概念（推荐白墙/纯色背景） |
| 五官清晰无遮挡 | 不戴墨镜口罩、别戴帽子遮住发型 |
| 分辨率 ≥ 800px | 太小会糊，AI 补出来的脸就不像你了 |
| 表情自然放松 | 参考图的表情会"遗传"给你的数字形象 |

> 我自己用的是 iPhone 正面棚拍半身照（西装 + 黑T），效果最好。

---

## 2. 第二步：基础形象提示词（核心）

这一步的作用是**定脸**。后面所有变体都基于这张图，千万不能每张重新文生图（那样会变成随机帅哥）。

### 2.1 英文版（通用，推荐用于 Pixar 风效果最好的工具）

```
Pixar-style 3D animated character portrait of the young East Asian man in the reference photo. Animated film hero look: smooth stylized CG skin, big expressive glossy brown eyes with large catchlights, soft rounded stylized features, sculpted wavy black hair, gentle smile. Realistic adult proportions, handsome and charismatic. Dark charcoal blazer over black crew-neck tee, thin silver chain. Simple warm gray gradient background, waist-up, facing camera, cinematic soft lighting, high quality 3D render, no text, no watermark
```

### 2.2 即梦中文版

```
皮克斯风格 3D 动画角色：正常成年身形（绝对不是 Q 版、不是三头身），保留照片本人清晰的五官、脸型和发型；光滑的 CG 皮肤质感，眼睛略大且带有明显高光，眉眼柔和精致，面带自然的微笑。穿搭：深炭灰色西装外套，内搭黑色圆领上衣，脖颈一条细银项链。浅灰白色干净背景，半身正面构图，柔和影棚布光，超高清画质，无文字无水印。
```

### 2.3 参数设置（以即梦为例）

- 模式：**图生图**（上传你的照片）
- 参考强度：选"人物特征"，强度调到 **7 成左右**（太高=直接变照片，太低=不像你）
- 比例：竖版 **3:4**
- 生成数量：一次多出几张，挑最像的一张作为"母版"

> ⚠️ **母版概念**：挑出来的那张图，是后面所有眼神变体唯一的老祖宗。存好它。

---

## 3. 第三步：三个眼神变体（做"鼠标追踪"用）

提示词模板（把后半段的方位换掉就能得出另外两张）：

```
Identical image, absolutely everything stays exactly the same: same Pixar-style 3D character, same young East Asian man, same face, same dark charcoal blazer and black crew-neck, same silver chain, same pose, same camera angle, same framing, same white background. Change ONLY the eye direction: his irises and pupils shift to gaze to HIS LEFT (toward the viewer's left), head stays completely still facing forward, no other change at all
```

三个版本只改最后半句：

| 变体 | 结尾指令 |
|---|---|
| 看左 | `his irises and pupils shift to gaze to HIS LEFT (toward the viewer's left)` |
| 看右 | `his irises and pupils shift to gaze to HIS RIGHT (toward the viewer's right)` |
| 看下 | `his irises and pupils shift downward as if looking down at something below him` |

关键点：**输入图必须是第 2 步挑出来的母版**，且参考强度拉到最高（保脸优先于一切）。

> 💡 中文工具替换用法：`这张图完全不变，只改变眼神方向：眼珠和瞳孔转向（他自己的左侧/右侧/下方），头部保持正对前方完全不动，其他一切严禁改变。`

---

## 4. 第四步：五个刹路口诀（不看不知道，看了少踩一堆坑）

### ❌ 千万别写的词

| 词 | 后果 |
|---|---|
| `realistic` / `semi-realistic` / `写实` / `超写实` | 图生图会被你的原照片拽回照片风，萌度全无 |
| `Q版` / `chibi` / `二头身` / `Q-version` | 变手办玩偶，根本不像你 |
| `photorealistic skin texture` | 毛孔痘印一起回来 |

### ✅ 必须写的词（命中 ANN-style 动画感的关键）

```
Pixar-style 3D animated character portrait  +  realistic adult proportions
```

就这两个组合：前者负责"动画 CG 皮肤/大眼/干净"，后者负责"不许 Q 版"。缺任何一个都会跑偏。

### 🎚 两个旋钮

- **想更像本人** → 参考强度调高（0.8–1.0），但可能偏照片
- **想更精致/更 cartoon** → 参考强度调低（0.5–0.7），代价是不太像你

我最终落点是：**中等保真度 + Pixar-style 关键词**，既有辨识度又不显老。

### 🔒 脸会不会变？

会，除非你遵守铁律：
**所有变体都拿同一张母版图做图生图，绝不重新文生图，也绝不换 Pose/穿搭描述。**

---

## 5. 第五步：后处理（可选，做网页/贴纸用）

生成完通常要处理三件事：去背景、去水印、压体积。

### 5.1 去背景（纯 Python，无需 PS）

```python
from PIL import Image, ImageDraw, ImageFilter

im = Image.open('你的图.png').convert('RGB')
w, h = im.size
work = im.copy()
# 从四角泛洪填充抠背景（阈值按背景干净程度调：干净 18，杂乱 28）
for pt in [(2,2),(w-3,2),(2,h-3),(w-3,h-3),(w//2,2)]:
    try: ImageDraw.floodfill(work, pt, (255,0,255), thresh=18)
    except Exception: pass

mask = Image.new('L', (w,h), 0); mp = mask.load(); px = work.load()
for y in range(h):
    for x in range(w):
        r,g,b = px[x,y]
        if r>200 and b>200 and g<80: mp[x,y] = 255      # 被填成品红的=背景
mask = Image.eval(mask, lambda v: 255-v)                 # 取反：人=白
mask = mask.filter(ImageFilter.MaxFilter(3)).filter(ImageFilter.GaussianBlur(1.1))

rgba = im.convert('RGBA'); rgba.putalpha(mask)
rgba.save('去背景.png')
```

### 5.2 底部淡出（做"站在页面上"的效果）

```python
px = rgba.load()
FADE = 46                       # 淡出高度 px
for y in range(rgba.size[1]-FADE, rgba.size[1]):
    k = (rgba.size[1]-y) / FADE
    for x in range(rgba.size[0]):
        r,g,b,a = px[x,y]; px[x,y] = (r,g,b,int(a*k))
```

### 5.3 压体积（放进网页必做）

```python
# PNG 406KB → WebP 41KB，肉眼无损
im.save('avatar.webp', 'WEBP', quality=88, method=6)
```

**统一画布**很重要：多张图（含眼神变体）必须缩放到同一尺寸再居中放置，否则切换时会跳位。

---

## 6. 第六步：放进网页（可选）

想要"鼠标划过窗口，形象转头看过去 + 眼珠跟着鼠标动"的效果，三件东西：

1. **四张图**：正视 + 看左 + 看右 + 看下（即 `lookL/lookR/lookD`）
2. **选图逻辑**：鼠标相对形象中心的偏移量 → 决定用哪张眼神图
   - 水平偏离 > 30% 视野宽 → 切左/右
   - 垂直偏下 > 34% 视野高 → 切下
   - 其余 → 正视
3. **透视姿态**：同时给整张图加 `perspective(900px) rotateY(∓9deg)` 让它整体微转

核心 JS（可直接抄）：

```js
function pickGaze(kx, ky){                       // kx/ky 是鼠标相对形象中心的归一化偏移(-1~1)
  if(Math.abs(kx) >= 0.30 && Math.abs(kx) >= Math.abs(ky)*0.8) return kx < 0 ? 'lookL' : 'lookR';
  if(ky >= 0.34) return 'lookD';
  return 'idle';
}
window.addEventListener('mousemove', e => {
  const r = img.getBoundingClientRect();
  const kx = Math.max(-1, Math.min(1, (e.clientX - (r.left+r.width/2)) / 380));
  const ky = Math.max(-1, Math.min(1, (e.clientY - (r.top+r.height/2)) / 520));
  img.src = gazeImage[pickGaze(kx, ky)];
  img.style.transform = `perspective(900px) translate(${kx*8}px,${ky*4}px) rotateY(${-kx*9}deg) rotate(${kx*1.5}deg)`;
});
```

---

## 7. 推荐工具

| 工具 | 谁适合 | 链接 |
|---|---|---|
| **即梦** | 首选，中文提示词、效果好、每天有免费额度 | https://jimeng.jianying.com/ai-tool/image/generate |
| 通义万相 | 阿里出品，中文友好 | https://tongyi.aliyun.com/wanxiang |
| Pollinations | 免注册、免 Key，网页直出（图生图不支持） | https://pollinations.ai |
| 硅基流动 / OpenAI 兼容 API | 想接自己的页面做一键生成 | OpenAI 兼容的图片接口 |

---

## 8. 一句话总结

> 一张正面照 → **Pixar-style + realistic adult proportions** 图生图定脸 → 同一张母版改眼神出三张变体 → 抠图压成 WebP → 挂到页面上让眼神跟着鼠标走。
> **别写"写实"，别写"Q版"，所有变体必须继承同一张母版。**
