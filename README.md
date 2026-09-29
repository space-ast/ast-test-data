# ast-test-data

`ast-nt` 的测试数据仓库，以子模块形式挂载在 `ast-nt` 的 `test/data/` 下。

目录结构在本仓库根下直接展开：测试代码里 `aTestDataDirGet() + "/ICRF/IAU2006_XYS.dat"`
即对应本仓库的 `ICRF/IAU2006_XYS.dat`。

## 目录

| 路径 | 内容 | 来源 |
|------|------|------|
| `ATK/` | GEMT1 重力场（v1/v2 两个版本），STK `.grv` 格式 | AGI/Ansys STK |
| `CentralBodies/` | 地球与月球重力场：EGM96/EGM2008、GGM01C/02C/03C、JGM2/JGM3、WGS84，月球 GL/GM/LP 系列 | STK `.grv` 格式 |
| `GMAT/` | 重力场 `.cof` 与 GMAT 启动文件 | NASA GMAT |
| `ICRF/` | IAU2000A / IAU2006 岁差-章动序列 | IERS / STK 格式 |
| `satkit/` | ICGEM `.gfc` 重力场与 `leap-seconds.list` | satkit |
| `STK/` | 星历 `.e`、卫星 `.sa`/`.sa3`/HPOP、两种格式的闰秒文件 | AGI/Ansys STK |
| 根目录 | `LeapSecond.dat`、`TestBKV.txt`、`EOP-All.csv`（地球指向参数）、`leDE*.4xx` 与 `plneph.405`（JPL DE 星历二进制） | 混合 |

## 注意事项

- **SPICE 内核不在这里。** `*.bsp` / `*.tls` / `*.tpc` 位于
  [ast-data](https://github.com/space-ast/ast-data) 的 `kernels/` 下，因为运行时的
  `aGetDefaultSPKDir()` 与数据目录初始化也要用它们，不属于纯测试数据。
- **本仓库不使用 git-lfs。** `.gitattributes` 里的 `* -text` 只是禁止行尾转换、
  保证检出字节与原始文件一致，不是 LFS 过滤器，请勿改成 `filter=lfs`。
- **不要放入 `.cpp` / `.cxx` / `.asc` 文件。** `test/xmake.lua` 会递归 glob 这些扩展名
  并逐个生成测试目标，数据文件一旦命中会被误当成测试用例。
- 本仓库内容原为 `ast-data` 的 `Test/` 目录，于 2026-09-29 整体迁出
  （源：ast-data `5bf27d2` 及其之前的历史）。
- `EOP-All.csv` 目前没有被任何代码或配置引用（代码只用 `EOP-All.txt`），
  且 ast-data 的 `README.md` 仍把它记在 `SolarSystem/Earth/` 下。保留在此仅供人工查证。
