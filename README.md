# crypto-observe
Service to get the growth or the decline of cryptocurrencies

### Requirement
1. `node` > 8
2. Some crypto currencies in mind

### How to use
1. `npm install crypto-observe`
2. For example:

```js
const { CryptoObserve } = require("crypto-observe");

const config = {
  currencies: ["bitcoin", "ethereum","ripple"], // REQUIRED: The currencies to be scraped
  frequency: "10s", // REQUIRED: The frequency of scraping coinmarketcap. E.g: "45s", "2m", "1h"
  decrease: {
    type: "daily", // REQUIRED: Check the threshold of decline, whether decline "hourly", "daily", or "weekly"
    percentage: 5, // REQUIRED: The minum percentage of decline before emitting "danger". E.g: It will emit "danger" if it declined below 5%
    rest: "3h" // REQUIRED: Rest time before emitting "danger" again. E.g: "15m", "3h", "1d"
  },
  increase: {
    type: "daily",
    percentage: 5,
    rest: "5m"
  }
};

const watch = new CryptoObserve(config);

watch.on("data", data => {
  console.log("data", data.length);
});

watch.on("decrease", res => {
  console.log("Danger...", res);
});


watch.on("increase", res => {
  console.log("To the moonnn...", res);
});

watch.on("error", err => {
  console.log(err);
  process.exit();
});

```