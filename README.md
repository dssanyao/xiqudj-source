# 戏曲DJ 采集源（xiqudj-source）

戏曲 DJ WordPress 主题的每周采集源：一个 JSON 文件，主题每周自动抓一次，
新曲入库、榜单换榜。不爬抖音 / 快手 / 视频号页面。

## 采集源地址（填进 WordPress 后台）

后台 → 戏曲DJ → 采集设置 → 采集源地址，填：

```
https://raw.githubusercontent.com/dssanyao/xiqudj-source/main/xiqudj-source.json
```

启用 GitHub Pages 后也可以用：

```
https://dssanyao.github.io/xiqudj-source/xiqudj-source.json
```

填好保存，点「立即采集一次」验证；之后每周自动采集，日志在同一页。

## 文件格式

`xiqudj-source.json`：

```json
{
  "version": 1,
  "updated": "2026-11-17",
  "tracks": [
    {
      "key": "夸定云（DJ版 · 张口妞版）|张口妞",
      "title": "夸定云（DJ版 · 张口妞版）",
      "singer": "张口妞",
      "opera": "豫剧名段《夸定云》",
      "genre": "yuju",
      "grade": "S",
      "bpm": 126,
      "duration": 198,
      "scenes": ["guangchang", "jianshen"],
      "source_url": "https://www.douyin.com/search/..."
    }
  ],
  "charts": {
    "douyin":    [{ "key": "…|…", "trend": "up" }],
    "kuaishou":  [{ "key": "…|…", "trend": "dn" }],
    "shipinhao": [{ "key": "…|…", "trend": "new" }]
  }
}
```

- `key`：曲目稳定标识，默认 `标题|演唱者`，改名、改演唱者会当成新曲。
- `genre`：剧种 id，只能用主题已有的（yuju / jingju / huangmei / yueju / qinqiang / jinju / yueju-gd / pingju / pop），写错整首跳过。
- `grade`：热度等级 S / A / B / C。
- `scenes`：场景 id 数组（guangchang / chezai / chenlian / jianshen / manyao / yedian），写错的忽略。
- `trend`：up 升 / dn 降 / new 新上榜。
- `charts`：每平台必须满 10 行、每行 key 都在 `tracks` 里，当周才换榜；不满 10 行该榜保留旧榜。

## 曲库规模

- 300 首：种子 50 首（主题内置）+ 扩库 250 首（2026-11-17 扩充）。
- 剧种分布：豫剧 70、京剧 50、黄梅戏 40、越剧 40、秦腔 30、晋剧 20、粤剧 20、评剧 20、戏腔流行 10。
- 扩库 250 首取材自真实剧目与真实经典唱段，DJ 版式、制作人、等级、场景按本站既有口径编配；三榜仍为种子榜单（各 10 行），未随扩库改动。

## 怎么更新

1. 改 `xiqudj-source.json`：新曲往 `tracks` 里加；换榜改 `charts` 三平台的名次和 `trend`。
2. `updated` 改成当天日期。
3. 提交。主题每周自动抓；想马上生效，去采集设置点「立即采集一次」。

## 口径说明

三平台没有公开榜单接口，本文件里的热门榜是人工整理的站内汇总，
不是官方实时榜。榜单按周更新，日期见 `updated` 字段。
