# pairs-trading-in_indian_equities
# i have craeted this project on pairs trading where i have two parts first is the reaserach notebook where i try adn find tradable pairs and other one is the backtesting part where i backtest the selected pairs in blueshift a backtesting ide build based on zipline 
# brief on the steps done in research notebooks where I try and find congregated pairs 
1)	So the way research will go is I want to run back tests for [2016,2017,2018] separately sector by sector reason I am running back test year by year ex:I don’t want to add pairs in 2016 back test algo which were  found  in 2017 research notebook to avoid look ahead bias and also this running back test for every year separately will allow me to add pairs and remove pairs from back test algo which means 2016 backtest will have a bit different tradable pairs than 2017 back test tradable pairs  which is more realstick way of back testing as we add pairs wich are satisfying the conintigration adn remove pairs wich no more satisfyies the critiries  

2)	So I am have three research notebook [2015,2016,2017] all of them have same code but different dates so if I wanted to find pairs for 2016 back test I find pairs from stocks data from last six month of 2015 each research note book tries to find pairs for upcoming year.

3)	So the main logic to find pairs will go like this  suppose I am in 2016 right now so I will run all the test on rolling basis for last so I have calculated rolling_adf_test and rolling_beta value and I have taken mean of  rolling adf_test_pavlue  for all pairs .so as I mentioned adf_test_pvalue in my code give 95% confidence for p values below -2.9 I have kept my rolling_adf_pvalue  mean condition to -2.5  will only select those pairs which have rolling_adf_pvalue_mean below -2.5
so what exactly is rolling_adf_pvalue_mean it is the single mostimport figure in my research to find robust tradable pairs wich means pairs whos spread hold stationarity for longer durations .so as we know to find conintigrated pairs throu8gh linear regression method first we have to run linear regression on the pair and then calculate the spread through the beat coefficient adn run adf test on that spread and if the adf test pvlue is less than 5% this means we can say with 95% confidence that spread is stationary good eneough it this happens we get a cointigrted pair but think about this tells taday that the apir is tradable it might change tommoorw who knows how do you the pairs has a hihgher cahnce of holding sattionarity so thats why i use rolling_adf_test_pvlue_mean so its simple think about it like this say we run linear regression on last 90 day of data and calculated spread and ran adf_test and we got adf_pvalue wich staets wether or not series is stationary but the twist is we run all these test every day on the last 90 day data from that day so we are running all these test on rolling basis for six months so we get rolling_pvalue according to the test i am using in my research notebook 95% confidence for stationary is achieved when the adf_pvalue is below -2.8 . so if we take mean of the rolling adf_pvalue and the mean is below -2.5 mark we can say that there lot of days where the pair remained conintigrated so we select only the pairs wich are whose rolling_adf_pvalue is below -2.5 keeping it lower than this u will get very few pairs to trade

# to give u a glipse of the selectes pairs spread and rolling adf_pvalue i have plotted the spread of some tradable from my research notebook and thier respective rolling adf

![Screenshot (134)](https://user-images.githubusercontent.com/48233070/63426389-51b80700-c430-11e9-8ded-2ea46fc83759.png)

4)	This way I can check how robust the congregation is between the pairs  will they  stay cointegrated for week or two three months yes even the pairs whose rolling_adf_pvalue_mean is below -2.5 for 5 months will show non stationary spread but still they will be cointegrated almost close to around 50% on the time period on which I ran my test

5)	So, I have created a user defined function to do above mention task so in short if I run function on 6month of stock data function calculates past 60 day spread on rolling bases and run adf_test on rolling basis.



note: pls know that adf pvalues below -2.9 signifies with 95% confidence that series is stationary .

# now  the backtest part so the backtesting will be done in blueshift for every year seprately so i will run the backtest for every year seprately 
 
