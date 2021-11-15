![unisniper pancakeswap sniper bot](https://i.imgur.com/FXnQVIA.png)

# [UniSniper.com - PancakeSwap Sniper Bot](http://unisniper.com/?aff=github)
**Website:** [www.unisniper.com](http://unisniper.com/?aff=github)</br>
**Demonstration video:** [Click to view](https://www.youtube.com/watch?v=A6xSSYdJCbU)

## [Download Bot](http://unisniper.com/?aff=github)



# Table of contents

 - [Introduction](#introduction)
	 - [Effectiveness](#effectiveness)
 - [Installation](#installation)
	 - [Requirements](#requirements)
		 - [Where to get a blockchain node](#where-to-get-a-blockchain-node)
	 - [Bot installation](#bot-installation)
 - [Usage](#usage)
	 - [Configuration](#configuration)
	 - [Modes](#modes)
	 - [How to run the Bot](#how-to-run-the-bot)

<br/>

# Introduction
UniSniper is a Command-Line sniping bot for PancakeSwap V2. It works by "sniffing" mempool for incoming unconfirmed transactions. Once the bot sees *add liquidity* transaction, it immediately places a buy order trying to buy newly listed tokens as soon as possible.


## Effectiveness
The performance and effectiveness of the bot are highly dependent on the blockchain node you are connected to, and the internet connection of a computer where the bot is running. The quicker / more up-to-date node and lower latency internet connection, the higher the chance of your transaction being processed and confirmed in the same block as the *add liquidity* one. WiFi can significantly raise the latency and lower the throughput of your connection, thus significantly lowering the effectiveness of the bot. Wired connection is recommended.

<br/>


# Installation

## Requirements
 - [Node.js](https://nodejs.org/) - If you are more experienced, we recommend to install Node.js via [NVM (Node Version manager)](https://github.com/nvm-sh/nvm#installing-and-updating)<br/>If you are using Windows, use [NVM for Windows](https://github.com/coreybutler/nvm-windows)
 - [Blockchain Node](#where-to-get-a-blockchain-node) - with WebSocket endpoint

### Node.js installation - Windows
### [-> Node.js Windows installation - Video Tutorial <-](https://vimeo.com/643484926)

[Visit this page to download NVM for Windows installer](https://github.com/coreybutler/nvm-windows/releases/latest). Scroll down and find **Assets** section. There should be a file called `nvm-setup.zip` which you need to download and install. Once you finished the installation, open the command prompt (CMD) and run it as Administrator. You can open CMD by pressing **Windows key** on your keyboard and typing `cmd`. 
Install LTS (long term support) version of Node.js by typing:
`nvm install lts`

Switch to the LTS version:
`nvm use lts`



### Where to get a blockchain node
[QuickNode.com](https://www.quicknode.com/chains/bsc) provides fast and easy way of connecting to the Binance Smart Chain blockchain node for as low as **9$** per month and 7 days trial. It comes with limited method calls which you will reach very quickly. You can always upgrade the plan later, but that comes with a higher cost.<br/>Their **PRO** plan should be enough for a regular user, as it comes with a 20M request limit. Bot at its peak usage uses up to 150 requests per second which give you an estimated **37 hours of runtime** per month.

 1. Create an account at [QuickNode.com](https://www.quicknode.com/chains/bsc)
 2. [You can use this link to order BSC Node directly](https://www.quicknode.com/endpoints/new/launch/bsc) or manually select your desired package.<br/>If you are ordering manually, click **CREATE NODE**, select **LAUNCH** package (9$ / month / 7 day trial), select **BSC** mainnet network, no addons are needed, click **CONTINUE TO BILLING** and complete the payment.
 3. Once paid, copy **WSS PROVIDER** and paste the URL to the **config.json**

<br/>

#### Dedicated FullNode
If you are experienced you can create your own dedicated blockchain fullnode which does not have any limits for ~100$ / month. [How to install Binance Smart Chain FullNode can be found here](https://docs.binance.org/smart-chain/developer/fullnode.html).<br/>As a server we recommend [Hetzner AX61-NVMe](https://www.hetzner.com/dedicated-rootserver/ax61-nvme/configurator) which is a Ryzen 9 3900 with 128 GB RAM and 1.92TB NVMe SSD (NVMe SSD is mandatory) for around 100$ / month. Hovewer, this method is not recommended for a newbie, as it requires experience with linux administration. For a beginner we recommend to use QuickNode.com which we already covered as it is the easiest method but comes with a downside of much higher cost and limited method calls.

<br/>

## Bot installation
### [-> Bot installation - Video Tutorial <-](https://vimeo.com/642969729)

Make sure you've got [Node.js](https://nodejs.org/) installed.
Download the latest version of the bot from our website [UniSniper.com](https://www.unisniper.com/Buy#download).
Extract downloaded .zip file somewhere, ex. to your desktop.
Open CMD and navigate to the folder where you extracted unisniper.
First, you need to install Node.js packages.

To install required packages type:
`npm i`

Node package manager should download and install all required.
When finished, you can test if the bot works by typing:
`node bot snipe`

It should display UniSniper logo and fail on reading config.json. It fails because you need to configure the config.json.


<br/>

# Usage
## Configuration

Sample **config.json**
```
{
	"web3provider": "wss://red-red-grass.bsc.quiknode.pro/4329f98532fa1b94328c98ef2432/",
    "account": {
        "address": "0x2b33b2e2fa6f5fdb324339118eb248eab1bea2fe",
        "privateKey": "b620df502546cbf1dcb2bcb62ee9f9a8db64f5810b5bfb4fa7365890"
    },
    "token": "0xe9e7cea3dedca5984780bafc599bd69add087d56",
    "tokenBuyWith": "0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c",
    "amount": 0.1,
    "liquidityThreshold": 150,
    "profitThreshold": 50,
    "buyMode": 0,
    "buyMode1Gas": "20000000000",
    "sellGas": "7000000000",
    "buyIfLagging": false
}
```

### Settings explained
| Setting | Detail |
| --- | --- |
| `address` | your wallet address |
| `privateKey` | private key to your address. Private key can be exported from a wallet program like MetaMask |
| `token` | contract address of the token you want to snipe/buy/sell
 |
| `tokenBuyWith` | address of the token you can buy with.<br>Ex. BUSD (0xe9e7cea3dedca5984780bafc599bd69add087d56)<br/>If not set, WBNB will be used (0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c) |
| `amount` | amount to buy in BNB |
| `liquidityThreshold` | bot will buy only if the liquidity value is higher or equal to this value. Value is in BNB. If you want to disable this feature, enter value `0`.|
| `profitThreshold` | bot will auto sell if the value of bought tokens exceeds this value. Value is in %. Ex.: You bought tokens for 1 BNB. If the profit value is set to 100, bot will sell if the token value reaches 2 BNB. |
| `buyMode` | There are 2 buy modes:<br>- Mode 0: buy token as soon as liquidity transaction is spotted. Bot sends buy transaction before liquidity is confirmed.<br>- Mode 1: buy token when liquidity transaction is confirmed and spend more gas to get transaction confirmed as soon as possible. |
| `buyMode1Gas` | Amount of gas which will be used for buy transcation using *Buy Mode 1*. Higher the value, faster your transaction will confirm.<br/>Value is in Gwei. If you don't understand this setting, please, leave the default value. |


## Modes

 - **approve**
    - approves token for trading
    - it's mandatory to approve token before selling, otherwise bot won't be able to sell and transaction will fail
 - **snipe**
    - Look for add liquidity transactions and buy as soon as liquidity is added, and wait for X amount of profit, then sell tokens
    - **Steps**:
       1. look for **add liquidity** transaction
       2. buy tokens immediately as **add liquidity** transaction is spotted
       3. wait for profit
       4. sell tokens for profit
 - **profit**
    -  does NOT look for liquidity nor buys tokens. It only waits for profit and then sells.
    - **Steps**:
       1. wait for profit
       2. sell tokens for profit
 - **buy**
    - buy token immediately and wait for profit. If you don't want to profit, just stop the bot. It skips need for laggy PancakeSwap interface
 - **sell**
    - sell token immediately. It skips need for laggy PancakeSwap interface


<br/>

## How to run the Bot
### [-> Usage DEMO - Video Tutorial <-](https://www.youtube.com/watch?v=A6xSSYdJCbU)

Run bot:
`node bot <mode>`

**Example**:
`node bot snipe`
