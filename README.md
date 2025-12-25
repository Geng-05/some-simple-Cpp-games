





# 游戏合集与框架说明（Qt/C++）

本仓库包含一个简单的 Qt Widgets 游戏框架以及 6 个小游戏示例，适合作为课程设计、入门练习或参考项目。各模块均基于 Qt（推荐 Qt 5.12+）与 C++ 开发，项目以 `.pro` 工程文件组织，使用 `qmake` 构建。

## 开发环境
- Qt 版本：建议 Qt 5.12 及以上（Qt 6 也可，但需按需调整）
- 编译器：MSVC 或 MinGW（随 Qt 安装）
- IDE：Qt Creator 或 VS Code（配合 Qt 插件 / CMake / Ninja）

## 构建与运行
1. 使用 Qt Creator：
	 - 直接打开各子目录中的 `.pro` 工程文件（如 `0_GameFrame【游戏主框架】/GameFrame.pro`）。
	 - 选择合适的 Kit（如 Desktop Qt 5.12.12 MSVC 或 MinGW）。
	 - 构建并运行。
2. 使用命令行（qmake）：
	 - 在子工程目录下执行：
		 - Windows（PowerShell）：
			 ```powershell
			 qmake
			 mingw32-make   # 若使用 MinGW
			 # 或使用 nmake（MSVC 工具链）
			 ```

资源文件通过 `.qrc` 收集，构建时会自动打包到可执行文件，确保图片与音频目录与 `.qrc` 中路径一致。

## 目录概览
- 0_GameFrame【游戏主框架】：统一窗口框架与入口示例。
- 1_Snake【小游戏一：贪吃蛇】：经典贪吃蛇，含基础 AI。
- 2_tankbattle【小游戏二：坦克大战】：俯视角坦克射击与地图碰撞。
- 3_sudoku【小游戏三：数独】：数独逻辑、难度选择、记录榜。
- 4_gomoku【小游戏四：五子棋】：人机/人人对战五子棋。
- 5_minesweeper【小游戏五：扫雷】：经典扫雷玩法与难度调节。
- 6_ZombieMob【小游戏六】：僵尸群小型动作游戏。

---

## 主框架：GameFrame
- 工程：`0_GameFrame【游戏主框架】/GameFrame.pro`
- 关键文件：`gamewindow.cpp`、`mainwindow.cpp`、`images/`
- 介绍：
	- 提供统一的主窗口与菜单导航，示范如何在同一框架中加载不同小游戏界面（`QMainWindow` + `QWidget` 页切换）。
	- 资源统一管理与基本 UI 布局（`gamewindow.ui`、`mainwindow.ui`）。
- 适用：作为启动器或示例框架，将各小游戏以页面或独立窗口方式挂载。

## 小游戏一：贪吃蛇（Snake）
- 工程：`1_Snake【小游戏一：贪吃蛇】/SnakeGamev2.2.pro`
- 关键文件：`snake.cpp`、`widget.cpp`、`snake_ai.cpp`、`images/`
- 玩法：
	- 方向键控制蛇移动，吃食物增长长度，避免撞墙或自撞。
	- 支持基本 AI 路径规划（`snake_ai.*`），可切换人机或演示模式。
- 特性：`resources.qrc` 管理图片资源；`widget.ui` 提供分数显示与按钮。

## 小游戏二：坦克大战（Tank Battle）
- 工程：`2_tankbattle【小游戏二：坦克大战】/tankbattle.pro`
- 关键文件：`player.cpp`、`enemy.cpp`、`bullet.cpp`、`game_map.cpp`、`images/`、`maps/`
- 玩法：
	- 控制主坦克移动与射击，摧毁敌人并避开墙体与子弹。
	- 地图由文本（`maps/map1.txt`, `map2.txt`）定义；资源通过 `images.qrc`、`maps.qrc`、`musics.qrc` 管理。
- 特性：
	- 碰撞检测（坦克-墙体/子弹）、爆炸动画（`images/boom`、`bullet_boom`）。
	- 菜单与难度入口（`menu.cpp`、`mainwindow.ui`）。

## 小游戏三：数独（Sudoku）
- 工程：`3_sudoku【小游戏三：数独】/sudoku.pro`
- 关键文件：`sudokulogic.cpp`、`sudokudelegate.cpp`、`gamewindow.cpp`、`recordsdialog.cpp`
- 玩法：
	- 选择难度后生成数独棋盘，填写数字 1-9，完成所有行/列/宫的约束。
	- 提供记录榜与难度选择（`difficultydialog.*`、`recordsdialog.*`）。
- 特性：
	- 逻辑生成与校验（`sudokulogic.*`）。
	- 自定义绘制与输入代理（`sudokudelegate.*`）提升交互体验。

## 小游戏四：五子棋（Gomoku）
- 工程：`4_gomoku【小游戏四：五子棋】/gomoku.pro`
- 关键文件：`boardwidget.cpp`、`mainwindow.cpp`
- 玩法：
	- 黑白双方轮流落子，五子连线即胜。支持人人或基础人机。
- 特性：
	- 棋盘绘制与胜负判定（`boardwidget.*`）。

## 小游戏五：扫雷（Minesweeper）
- 工程：`5_minesweeper【小游戏五：扫雷】/minesweeper.pro`
- 关键文件：`cellbutton.cpp`、`gameboard.cpp`、`difficultydialog.cpp`
- 玩法：
	- 选择难度，点击格子，标记雷。翻开所有非雷格子即胜。
	- 支持右键标记、展开空白区域、计时与统计。
- 特性：
	- 自定义按钮控件（`cellbutton.*`）与棋盘逻辑（`gameboard.*`）。

## 小游戏六：ZombieMob
- 工程：`6_ZombieMob【小游戏六】/ZombieMobGame.pro` 或 `src/QtZombieMobGame.pro`
- 关键文件：`src/gamewindow.cpp`、`src/mysprite.cpp`、`src/utils.cpp`、`images/`
- 玩法：
	- 控制角色在地图中移动与躲避/击退僵尸群，存活尽可能久。
- 特性：
	- 贴图与精灵封装（`mysprite.*`），工具函数（`utils.*`），资源打包（`images.qrc`）。

---

## 常见问题
- 资源路径：若运行时报资源缺失，请确认图片/音频目录与 `.qrc` 文件中的路径一致，且 `qmake` 已重新生成构建文件。
- 编译错误：
	- 检查 Qt 版本是否与工程设置匹配；
	- 使用与项目一致的工具链（MinGW vs MSVC）。
- 运行白屏：确保 `QRC` 正确编译，或在 `*.ui`/`*.cpp` 中资源引用路径无误。

## 许可与引用
本项目为学习与演示用途。若需商用或二次分发，请根据所属资源与代码来源自查许可并合规使用。
