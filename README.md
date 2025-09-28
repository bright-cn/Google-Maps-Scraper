# 谷歌地图爬虫

## 目录
- [免费谷歌地图爬虫](#免费谷歌地图爬虫)
  - [设置与安装](#设置与安装)
  - [如何使用爬虫](#如何使用爬虫)
  - [输出](#输出)
- [常见爬取挑战](#常见爬取挑战)
- [解决方案：Bright Data 谷歌地图爬虫 API](#解决方案：bright-data-谷歌地图爬虫-api)
  - [使用谷歌地图爬虫 API](#使用谷歌地图爬虫-api)
  - [使用 API 参数自定义数据采集](#使用-api-参数自定义数据采集)

## 免费谷歌地图爬虫
使用这个免费爬虫从 Google 地图提取商家评论。只需几步即可获取评论者、评分、评论文本、照片等详细信息。

### 设置与安装
开始之前，请确保已安装以下前置条件：
- Python 3.9+
- Playwright（用于浏览器自动化）

按以下步骤完成设置：
1. 将仓库克隆到本地
2. 进入 `free-scraper` 目录
3. 安装依赖：

    ```bash
    pip install playwright
    playwright install
    ```
### 如何使用爬虫
按以下步骤使用爬虫：

1. 打开 `main.py` 并添加目标 Google 地图 URL：

    ```python
    urls = [
            "https://www.google.com/maps/place/Joe's+Pizza+Broadway/@40.7546835,-73.989604,17z/data=!3m1!5s0x89c259ab3e91ed73:0x4074c4cfa25e210b!4m8!3m7!1s0x89c259ab3c1ef289:0x3b67a41175949f55!8m2!3d40.7546795!4d-73.9870291!9m1!1b1!16s%2Fg%2F11bw4ws2mt?entry=ttu",
            "https://www.google.com/maps/place/Googleplex/@37.4220583,-122.0878991,17z/data=!4m8!3m7!1s0x808fba02425dad8f:0x6c296c66619367e0!8m2!3d37.4220541!4d-122.0853242!9m1!1b1!16zL20vMDNiYnkx?hl=en&entry=ttu",
            # Add as many URLs as you need
        ]
    ```
2. 运行脚本：

    ```bash
    python main.py
    ```
### 输出
爬虫会将结果保存到 [free_scraper_output.json](https://github.com/bright-cn/Google-Maps-Scraper/blob/main/sample_data/free_scraper_output.json)，示例内容：
```json
{
    "reviewer_name": "Jacqueline",
    "reviewer_link": "https://www.google.com/maps/contrib/108281841745817069467/reviews?hl=en-GB",
    "reviewer_image": "https://lh3.googleusercontent.com/a-/ALV-UjUzl62rTNZOxsKGxvlnjM3leUg7DZostYzDJvG_8DUSNEtC7p-X=w36-h36-p-rp-mo-ba4-br100",
    "rating": 5,
    "date": "a week ago",
    "text": "Went for lunch on a Tuesday at around 12:45pm. As usual, there was a line, but it moved really quickly and I was able to get my pizza 10 minutes later. Don't let the line deter you from trying Joe's! The pizza is great as always and the staff are nice. Never disappointed. I tried the caprese pizza and it was great!\n\nThere are a lot of people inside and outside so it can get hectic, but turnover for seats is quite quick and I got a seat on the bench outside almost right away.",
    "photos": [
        "https://lh5.googleusercontent.com/p/AF1QipMChGwUdQgWF9NAqdvss36KeuBZw_DAiuZy5yJj=w300-h225-p-k-no",
        "https://lh5.googleusercontent.com/p/AF1QipNvachPq2HyJU0_3hs0DsRDRChaHZrQDDKOc3hz=w300-h225-p-k-no"
    ],
    "likes_count": "1"
}
```

每条评论包含：
- **评论者信息**：姓名、个人主页链接、头像
- **评论内容**：星级评分、发布时间、完整评论文本
- **媒体**：附带照片的 URL
- **互动**：点赞数量

## 常见爬取挑战
从 Google 地图抓取数据可能面临以下挑战：
1. **动态内容加载**：Google 地图通过滚动时的 XHR/API 调用动态加载评论。如果不正确处理动态请求与等待策略，爬虫可能只能抓到部分数据。
2. **DOM 结构变化**：Google 频繁更新 DOM 结构、类名和数据属性，需要持续维护并适配变化。
3. **速率限制与检测**：抓取行为可能触发反爬机制，导致限流或 IP 封禁。

## 解决方案：Bright Data 谷歌地图爬虫 API
如果您需要可靠、可规模化的数据采集，请使用 [Bright Data Google Maps Scraper API](https://www.bright.cn/products/serp-api/google-search/maps)。优势包括：
- 无需自建或管理代理
- 可从任意地理位置抓取
- 覆盖 195 个国家/地区、7200 万+真实 IP
- 多种数据交付方式（S3、Cloud Storage 等）
- 符合 GDPR 与 CCPA
- 7×24 技术支持

此外，您可获得 20 次免费 API 调用进行测试。

## 使用谷歌地图爬虫 API
只需提供一个 URL，即可收集详尽的 Google 地图评论数据。

<img width="700" alt="bright-data-web-scraper-api-google-maps-reviews" src="https://github.com/bright-cn/Google-Maps-Scraper/blob/main/google-maps-review-example.PNG">

> 详细的设置步骤请参阅我们的[分步设置指南](https://github.com/bright-cn/Google-Maps-Scraper/blob/main/scraper_api_setup.md#setting-up-google-maps-scraper-api)。

关键输入参数：

| 参数 | 类型 | 描述 | 必填 |
|------|------|------|------|
| `url` | 字符串 | Google 地图商家页面 URL | 是 |
| `days_limit` | 数字 | 拉取最近多少天内的评论 | 否 |

示例输出数据：

```json
{
    "url": "https://www.google.com/maps/place/Apple+Apple+Park+Visitor+Center/@37.3327772,-122.0079593,17z/data=!4m18!1m9!3m8!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!2sApple+Apple+Park+Visitor+Center!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg!3m7!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg?entry=ttu",
    "place_id": "ChIJ0aPn18W1j4ARgC9zTSPeQRc",
    "place_name": "Apple Apple Park Visitor Center",
    "country": "US",
    "address": "10600 N Tantau Ave, Cupertino, CA 95014",
    "review_id": "ChdDSUhNMG9nS0VJQ0FnSUMzcDdqMHJRRRAB",
    "reviewer_name": "Krzysztof Wojtczak",
    "reviews_by_reviewer": 32,
    "photos_by_reviewer": "12",
    "reviewer_url": "https://www.google.com/maps/contrib/110797405132582450368/reviews?hl=en",
    "local_guide": true,
    "review_rating": 5,
    "review": "Fajnie można spędzić czas, czilując na tarasie z kawką 🤙",
    "review_date": "2024-11-09T22:18:01.713Z",
    "number_of_likes": 0,
    "response_of_owner": null,
    "response_date": null,
    "photos": [
      "https://lh5.googleusercontent.com/p/AF1QipOtSDFfVpLL5GopXJzoFbTapha0G91nmEx5aSus",
      "https://lh5.googleusercontent.com/p/AF1QipPcr5_TU6MWhAu1_K54DbxywZ4O88Q_qT7NSnhv",
      "https://lh5.googleusercontent.com/p/AF1QipNLM5jHD0iDozGHsax9ydGAWUI_pn_fujQ3Q4Wr",
      "https://lh5.googleusercontent.com/p/AF1QipPcKPwXyHDawuClpTpfV3zE7vMFO0UabmdjX9IG"
    ],
    "timestamp": "2024-11-10T07:37:58.326Z",
    "input": {
      "url": "https://www.google.com/maps/place/Apple+Apple+Park+Visitor+Center/@37.3327772,-122.0079593,17z/data=!4m18!1m9!3m8!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!2sApple+Apple+Park+Visitor+Center!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg!3m7!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg?entry=ttu",
      "days_limit": 30
    }
  }
```
可通过下载[这个示例 JSON](https://github.com/bright-cn/Google-Maps-Scraper/blob/main/sample_data/api_scraper_output.json)查看完整输出。

代码示例：

以下 Python 脚本用于收集 Google 地图评论并将结果保存为 JSON 文件：

```python
import requests
import json
import time


class BrightData:
    def __init__(self, api_token):
        self.api_token = api_token
        self.headers = {
            "Authorization": f"Bearer {api_token}",
            "Content-Type": "application/json",
        }

    def collect_reviews(self, urls_data):
        """
        Collect Google Maps reviews using BrightData API
        """
        # 1. Trigger data collection
        print("Starting data collection...")
        trigger_response = self._trigger_collection(urls_data)
        snapshot_id = trigger_response.get("snapshot_id")
        print(f"Snapshot ID: {snapshot_id}")

        # 2. Wait for data to be ready
        print("Waiting for data...")
        while True:
            status = self._check_status(snapshot_id)
            print(f"Status: {status}")

            if status == "ready":
                # Check if data is actually available
                data = self._get_data(snapshot_id)
                if data and len(data) > 0:
                    break
            time.sleep(10)  # Wait 10 seconds before next check

        # 3. Get and save the data
        print("Saving data...")
        filename = f"api_scraper_output.json"
        with open(filename, "w", encoding="utf-8") as f:
            json.dump(data, f, indent=2, ensure_ascii=False)
        print(f"✓ Data saved to {filename}")
        print(f"✓ Collected {len(data)} reviews")
        return data

    def _trigger_collection(self, urls_data):
        """Trigger data collection"""
        response = requests.post(
            "https://api.brightdata.com/datasets/v3/trigger",
            headers=self.headers,
            params={"dataset_id": "gd_luzfs1dn2oa0teb81",
                    "include_errors": "true"},
            json=urls_data,
        )
        return response.json()

    def _check_status(self, snapshot_id):
        """Check collection status"""
        response = requests.get(
            f"https://api.brightdata.com/datasets/v3/progress/{snapshot_id}",
            headers=self.headers,
        )
        return response.json().get("status")

    def _get_data(self, snapshot_id):
        """Get collected data"""
        response = requests.get(
            f"https://api.brightdata.com/datasets/v3/snapshot/{snapshot_id}",
            headers=self.headers,
            params={"format": "json"},
        )
        return response.json()


if __name__ == "__main__":
    # Initialize with your API token
    brightdata = BrightData("<YOUR_API_TOKEN>")

    # Define URLs to collect reviews from
    urls_to_collect = [
        {
            "url": "https://www.google.com/maps/place/Apple+Apple+Park+Visitor+Center/@37.3327772,-122.0079593,17z/data=!4m18!1m9!3m8!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!2sApple+Apple+Park+Visitor+Center!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg!3m7!1s0x808fb5c5d7e7a3d1:0x1741de234d732f80!8m2!3d37.332773!4d-122.0053844!9m1!1b1!16s%2Fg%2F11rjtz4vtg?entry=ttu",
            "days_limit": 30,
        },
        {
            "url": "https://www.google.com/maps/place/Joe's+Pizza+Broadway/@40.7546835,-73.989604,17z/data=!3m1!5s0x89c259ab3e91ed73:0x4074c4cfa25e210b!4m8!3m7!1s0x89c259ab3c1ef289:0x3b67a41175949f55!8m2!3d40.7546795!4d-73.9870291!9m1!1b1!16s%2Fg%2F11bw4ws2mt?entry=ttu",
            "days_limit": 25,
        },
    ]

    # Collect reviews
    reviews = brightdata.collect_reviews(urls_to_collect)
```

**代码工作原理：**
1. **需要 API Token**：如果还没有，请查看我们的[Google 地图爬虫 API 设置指南](https://github.com/bright-cn/Google-Maps-Scraper/blob/main/scraper_api_setup.md#setting-up-google-maps-scraper-api)获取。
2. **启动数据采集**：将 API Token 填入代码后，发起采集请求并返回 `snapshot_id`，用于后续跟踪任务状态。
3. **等待结果**：采集需要几分钟时间。期间代码会轮询 `snapshot_id` 的状态：
    - 状态 "running" = 仍在采集
    - 状态 "ready" = 采集完成，数据已保存为 JSON 文件
4. **其他参数**：可在 `_trigger_collection` 中添加更多参数以自定义采集。参见[下一节](https://github.com/bright-cn/Google-Maps-Scraper?tab=readme-ov-file#customizing-data-collection-with-api-parameters)了解参数与不同数据交付方式。

### 使用 API 参数自定义数据采集
通过以下 API 参数自定义数据采集：

| 参数 | 类型 | 描述 | 示例 |
|------|------|------|------|
| `limit` | 整数 | 限制每个输入返回的结果数量 | `limit=10` |
| `include_errors` | 布尔 | 在输出中包含错误报告，便于排障 | `include_errors=true` |
| `notify` | URL | 采集完成后回调通知的地址 | `notify=https://notify-me.com/` |
| `format` | 枚举 | 数据交付格式：JSON、NDJSON、JSONL、CSV | `format=json` |

提示：还可通过[Webhook](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-webhook)或[API 拉取](https://docs.brightdata.com/scraping-automation/web-data-apis/web-scraper-api/overview#via-api)的方式交付数据。
