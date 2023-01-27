# Binance Futures Leaderboard Scraper

Binance Futures Leaderboard Scraper is an Apify actor which lets you extract data from [Binance](https://www.binance.com/en/futures-activity/leaderboard) by using any filtering and sorting options provided by Binance.

## Features

-   Scrape leaderboards by filters - You can scrape leaderboards by using advanced filters (described detailly below) and get user's PNL, ROI and rank informations.

-   Scrape leaderboards by urls - You can scrape filtered leaderboards by directly using urls.

-   Scrape positions - You **Trend Analysis:** You can analyse the position trends of the top users can scrape specific user's current open positions and get attributes like symbol entry price, mark price, amount, PNL, ROE,

-   Sort - You can sort users by using their ROI, PNL or Followers attributes.

-   You can define maximum number of users

## Possible Use-cases

-   Automated trading: You can integrate this scraper to your automated trading algorithms and copy positions of the top users on Binance Futures

-   Developing Signal Bots: You can process the positions of the top users and send signals possible places like Telegram or IRC bots.

-   Trend Analysis: You can analyse the position trends of the top users.

-   Popular Positions: You can compare open positions and learn what top users are on to.

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/binance-futures-leaderboard-scraper/issues).

## Incoming Changes

-   Scrape specific users
-   Detect position changes and updates

## Setup & Usage

You can see how this actor works these videos:

### Using Start URLs

[![Apify - Binance Futures Leaderboard Scraper - Using Start URLs](https://img.youtube.com/vi/FiHwqyGzKkE/0.jpg)](https://www.youtube.com/watch?v=FiHwqyGzKkE)

### Using Filters

[![Apify - Binance Futures Leaderboard Scraper - Using Filters](https://img.youtube.com/vi/aKT6e8pLyaA/0.jpg)](https://www.youtube.com/watch?v=aKT6e8pLyaA)

## Input Parameters

| Field             | Type    | Description                                                                                                                                                                                                                                                                                                        |
| ----------------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| startUrls         | array   | (optional) List of Binance futures leaderboard URLs. It can be a any filtered leaderboard like [this](https://www.binance.com/en/futures-activity/leaderboard?type=filterResults&isShared=true&tradeType=PERPETUAL&symbol=ETHUSDT&periodType=WEEKLY&roiGainType=LEVEL1&pnlGainType=LEVEL2&sortType=ROI&limit=200). |
| includePositions  | boolean | This will tell the actor to fetch the positions of the users that are sharing.                                                                                                                                                                                                                                     |
| maxItems          | number  | (optional) You can limit scraped users. This should be useful when used with sortType to get the top users.                                                                                                                                                                                                        |
| useFilters        | boolean | Enable this option if you want to use the filters described below.                                                                                                                                                                                                                                                 |
| tradeType         | enum    | Type of the leaderboard you want to scrape. Valid values: `PERPETUAL` \| `DELIVERY`                                                                                                                                                                                                                                |
| symbol            | enum    | Symbol filter for the leaderboard. Valid values: `""` (All) \| `BTCUSDT` \| `ETHUSDT` \| `LINKUSDT` \| `DOTUSDT` \| `LTCUSDT` \| `XRPUSDT` \| `ADAUSDT` \| `BCHUSDT` \| `CRVUSDT` \| `BNBUSD`                                                                                                                      |
| periodType        | enum    | Period filter for the leaderboard. Valid values: `DAILY` \| `WEEKLY` \| `EXACT_WEEKLY` \| `MONTHLY` \| `EXACT_MONTHLY` \| `YEARLY` \| `EXACT_YEARLY` \| `ALL`                                                                                                                                                      |
| roiGainType       | enum    | ROI Gains filter for the leaderboard. Valid Values: `ALL` \| `LEVEL1` \| `LEVEL2` \| `LEVEL3` \| `LEVEL4` \| `LEVEL5`                                                                                                                                                                                              |
| pnlGainType       | enum    | PNL Gains at least filter for the leaderboard. Valid values: `ALL` \| `LEVEL1` \| `LEVEL2` \| `LEVEL3` \| `LEVEL4` \| `LEVEL5`                                                                                                                                                                                     |
| coinmPnlGainType  | enum    | PNL Gains at least filter for the leaderboard that is used when `tradeType` equals to `DELIVERY`. Valid values: `ALL` \| `LEVEL1` \| `LEVEL2` \| `LEVEL3` \| `LEVEL4` \| `LEVEL5`                                                                                                                                  |
| isShared          | boolean | This will tell the actor only to scrape users that are sharing their positions.                                                                                                                                                                                                                                    |
| sortType          | enum    | Sorting filter for the leaderboard. Valid values: `ROI` \| `PNL` \| `FOLLOWERS`                                                                                                                                                                                                                                    |
| customMapFunction | string  | (optional) A function which helps you to map the output data by your preferences.                                                                                                                                                                                                                                  |
| proxy             | object  | Proxy configuration                                                                                                                                                                                                                                                                                                |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use <a href="https://www.apify.com/docs/proxy">Apify Proxy</a>.

## Tips

If you want to use `includePositions`, it is advised to use it with `isShared`. Otherwise the leaderboard will contain lots of users that are not sharing their positions so you will get less results.

Please keep in mind that for the sake of not to lose any of the data the actor returns all the possible output. That's it's suggested to use `customMapFunction` all the time.

## Compute Unit Consumption

The actor optimized to run blazing fast not to miss any position at a given time. It will fetch each leaderboard in a single request. However if you enable `includePositions`, it will scrape all users individually.

If you don't enable `includePositions`, the actor will fetch ~200 users around ~1 minute with ~0.01 - 0.03 compute units.

If you enable `includePositions`, the actor will fetch ~200 users around ~3 minutes with ~0.03 - 0.05 compute units.

## Binance Futures Leaderboard Scraper Input example

```json
{
    "startUrls": [
        {
            "url": "https://www.binance.com/en/futures-activity/leaderboard?type=filterResults&isShared=true&limit=200&periodType=EXACT_MONTHLY&pnlGainType=LEVEL4&roiGainType=LEVEL3&sortType=ROI&symbol=BTCUSDT&tradeType=PERPETUAL",
            "method": "GET"
        }
    ],
    "useOnlyStartUrls": false,
    "tradeType": "PERPETUAL",
    "periodType": "DAILY",
    "roiGainType": "ALL",
    "pnlGainType": "ALL",
    "coinmPnlGainType": "ALL",
    "isShared": true,
    "includePositions": true,
    "sortType": "ROI",
    "customMapFunction": "(object) => ({...object})",
    "maxItems": 200,
    "proxy": {
        "useApifyProxy": true
    },
    "symbol": ""
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
    "id": "70269580C70D9F62BFDEE81E8080E0F9",
    "name": "AroJarHzEe",
    "positionShared": true,
    "deliveryPositionShared": false,
    "pnl": 409.017814,
    "roi": 1.00638248,
    "rank": 201,
    "positions": [
        {
            "symbol": "STORJUSDT",
            "entryPrice": 1.303275,
            "markPrice": 1.26076783,
            "pnl": -40.12676848,
            "roe": -1.34861214,
            "amount": 944,
            "updateTimeStamp": 1634571653046
        },
        {
            "symbol": "SCUSDT",
            "entryPrice": 0.017954,
            "markPrice": 0.01809703,
            "pnl": 7.1515,
            "roe": 0.31614027,
            "amount": 50000,
            "updateTimeStamp": 1634574301699
        }
    ]
}
```
