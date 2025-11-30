# FarmPixel: 2D像素风格农场模拟经营游戏
基于Godot 4.3引擎开发的开源2D像素风格模拟经营游戏，以农场经营为核心玩法，集成作物种植、NPC交互等完整功能，既为休闲玩家提供轻量化农场经营体验，也为开发者提供可复用的Godot游戏开发模板。


## 项目亮点
- **开源轻量化**：基于Godot开源引擎，无商业版权成本，打包体积<200MB，低配设备可流畅运行
- **模块化架构**：拆分独立功能模块，提供标准化接口，支持快速扩展（如新增作物、NPC类型）
- **创新玩法机制**：采用「时间驱动-状态机」作物生长模型，支持浇水/施肥等交互干预，丰富策略维度


## 核心功能
1. **作物种植系统**：支持小麦、番茄等多类型作物，差异化生长周期（3-5天游戏时间）；包含开垦、播种、浇水、收获全流程交互,作物状态可视化（幼苗 / 生长 / 成熟 / 枯萎）.
2. **NPC交互系统**：涵盖鸡、牛等动物 NPC 及村民等人类 NPC； 动物 NPC 内置自主导航路线并且能随机切换行为状态（观望 - 行走）.
3. **昼夜循环系统**：1 天游戏时间 = 现实 2 分钟 , 模拟日夜交替，影响作物生长速度与 NPC 行为逻辑 .
4. **2D 世界优化**：自定义 5 层碰撞层（角色、地形、交互物体、动物、作物），精准区分碰撞逻辑（如玩家可穿过作物但不可穿过建筑）；基于 YSort 节点实现 Y 轴排序，角色 / 物体根据 Y 坐标自动调整显示层级，彻底解决 2D 场景遮挡问题 .
5. **资源采集系统**：地图分布树木、石头等可采集资源，砍伐树木 / 开采石头时触发摇摆反馈动画，采集后掉落木材、矿石等基础材料 .
6. **自动拾取系统**：鸡蛋、木材、矿石等掉落物自带碰撞区域，玩家角色接触碰撞范围时自动拾取，无需额外操作；拾取后即时更新背包数据，同时触发简短 UI 提示（显示获取物品名称 + 数量） .
   
## 目录结构
```
cromptails-1/
├── assets/                # 游戏资源文件
│   ├── ui/                # UI 相关资源
│   │   ├── fonts/         # 像素风格字体文件
│   │   └── basic_ui_sprites.png # UI 基础素材（按钮、图标）
│   └── game/              # 游戏核心素材
│       ├── objects/       # 物品素材（作物、工具、设施）
│       ├── characters/    # 角色素材（玩家、NPC、动物）
│       └── tilesets/      # 地图瓦片素材（地形、建筑）
├── scenes/                # Godot 场景文件
│   ├── characters/        # 角色场景（player、chicken、cow 等）
│   ├── components/        # 功能组件（作物、昼夜系统、交互组件）
│   ├── objects/           # 物品场景（plants、rocks、trees）
│   └── ui/                # UI 界面场景（背包、工具面板、昼夜显示）
├── scripts/               # 核心逻辑脚本
│   ├── globals/           # 全局管理脚本（昼夜循环、背包、工具管理）
│   └── state_machine/     # 状态机脚本（角色 / 作物状态切换）
├── Tilesets/              # 地图瓦片配置文件
└── project.godot          # Godot 项目主配置文件
```

## 技术栈
### 核心引擎技术（Godot 4.3）
- 2D 场景与交互：YSort节点（实现 Y 轴自动排序，解决角色 / 物体遮挡）、Area2D/CollisionShape2D（构建 5 层碰撞层，区分角色、地形、交互物体等逻辑）
- NPC 与动画：NavigationAgnet2d（实现鸡、牛等 NPC 的自主导航路径）、AnimationPlayer（制作像素角色行走、作物生长的帧动画）
- 模块解耦：Godot 原生信号（Signal）机制（如作物成熟信号触发收获提示，替代硬编码依赖）
- 全局管理：Autoload单例（实现昼夜循环、背包状态等全局数据的跨场景共享）
### 开发与设计工具
- 编程与脚本：GDScript（Godot 原生脚本，适配引擎节点体系，轻量易上手）
- 素材制作：Aseprite（绘制 2D 像素角色、作物、场景素材，导出帧动画）、Tiled（编辑地图瓦片，导出为 Godot 兼容的TileMap资源）
### 设计模式与逻辑框架
- 状态机模式：基于state_machine脚本实现作物生长阶段、NPC 行为状态的切换（如鸡的「观望 - 行走」状态流转）
- 观察者模式：通过 Godot 信号实现事件监听

## 快速开始
1. 克隆仓库：
   ```bash
   git clone https://github.com/your-username/FarmPixel.git
   ```
2. 安装 Godot 4.3 引擎：Godot 官网下载
3. 打开项目：在 Godot 编辑器中选择「导入项目」，选中仓库根目录的project.godot文件
4. 运行游戏：点击编辑器右上角的「播放」按钮启动游戏


## 游戏界面展示
1.游戏主页面（START, SABE, EXIT）
<img width="1698" height="989" alt="image" src="https://github.com/user-attachments/assets/39215942-8b3e-4601-b286-833eb9fc6f07" />

2.游戏运行画面

左侧是背包的收集物栏，显示目前的收集情况（分别有木材Log、石头Stone、玉米Corn、番茄Tomato、鸡蛋Egg、牛奶Milk）；

下方是角色的工具栏，显示当前的工具。每个工具对应不同的事件（砍伐Axe、耕地Tilling、浇水Watering、播种玉米Corn、播种番茄Tomato）；

右上角是时间状态栏，显示当天天数和具体时间。下方还配有加速键。

<img width="1686" height="993" alt="image" src="https://github.com/user-attachments/assets/7378bbf8-3a6c-4d2d-90e6-e86a3e609c9c" />

3.动物NPC（鸡、牛）自由导航，自由切换形态（行走Walk,待机Idle）
<img width="1705" height="996" alt="image" src="https://github.com/user-attachments/assets/928bb540-3013-4635-98c7-b892bc779e3b" />

4.农作物（小麦、番茄）随时间切换形态（播种Seed，萌发Germination,生长Vegetative,繁殖Reproduction,成熟Mautrity,收获Harvesting）

<img width="465" height="287" alt="image" src="https://github.com/user-attachments/assets/546659c9-9a31-48ca-b0a2-a012f720715b" />

## 注意事项

1. 确保安装Godot 4.3 版本引擎
2. 游戏运行若出现 UI 显示异常，可在 Godot 编辑器中重新导入assets/ui目录下的字体 / 素材资源
3. 项目中像素素材（如assets/game/objects下的大体积帧动画）、地图瓦片文件通过 Git LFS 管理，拉取仓库前需先安装 Git LFS 并执行 git lfs install，再克隆仓库
4. 若拉取后发现素材缺失，可执行 git lfs pull 手动同步 LFS 资源；若资源引用失效，在 Godot 编辑器中右键assets目录选择「重新导入所有资源」
5. 内置像素素材、字体资源仅用于项目演示，若用于商业发布，需替换为自有版权资源

## 未来发展方向
1. **玩法扩展**：新增畜牧养殖全流程（动物喂养、产物收集、棚舍升级）、渔业系统（钓鱼、鱼塘养殖）、节日活动（如丰收节任务、限定作物），丰富核心玩法维度
2. **生态构建**：开发 Mod 支持框架，允许第三方开发者通过配置文件新增作物、NPC、场景与任务；搭建开源素材资源库，提供像素素材模板与脚本插件；探索多人联机模式（局域网合作种植、好友农场互访、交易市场）。
