# BumpMesh by CNC Kitchen

**在线使用:** https://bumpmesh.com  
**GitHub:** https://github.com/CNCKitchen/stlTexturizer
**作者:** Stefan Hermann

一款基于浏览器的工具，用于为 3D 网格模型应用表面置换纹理 — 无需安装。

加载 STL、OBJ 或 3MF 文件，选择纹理，调整参数，然后导出带有置换效果的新 STL 文件，即可用于切片。

## 最近更新

- 保存/加载项目文件（`.bumpmesh`）
- 撤销/重做历史记录
- 部件旋转小工具
- 网格诊断功能
- 平滑掩膜边界
- 新增语言：意大利语、西班牙语、葡萄牙语、日语、法语、简体中文
- 速度提升 2–3 倍
- 3MF 导出功能
- 鼠标滚轮微调数值
- 生活质量改进

## 功能特性

### 纹理
- **24 种内置无缝纹理** — 篮子、砖块、气泡、碳纤维、水晶、圆点、网格、防滑表面、六边形、六角形、等网格、针织、滚花、皮革 2、噪点、条纹（×2 变体）、沃罗诺伊、编织（×3 变体）、木材（×3 变体）
- **自定义纹理** — 上传自己的图片作为置换贴图
- **纹理平滑** — 可配置的模糊处理，在应用前柔化置换贴图

### 投影模式
- **三平面**（默认）— 根据表面法线混合三个平面投影；最适合复杂形状
- **立方体（盒状）** — 从 6 个盒子面进行投影，具有边缘接缝融合和智能轴主导
- **圆柱形** — 将纹理包裹在圆柱轴上，可配置盖帽角度
- **球形** — 围绕物体进行球形映射
- **平面 XY / XZ / YZ** — 平坦的轴对齐投影

### UV 与变换控制
- **U/V 缩放** — 独立或锁定缩放（0.05–10×，对数刻度）
- **U/V 偏移** — 在每个轴上定位纹理位置
- **旋转** — 在投影前旋转纹理
- **接缝融合强度** — 柔化立方体/圆柱体投影面交汇处的硬边缘
- **接缝带宽度** — 控制接缝边缘处混合区域的宽度
- **盖帽角度**（圆柱形）— 切换到顶部/底部盖帽投影的阈值

### 置换
- **振幅** — 将置换深度从 0% 缩放到 100%
- **对称置换** — 50% 灰色保持中性，白色向外推，黑色向内推（保持体积）
- **3D 置换预览** — 实时 GPU 加速预览切换，显示实际顶点置换
- **振幅重叠警告** — 当深度超过最小模型尺寸的 10% 时发出警报

### 表面掩膜
- **角度掩膜** — 抑制接近水平的顶部和/或底部面上的纹理（每个阈值为 0°–90°）
- **面排除/包含绘制** — 绘制单个面以排除（橙色）或专门包含（绿色）它们
  - 画笔工具 — 单击单个三角形或可调节半径的圆形画笔
  - 桶填充 — 洪水填充相邻面，直到达到可配置的二面角阈值
  - 擦除 — 按住 Shift 键撤消绘制的面
  - 清除全部 — 重置掩膜

### 网格处理
- **自适应细分** — 细分边直到它们 ≤ 目标长度；尊重锐利折痕（>30° 二面角）
- **QEM 简化** — 使用二次误差度量将结果简化为目标三角形数量，具有边界保护、链接条件检查、法线翻转拒绝和折痕保留
- **网格诊断** — 自动检查开放边和壳数量，提供高级诊断和问题区域覆盖高亮
- **安全上限** — 细分过程中硬性限制为 1000 万三角形，防止内存溢出

### 3D 查看器
- **轨道/平移/缩放** 控制
- **线框切换** — 可视化网格拓扑
- **网格信息** — 实时三角形计数、文件大小、包围盒尺寸
- **网格和轴指示器** — X = 红色，Y = 绿色，Z = 蓝色
- **放置在面上** — 点击一个面将其朝下放置在打印平台上

### 文件支持
- **.STL** — 二进制和 ASCII
- **.OBJ** — 通过 Three.js OBJLoader
- **.3MF** — 基于 ZIP 的格式（通过 fflate 解压缩）

### 导出
- 下载**二进制 STL**，内置置换效果
- 通过细分 → 置换 → 简化 → 写入阶段报告进度
- 可配置的边长阈值和输出三角形限制

### 其他
- **浅色/深色主题** — 遵循操作系统偏好，按浏览器持久化
- **多语言** — 英语、德语和简体中文界面，自动检测

## 使用方法

1. 在现代浏览器（Chrome、Edge、Firefox、Safari）中打开 `index.html`。
2. 将模型拖放到视口中，或点击**加载模型…**（支持 STL、OBJ、3MF）。
3. 从侧边栏选择纹理预设（或上传自定义图片）。
4. 选择投影模式并调整 UV 缩放、偏移、旋转和振幅。
5. （可选）使用角度滑块或绘制工具掩膜或排除表面。
6. 点击**导出 STL** 下载置换后的网格。

> **注意：** 所有处理完全在浏览器中运行 — 不会将任何数据上传到服务器。

## 项目结构

```
index.html            # 主入口点
style.css             # 样式（浅色/深色主题）
logo.png              # 网站图标和标题徽标
CNAME                 # 自定义域名（bumpmesh.com）
textures/             # 内置 JPG/PNG 置换贴图图像（24 种纹理）
js/
  main.js             # 应用程序引导和 UI 连接
  viewer.js           # Three.js 场景/相机/控制器
  stlLoader.js        # 二进制和 ASCII STL 解析器
  presetTextures.js   # 内置纹理预设 + 自定义上传
  previewMaterial.js  # Three.js 材质，用于实时和置换预览
  mapping.js          # UV 投影逻辑（7 种模式）
  displacement.js     # 顶点置换烘焙
  subdivision.js      # 自适应网格细分
  decimation.js       # QEM 网格简化
  exclusion.js        # 面排除/包含绘制
  exporter.js         # 二进制 STL 导出
  i18n.js             # 翻译（EN / DE / ZH）
```

## 本地运行

所有处理完全在浏览器中运行 — 不需要后端或构建步骤。您只需要一个本地 HTTP 服务器，因为浏览器会阻止从 `file://` URL 加载 ES 模块导入和纹理。

```bash
# 克隆仓库
git clone https://github.com/CNCKitchen/stlTexturizer.git
cd stlTexturizer
```

然后从项目根目录启动任何静态文件服务器。选择您已安装的任何一种：

**Python (3.x)**
```bash
python -m http.server 8000
```

**Python (2.x)**
```bash
python -m SimpleHTTPServer 8000
```

**Node.js (npx, 无需安装)**
```bash
npx serve .
```

**PHP**
```bash
php -S localhost:8000
```

在浏览器中打开 http://localhost:8000，即可开始使用。

> **提示：** 任何静态服务器都可以工作 — 该应用程序没有服务器端依赖。

## 依赖项

通过 CDN ([jsDelivr](https://www.jsdelivr.com/)) 加载 — 无需构建步骤或 npm 安装：

| 库 | 版本 | 许可证 | 用途 |
|---------|---------|---------|-------|
| [Three.js](https://threejs.org/) | 0.170.0 | MIT | 3D 渲染、场景管理、材质 |
| — [OrbitControls](https://threejs.org/docs/#examples/en/controls/OrbitControls) | 0.170.0 | MIT | 相机轨道/平移/缩放 |
| — [STLLoader](https://threejs.org/docs/#examples/en/loaders/STLLoader) | 0.170.0 | MIT | 二进制和 ASCII STL 导入 |
| — [OBJLoader](https://threejs.org/docs/#examples/en/loaders/OBJLoader) | 0.170.0 | MIT | OBJ 网格导入 |
| — [LineSegments2 / LineSegmentsGeometry / LineMaterial](https://threejs.org/docs/#examples/en/lines/LineSegments2) | 0.170.0 | MIT | 宽线线框覆盖 |
| [fflate](https://github.com/101arrowz/fflate) | 0.8.2 | MIT | 3MF 导入/导出的 ZIP 压缩和解压缩 |

所有依赖项均采用 MIT 许可证。

## 许可证

GNU AGPL v3.0 — 参见 [LICENSE](LICENSE)。
