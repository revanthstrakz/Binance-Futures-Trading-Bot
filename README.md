# Binance-Futures-Trading-Bot [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Check%20out%20this%20free%20Binance%20Trading%20Bot%20I%20found%20on%20Github%20&url=https://github.com/conor19w/Binance-Futures-Trading-Bot&hashtags=Trading,Bot,Trading_Bot,Cryptocurrency_Trading_Bot,Crypto,Bitcoin,Ethereum,Cryptocurrency,Binance,DOGE,dogecoin)
---
## To-Do list: (suggest something and I'll add it) 😃
* Trailing Stop
* Upload Backtesting results for some strategies over last two months
* Add option to overwrite saved price data so as not have to manually delete
* Maybe Provide a standard bot strategy for Bot...
* GUI if people were interested (could take a while I've no experience here)
* Speed up Data Set aligner in Backtester with multiprocessing
---
## Latest Changes (if any):
* Mainly Bug fixes lately no new features.
---
## Technical Analysis driven Crypto Trading bot on Binance Futures 📈 ₿ 🚀 [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Check%20out%20this%20free%20Binance%20Trading%20Bot%20I%20found%20on%20Github%20&url=https://github.com/conor19w/Binance-Futures-Trading-Bot&hashtags=Trading,Bot,Trading_Bot,Cryptocurrency_Trading_Bot,Crypto,Bitcoin,Ethereum,Cryptocurrency,Binance,DOGE,dogecoin)
[__Join My Discord Server__](https://discord.gg/jBu6thyP66) __&__ [__Follow The Twitter__](https://twitter.com/futures_bot)
* Utilizes [python-Binance](https://python-binance.readthedocs.io/en/latest/) Client to execute orders and pull data from Binance
* Utilizes [ta](https://technical-analysis-library-in-python.readthedocs.io/en/latest/) library for Technical indicators
* Write your own functions/classes to implement your TA strategies.
* There is no default Strategy implemented you must do this in Data_Set.py as specified below.
* Comes with some pre-coded strategies found in [TradingStrats.py](https://github.com/conor19w/Binance-Futures-Trading-Bot/blob/main/TradingStrats.py)
* If you enjoy the repo please share it around to friends & tweet about it using the tweet button above 😃   
or [Buy me a Coffee](https://www.buymeacoffee.com/conor19w)
* Min version = python 3.7 
## Binance Setup
---
* Create a [Binance Account](https://accounts.binance.com/en/register?ref=BKR8BMMP) (This link uses my referral which gives you 5% kickback on trades & would be greatly appreciated)
* __Enable Two-factor Authentication in the security section to keep your crypto safe.__
* Create a new API key under the API Management section.
*  [✓] Read Info [✓] Enable Trading [✓] Enable Futures [X] Enable Withdrawals
* Whitelist your IP address to further secure your account, and so that your API keys don't expire after 1 month.
* Fill in your api keys into api_secret and api_key in [API_keys.py](https://github.com/conor19w/Binance-Futures-Trading-Bot/blob/main/API_keys.py).
* ---
### YouTube Channels with Strategy Ideas:
[__Trade Pro__](https://www.youtube.com/channel/UCrXjzUN6EtlyhaaAerbPfkQ) | [__Strategy Testing__](https://www.youtube.com/c/TradingStrategyTesting) | [__Trading Journal__](https://www.youtube.com/c/TradingJournal1) | [__Critical Trading__](https://www.youtube.com/c/CriticalTrading) | [__The Moving Average__](https://www.youtube.com/channel/UCYFQzaZyTUzY-Tiytyv3HhA)  
---
### Back test strategies in [Backtester.py](https://github.com/conor19w/Binance-Futures-Trading-Bot/blob/main/Backtester.py)
---
* Create a list named 'symbol' of coin/coins you wish to run a strategy on ie. symbol = ['BTCUSDT' , 'ETHUSDT'] , this would run your strategy on BTC and ETH.
Whereas symbol = ['BTCUSDT'] would run the strategy on BTC only.
* Ignore the __pair-trading__ section and ensure pair_Trading = 0, if you are executing a TA strategy
* The data is split into an in-sample set and a test set, the flag __test_set__ decides which set we are running the strategy on, both sets are in same units as test_set_length but we adjust __time_period__ variable to change the in-sample data set length. The reason for splitting the data like this is to optimize parameters on the in-sample set and then once optimized run the strategy on the test-set to see if you have overfit your model by cherry picking values for parameters that suit the in-sample data.
* The __time_period__ variable is the length of time in the past from today excluding the test-set, to run the strategy on. This is in the same units as the test_set_length.
* The __TIME_INTERVAL__ variable is the interval for the candlesticks we want to trade on.
* Next we want to choose our TA strategy, this is done after __line 295__ , uncomment a strategy or call a new strategy you have written yourself here, the 'prediction' variable is used to tell the script to go short (0), go long (1), or go flat (-99). This should be returned by custom strategy functions/classes you write for the strategy to be executed correctly
* Some of the pre-coded strategies return a 'Type' variable, if a strategy returns the 'Type' variable you must call the SetSLTP() function from __TradingStrats.py__ in order to set the corresponding Stop loss value, and Take profit value, this function is found in TradingStrats.py
* Now just run the script and wait a few minutes for it to pull the data and begin backtesting
* use_heikin_ashi is a flag __line 145__ that will create the heikin ashi candles for use, Called CloseStream_H, OpenStream_H, LowStream_H, HighStream_H which can be referenced or passed to Strategies.

#### Using Downloaded data for backtesting
---
* Reason to do this is to speed up backtesting 
* Create a folder on the desktop called __price_data__.
*  In __download_Data.py__ change the __path__ to f"C:\\Users\\your_name\\Desktop\\price_data  
__replacing your_name with the user that you are logged into.__
* Switch __load_data__ on in __Backtester.py__ on __line 120__, now when you run the script it will load from the folder & if the specified candlestick data isn't present in the folder then it will be downloaded and saved for future use.  
__NOTE: this data is static so if you want up to date data in future you will have to manually delete the data from the folder on your desktop and then run the script again.
Otherwise you can just turn load_data off and pull data from the server everytime you want to run a backtest.__
#### Strategy_Tester.py
---
__This script will run a strategy on every coin on Binance & then generate graphs and statistics which are saved to a folder on the desktop.__
* __Line 29 to Line 43__ are the settings which should be clear with the comments I've provided
* Create a folder on the desktop called Strategy_tester with another folder matching the __Strategy_name__ variable, this is where the data will be stored when you run.
* Change __path1__ on __line 44__ to reflect the location of the Strategy_tester folder you've just created.
* Uncomment a strategy after __line 258__ or else call your custom strategy here, following the same guidelines layed out in the backtesting section above.
* Now run the script with the settings you've chosen and check up on the graphs and statistics that are created soon after.
---
### Run strategies live in [Bot.py](https://github.com/conor19w/Binance-Futures-Trading-Bot/blob/main/Bot.py)
---
__Run strategies at your own risk I am not responsible for your trading decisions, futures are risky and proper risk management should be adhered to at all times, always have a stoploss__
---
* In __Bot.py__ on __line 334__ are the settings.
* Choose the Interval you want to trade and the buffer of candlesticks your strategy will need.
* leverage and order_size should be changed acording to your preference
* symbol[] is a list of the symbols you wish to trade, the default is all the coins on the exchange currently.

__Strategies are implemented in Data_Set.py as a function named Make_decision() in the Data_set class__
* Make_decision() must return Trade_Direction,stoplossval,takeprofitval for the strategy to work properly
* You might draw inspiration for a strategy from one In __TradingStrats.py__
---
###### (Depreciated) Run strategies live in [Bot__(depreciated).py](https://github.com/conor19w/Binance-Futures-Trading-Bot/blob/main/Bot__(depreciated).py)

# Contact me [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Check%20out%20this%20free%20Binance%20Trading%20Bot%20I%20found%20on%20Github%20&url=https://github.com/conor19w/Binance-Futures-Trading-Bot&hashtags=Trading,Bot,Trading_Bot,Cryptocurrency_Trading_Bot,Crypto,Bitcoin,Ethereum,Cryptocurrency,Binance,DOGE,dogecoin)
* If you have any querys about anything, or need me to explain any blocks of code please reach out to me at wconor539@gmail.com.
* If you have any suggestions or requests please reach out to me as well.  
[__Join My Discord Server__](https://discord.gg/jBu6thyP66) __&__ [__Follow The Twitter__](https://twitter.com/futures_bot)
