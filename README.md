# samsung_legacy_builder — 老内核（4.19 / 5.4）ROOT 内核构建

ReSukiSU + SuSFS，GitHub Actions 一键出包，boot-only AnyKernel3 卡刷包。By 抖音王德发刷机

## 用法

Actions 页选对应机型的 workflow → Run workflow → 构建完成后在 Artifacts 下载（可选发布 Release）。

## 覆盖机型

| 设备 | 代号 | 内核源 @ 分支 | defconfig | 补丁分支 |
|---|---|---|---|---|
| Samsung_Tab_S7 | gts7l | BailinT/android_kernel_samsung_sm8250 @ lineage-23.2 | vendor/kona_defconfig | samsung-gts7 |
| Samsung_Galaxy_Note20_Ultra | r8s | Android-Artisan/android_kernel_samsung_exynos990 @ main | exynos9830_defconfig | samsung-e9x |

## 结构

- `.github/workflows/build-*.yml` — 每机型一个一键构建
- `.github/workflows/{build-env,build-ready,build-process,pack-process,patch-susfs,...}` — 共用 action 链（源自 Xiaomi-Kernel-Builder 母本）
- 补丁库：BailinT/NonGKI_Kernel_Patches；打包框架：BailinT/AnyKernel3

## 注意

- 只刷 boot 分区，刷前务必备份原厂 boot
- 部分机型源码有已知坑（如悬空 symlink、MODULE_SIG_FORCE、LTO 标志），workflow 内已按调研结论配置；首次构建失败属正常，按日志迭代