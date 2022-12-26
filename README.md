# An Overview of Machine Learning Models on Crypto Clustering and Price Prediction on Binance.

## INTRODUCTION
Cryptocurrencies are known for their volatility and susceptibility to scams, making it difficult for investors to navigate the market. Unlike the traditional stock market, there is not much research applied to the crypto market. With the abundant data online and the growing interest in cryptos and blockchain tech, using crypto clustering and price prediction tools can help investors mitigate some of these risks and make more informed decisions. 

The dataset is generated directly from the market via Binance API. In brief, Binance is the biggest centralized exchange in the world. All the cryptos that are listed on Binance must pass Binance’s internal criteria. Even though there are only 409 crypto pairs listed on Binance, they are more valuable to investors than over 1000 pairs in the whole crypto market.

## CLUSTERING
K-means Clustering is an unsupervised machine-learning (ML) model that groups cryptocurrencies based on the similarity of their price-volume movement. The model recommended 5 clusters which are found at the elbow in the Inertia plot and the highest of the Silhouette Score. Based on the model and domain knowledge, the following clusters are below (Plot attached below for reference):

![](assets/CLUSTERING%20-%20Map.png)

#### Group 0 - Small Cap: 
Contains small-cap cryptos. They contain some quality projects with a strong team and are backed by VCs. Similar to Group 0, they have low prices and high volume, suitable for trading. However, they may not be the best to hold long-term.

#### Group 1 - HR/HR Yield Farm: 
Contains gold-back or high-risk/rewards yield farm (crypto banks that offer high returns if you deposit into their coins). They have a high price but low volume, not suitable for retail trading. 

#### Group 2 - OG: 
Contains mostly original and well-known cryptos such as BTC, and ETH. They are highly safe to hold for long-term periods. Most of these cryptos have low prices and high volume (aka. High liquidity) which are suitable for trading.

#### Group 3 - Penny: 
Contains penny cryptos. Very small in values like meme coins: BabyElon, BabyDodge, high risk, high reward. likely a pump-dump scheme. They have characteristics of Group 2 and 3, except, group 4 is a very low price and very high volume, thus, the volatility is extreme. Take caution when trading.

#### Group 4 - Trash: 
Contains high-risk but also high-return crypto projects like Squid Coin (Pump and Dump scheme based on the Squid Game Netflix series) with unknown teams or backers. Only suitable for the pump-dump scheme. Trade or buy with CAUTION.

#### Group 5 - Delisted (manually created): 
Coins that are not clustered in 2022 which means they were delisted before 2022. This cluster behaves similarly to Group 3 in both price, volume, and the number of trades. Only for reference, cannot trade or buy these cryptos anymore.

### Comparison: 
Comparing to similar works online that use Kmeans clustering on cryptocurrencies, I found that everyone took a different approach and solution on how to use Kmeans to cluster cryptos. In addition, not many works have been done in the crypto space, mostly with the stock market. I believe my business approach will bring clarity to the investors. 

### Improvement: 
Due to the complexity of the dataset and relevance for the business use case, the clustering is based on only data in 2022. Thus, some cryptos that were delisted before 2022 will be manually put in group 5. An improvement model will include these delisted cryptos as well. In addition, I can try different clustering methods, or feature engineering to simplify the clusters. Lastly, if the same clustering can be applied to the whole crypto market, it will be more valuable as there are over 1000 cryptos and it will give better insights to the mass than just within Binance ecosystem.

![](assets/CLUSTERING%20-%20Price.png)
![](assets/CLUSTERING%20-%20Volume.png))
![](assets/CLUSTERING%20-%20Number%20of%20Trades.png)

## Price Prediction
Price prediction algorithms can also be used to forecast the future value of cryptocurrencies. SARIMA and FBProphet are the 2 models which predict the CHANGE in the price of the representative crypto in each cluster. Then, the actual price prediction is reconstructed to show the future price.

There are 6 price predictions in total for each cluster group from 0-5. However, due to insufficient data by delisting, Group 4 and 5 cannot produce any meaningful prediction. On the other hand, the MAPE (ie. mean error, the lower the better) for Group 0,1,2, and 3 are all less than 1% for both SARIMA and FBProphet. These are the score when predicting 10 days or less. MAPE score increased significantly more than 10 days. 

### Comparison: 
Other price prediction models available seem to use prediction directly on the Price data frame rather than the price CHANGE. Such as FBProphet has the option to predict the future with just historical price. Thus, our model is better and more logical as we predict the change in price which is stationary. 

### Improvement: 
An improvement would be including LSTM RNN in the price prediction which many articles were written about. Another improvement would be setting up a live and real-time price prediction for the business use case.

![](assets/Daily%20Price%20Prediction%20BTCUSDT.png)

![](assets/Daily%20Price%20Prediction%20BAKEUSDT.png)

## Conclusion
This project set the foundation for more complex projects such as real-time clustering and price prediction of cryptos. In addition, algo trading bots would also be benefits from this project as it depends on the price prediction to make buy and sale orders.
 
In conclusion, while these tools can help investors mitigate some of the risks associated with investing in cryptocurrencies, it is important to remember that the market for cryptocurrencies is still highly unpredictable and investing in them carries significant risks. Investors need to conduct thorough research aka. DYOR (Do Your Own Research) and consult with financial professionals before making any investment decisions.

# Citation
Use this bibtex to cite this repository:

```
@misc{thai22011_Crypto_Clustering_PricePrediction_2022,
  title={An Overview of Machine Learning Models on Crypto Clustering and Price Prediction on Binance},
  author={Thai Nguyen},
  year={2022},
  publisher={Github},
  journal={GitHub repository},
  howpublished={\url{https://github.com/thai22011/Crypto_Clustering_PricePrediction}},
}
```

# Contributing
Contributions to this repository are welcome. Examples of things you can contribute:

* Real-time data extraction
* Real-time Clustering
* Real-time price prediction for 1min, 5min, 15min 
* Improvement on Price Prediction Model such as LSTM RNN

# Requirements

The `python-binance` package is ONLY required for notebook 1.CRYPTO - Thai Nguyen - Data Collection.ipynb
Other notebooks do not require special package

```
conda create -n timeseries python=3.8 numpy pandas matplotlib seaborn statsmodels scikit-learn==0.24.1 datetime dateutil jupyter jupyterlab

conda activate timeseries

conda install -c plotly plotly=4.14.3

conda install -c conda-forge fbprophet=0.7.1

pip install python-binance

ipython kernel install --name "timeseries" --user
```
