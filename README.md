<p align="center">
  <a href="http://moca-tech.net/">
    <img src="https://www.moca-tech.net/logo.png" alt="S2S" height=72>
  </a>
  <h3 align="center">Moca Tech</h3>
  <p align="center">
    MOCA SKAdNetwork Solution
    <br>
    zh
    ·
    <a href="https://github.com/moca-tech/Performance-SKAN/tree/master/en" target="_blank">en</a>
    <br>
    <a href="http://www.moca-tech.net" target="_blank"><strong>More »</strong></a>
    <br>
    <br>
    <a href="mailto:business@moca-tech.net">Business@moca-tech.net</a>
  </p>








## 获取SKAdNetwork广告展示需要的参数及签名

### 1. 准备
将以下Network ID加入Info.plist
```
hb56zgv37p.skadnetwork
rvh3l7un93.skadnetwork
```
### 2. 请求
1. 请求接口：https://tracking.moca-tech.net/ad-impression
2. 请求方式：GET
3. 请求频率：每次广告展示
4. 请求参数

| 参数名        | 类型   | 必要性 | 说明                                                         |
| ------------- | ------ | ------ | ------------------------------------------------------------ |
| aff_id        | int    | 是     | 渠道ID，示例：10001                                          |
| offer_id      | int    | 是     | 项目号，示例：100001                                         |
| app_bundle    | int    | 是     | 媒体Itunes ID，示例：1125517808                              |
| version       | string | 否     | SKAdNetwork版本号<br />1.0<br />2.0<br />2.2 （缺省时默认）  |
| fidelity_type | int    | 否     | SKAdNetwork 2.2版本用于区分广告展示类型<br />1: StoreKit Render Ads<br />2: View-Through Ads |
| idfv | string    | 否     | IDFV |
| idfa | string    | 否     | IDFA |
| ua | string    | 否     | UA，通常server to server请求需要上传，缺省为HTTP Header User-Agent |
| ip | string    | 否     | IP，通常server to server请求需要上传，缺省从HTTP Header X-Forwarded-For或Remote Address|
| aff_pub | string    | 否     | Affiliate Sub-publisher |
| app_name | string    | 否     | App Name |


6. 示例

   > https://tracking.moca-tech.net/ad-impression?offer_id=106495&aff_id=21124&app_bundle=0&version=2.0

### 3. 响应

1. SKAdNetwork AD Impression: JSON

| 字段名                                      | 类型   | 说明                                                  |
| ------------------------------------------- | ------ | ----------------------------------------------------- |
| status &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; | string | 处理结果 (ok, fail)                                   |
| error                                       | string | 请求失败原因，成功时不返回                            |
| data                                        | object | 用于上报Apple SKAdNetwork的广告展示参数，失败时不返回 |

2. 广告展示参数

| 字段名                                                       | 类型                                                     | 说明        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------- |
| version | string | SKAdNetwork版本，请求时上传的version                         |
| ad-network-id | string | SKAdNetwork提供的网盟ID                                      |
| campaign-id | int | 项目号                                     |
| itunes-item-id | int | 广告的Itunes ID |
| nonce | string | nonce                                                        |
| timestamp | int | 毫秒时间戳 |
| source-app-id | int | 媒体Itunes ID，请求时上传的app_bundle。<br />version=1.0时，不返回 |
| fidelity-type                                  | int                                                | SKAdNetwork约定的广告展示形式，请求时上传<br />version=2.2时，返回 |
| click_trackers | array[string] | 点击上报链接，通常客户使用第三方检测时会返回 |
| impression_trackers | array[string] | 展示上报链接，通常客户使用第三方检测时会返回 |

3. 示例

```json
{
	"data": {
		"version": "2.2",
		"ad-network-id": "hb56zgv37p.skadnetwork",
		"campaign-id": 1,
		"itunes-item-id": 1125517808,
		"nonce": "8d4ee37c-eac3-4ebc-baa9-135618eac483",
		"source-app-id": 0,
		"fidelity-type": 1,
		"timestamp": 1616754257676,
		"signature": "MEUCIDjiwgP6cBQv9dtg9+2hfAPX3CqjwVPdwVdgviVEfFbOAiEA6Aqqc2wzP4c5MbV2P90sVdMJTgEcOZ91YASbnCTHe1U=",
		"click_trackers": ["link1","link2"],
		"impression_trackers": ["link1","link2"]
	},
	"status": "ok"
}
```
