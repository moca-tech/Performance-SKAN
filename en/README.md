<p align="center">
  <a href="http://moca-tech.net/">
    <img src="https://www.moca-tech.net/logo.png" alt="S2S" height=72>
  </a>
  <h3 align="center">Moca Tech</h3>
  <p align="center">
    MOCA SKAdNetwork Solution
    <br>
    en
    ·
    <a href="https://github.com/moca-tech/Performance-SKAN" target="_blank">zh</a>
    <br>
    <a href="http://www.moca-tech.net" target="_blank"><strong>More »</strong></a>
    <br>
    <br>
    <a href="mailto:business@moca-tech.net">Business@moca-tech.net</a>
  </p>









## Get SKAdNetwork Ad Impression Parameters

1. Request URL：https://tracking.moca-tech.net/ad-impression
2. Request Method：GET
3. Request Frequency：per impression
4. Request Parameters

| Param         | Type   | Mandatory | Description                                                  |
| ------------- | ------ | --------- | ------------------------------------------------------------ |
| aff_id        | int    | Y         | MOCA Affiliate ID，ex. 10001                                 |
| offer_id      | int    | Y         | MOCA Campaign ID，ex. 100001                                 |
| app_bundle    | int    | Y         | Source App Itunes ID，ex. 1125517808                         |
| version       | string | N         | SKAdNetwork Version<br />1.0<br />2.0<br />2.2 （Default）   |
| fidelity_type | int    | N         | SKAdNetwork 2.2 Fidelity Type<br />1: StoreKit Render Ads<br />2: View-Through Ads |

5. Request sample

   > https://tracking.moca-tech.net/ad-impression?offer_id=106489&aff_id=21124&app_bundle=0&version=2.0

## RESPONSE

1. SKAdNetwork AD Impression: JSON

| Field                                       | Type   | Description                   |
| ------------------------------------------- | ------ | ----------------------------- |
| status &emsp;&emsp;&emsp;&emsp;&emsp;&emsp; | string | Response Result (ok for fail) |
| error                                       | string | Request failure reason        |
| data                                        | object | SKAdNetwork AD Impression     |

2. SKAdNetwork AD Impression Parameters

| Field                                                  | Type                                                  | Description |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------- |
| version | string | SKAdNetwork Version                  |
| ad-network-id | string | SKAdNetwork Provided Network ID                   |
| campaign-id | int | Campaign ID                           |
| itunes-item-id | int | Advertiser Itunes ID |
| nonce | string | Nonce |
| timestamp | int | Millsecond timestamp |
| source-app-id | int | Source Itunes ID. This field is not present when version is 1.0. |
| fidelity-type                                  | int                                                | SKAdNetwork Fidelity Type. This field is present when version is 2.2. |

3. Response Sample

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
		"signature": "MEUCIDjiwgP6cBQv9dtg9+2hfAPX3CqjwVPdwVdgviVEfFbOAiEA6Aqqc2wzP4c5MbV2P90sVdMJTgEcOZ91YASbnCTHe1U="
	},
	"status": "ok"
}
```
