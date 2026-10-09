# shanghai-eats · 上海逛吃地图

单文件交互地图：高德底图 + GCJ-02 坐标，按街区组织；手机上一键唤起高德地图 / 大众点评 App。

**线上地址：<https://lyf1122.github.io/shanghai-eats/>**

## 加一家店（无需本地环境，手机/网页即可）

1. 打开 [`src/data.js`](src/data.js) → 点右上角铅笔 ✏️ 进入编辑
2. 照现有条目格式，在对应街区的 `places` 数组里加一条：
   ```js
   { name: '店名', type: 'food', lat: 31.22, lng: 121.47,
     desc: '一句话推荐', budget: '人均 60-100',
     detail: '展开后的补充，\n 换行' },
   ```
   type 取值：`food` 餐厅 · `cafe` 咖啡·甜品 · `spot` 逛·街区 · `bar` 酒吧 · `shop` 购物；
   可选字段 `dpKeyword`（点评搜索词）、`dianping: false`（隐藏点评按钮）、`reserve`（预约链接）
3. Commit changes → GitHub Actions 自动构建，约 1-2 分钟后线上更新

坐标用**高德系 GCJ-02**：用[高德坐标拾取器](https://lbs.amap.com/tools/picker)搜店名，复制 `lng,lat`（注意拾取器给的是 `经度,纬度`，对应本文件的 `lng,lat`）。

## 目录结构

| 路径 | 说明 |
|---|---|
| `src/data.js` | **数据区：加店/改店只动这里**（字段注释在文件顶部） |
| `src/engine.js` `src/app.css` `src/shell.html` | 引擎 / 样式 / 页面骨架 |
| `src/build.mjs` | 构建脚本 |
| `lib/` | Leaflet 1.9.4 |
| `index.html` | ⚠️ 构建产物，别手改（Actions 会在 src 变更后自动重新生成） |

## 本地构建（可选）

```bash
node src/build.mjs        # 生成 index.html
node src/build.mjs out.html   # 输出到指定路径
```
