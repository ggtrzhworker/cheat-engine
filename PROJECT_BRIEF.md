# PROJECT_BRIEF.md

## 项目目标

- 只现代化 Cheat Engine 的 UI 和交互。
- 不增强扫描、调试、注入、驱动、绕过检测、反检测能力。

## 禁止修改范围

- `Cheat Engine/memscan.pas`
- `Cheat Engine/foundlisthelper.pas`
- `Cheat Engine/MemoryRecordUnit.pas`
- debugger / driver / DBK / kernel / injection / hook / anti-detection 相关代码

## 第一阶段允许范围

- 只写 `PROJECT_BRIEF.md`
- 不改 `Cheat Engine/MainUnit.pas`
- 不改 `Cheat Engine/MainUnit.lfm`
- 不改 `Cheat Engine/MemoryBrowserFormUnit.pas`
- 不改 `Cheat Engine/MemoryBrowserFormUnit.lfm`

## 后续允许修改范围

- `Cheat Engine/MainUnit.lfm`
- `Cheat Engine/MainUnit.pas` 中纯 UI 初始化、布局、主题、状态提示相关代码
- `Cheat Engine/MemoryBrowserFormUnit.lfm`
- `Cheat Engine/MemoryBrowserFormUnit.pas` 中纯 UI 初始化相关代码
- 新增 UI theme/helper 单元

## 主窗口第一优先级

- 第一轮只处理 `MainUnit` 主窗口。
- 暂不处理 Memory Browser。
- 暂不处理 `TDisassemblerview` / `THexview`。
- 暂不处理地址列表内部实现。

## 必须保留控件名和事件绑定

- `Foundlist3`
- `Panel1`
- `Panel5`
- `scanvalue`
- `scanvalue2`
- `ScanType`
- `VarType`
- `gbScanOptions`
- `btnNewScan`
- `btnNextScan`
- `btnFirst`
- `btnNext`

## UI 改造方向

- 保留旧功能入口。
- 重排主窗口视觉层级。
- 让“选择进程 → 输入数值 → 选择扫描类型 → 首次扫描 → 再次扫描 → 加入地址表”更清楚。
- 优化间距、分组、状态提示。
- 不重命名核心控件。
- 不替换 `Foundlist3` 的虚拟列表机制。
- 不把动态 `TAddresslist` 搬进 `.lfm`。

## 风险

- `.lfm` 组件名和事件绑定易断。
- `Foundlist3` 是虚拟列表，不能替换成普通列表。
- `btnNewScan` / `btnNextScan` 可能转发到 `btnFirst` / `btnNext`，不能随意删除。
- `Panel1` 内动态创建地址列表，不能第一阶段重构内部。
- Lazarus IDE 自动保存可能产生巨大无关 diff。

## 回滚方式

- 每阶段单独 commit。
- 每次只改少量文件。
- 出问题优先 `git checkout -- <file>` 回滚本阶段文件。

## 后续工作规则

- 每轮先阅读 `PROJECT_BRIEF.md`。
- 继续遵守最小读取、最小 diff、短报告。
- 修改前只列文件名。
- 修改后只列文件清单、改动、检查、下一步。
