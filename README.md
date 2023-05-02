# Binance Futures Leaderboard Scraper

Binance Futures Leaderboard Scraper is an Apify actor which lets you extract data from [Binance](https://www.binance.com/en/futures-activity/leaderboard) by using any filtering and sorting options provided by Binance. You can read more on this blog post about how this actor works.

## Features

-   Scrape leaderboards by filters - You can scrape leaderboards by using advanced filters (described detailly below) and get user's PNL, ROI and rank informations.

-   Scrape leaderboards by urls - You can scrape filtered leaderboards by directly using urls.

-   Scrape positions - You **Trend Analysis:** You can analyse the position trends of the top users can scrape specific user's current open positions and get attributes like symbol entry price, mark price, amount, PNL, ROE,

-   Sort - You can sort users by using their ROI, or PNL attributes.

-   You can define maximum number of users

## Possible Use-cases

-   Automated trading: You can integrate this scraper to your automated trading algorithms and copy positions of the top users on Binance Futures

-   Developing Signal Bots: You can process the positions of the top users and send signals possible places like Telegram or IRC bots.

-   Trend Analysis: You can analyse the position trends of the top users.

-   Popular Positions: You can compare open positions and learn what top users are on to.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/binance-futures-leaderboard-scraper/issues).


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Clutch.co that should be visited. Possible fields are:

- `startUrls`: (Optional) (Array) List of Binance futures leaderboard URLs. It can be a any filtered leaderboard or User detail page.

- `tradeType`: (Optional) (String) Type of the leaderboard you want to scrape. Valid values: `PERPETUAL` \| `DELIVERY`.

- `periodType`: (Optional) (String) Period filter for the leaderboard. Valid values: `DAILY` \| `WEEKLY` \| `MONTHLY` \| `ALL`.

- `sortType`: (Optional) (String) orting filter for the leaderboard. Valid values: `ROI` \| `PNL`.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use <a href="https://www.apify.com/docs/proxy">Apify Proxy</a>.

## Compute Unit Consumption

The actor optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the important requests. If actor doesn't block very often it'll scrape 100 listings in 1 minute with ~0.01-0.03 compute units.

## Binance Futures Leaderboard Scraper Input example

```json
{
  "startUrls":[
    "https://www.binance.com/en/futures-activity/leaderboard/user/cm?encryptedUid=708A41D98F05FD23F8423AB41514E489"
  ],
  "periodType":"ALL",
  "sortType":"ROI",
  "tradeType":"PERPETUAL",
  "maxItems": 200,
  "proxy": {
    "useApifyProxy": true
  }
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.

When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

## Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this actor.

## Scraped Users & Positions

```json
{
	"nickName": "CryptoNifeCatchN",
	"userPhotoUrl": "https://public.bnbstatic.com/image/common_notification/20211230/f6305dee-e00e-4bfe-9d13-3073ad8eb565.png",
	"positionShared": true,
	"deliveryPositionShared": false,
	"followingCount": 0,
	"followerCount": 1501,
	"twitterUrl": "https://twitter.com/CryptoNifeCatch",
	"introduction": "Follow on Twitter and get a link there to copy all my trades",
	"twShared": true,
	"isTwTrader": false,
	"openId": null,
	"portfolioId": null,
	"positions": [
		{
			"symbol": "TOMOUSDT",
			"entryPrice": 0.5825,
			"markPrice": 0.57599205,
			"pnl": -16.7514633,
			"roe": -0.01123453,
			"updateTime": [
				2023,
				3,
				24,
				9,
				12,
				53,
				157000000
			],
			"amount": 2574,
			"updateTimeStamp": 1679649173157,
			"yellow": true,
			"tradeBefore": false,
			"leverage": 2
		}
	]
}
```
