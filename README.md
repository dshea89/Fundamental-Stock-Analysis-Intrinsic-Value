# Fundamental-Stock-Analysis-Intrinsic-Value

## Preamble

This repository has been forked from its original codebase and modified here to resolve the issues that caused the original build to no longer function (library updates deprecating some functionality, Google Finance going down, certain function calls from other libraries no longer operating due to other API and library issues of their own, and so on). Data is retrieved from Yahoo Finance.

### Summary 

In this application, we will be analyzing the intrinsic value of stocks using various valuation methods and financial ratios. Investors such as Warren Buffet and Benjamin Graham are just a few examples of people who use a fundamental analysis approach to value stocks based upon their intrinsic value. Below I will talk about how this app works and the motivation for this type of automated analyses:

I have taken a class from [https://www.udemy.com/value-investing-bootcamp-how-to-invest-wisely] which goes over how to go over fundamental stock analysis like those legendary investors mentioned above. I needed a way to apply the things learned in this course without having to do manual calculations for every single stock to come up with an intrinsic value estimate. Before using this app, it is highly reccommend that you take the class on Udemy which was referenced earlier in this paragraph. If you navigate to Steps 2 and 3, that will explain the fundamental analysis and valuation methods that are provided by the application.

### R Packages

To run this project yourself, you must install the following packages:

* quantmod
* shiny
* reshape
* ggplot2
* plyr
* rvest

### Run

Just open and run 'app.R' in the R environment. A page will launch in your web browser allowing you to interact with the app.

## Value Investing Process

### Step 1: Initial Screening - Manual Process

An initial stock screener can be done on Yahoo Finance. There are thousands upon thousands of companies in which you can buy stock. You need to use an initial stock screener to narrow down your search. Use the following filtering criteria to narrow down more specific stocks:

1. Filter for companies with return on equity greater than 15%
Return on equity tells us how efficiently a company uses its assets to generate earnings. The higher the return on equity, the better. This is calculated by:
Net Income / Shareholders' Equity = Return on Equity

2. Filter for companies with a current ratio greater than 2%
If the current ratio is greater than 1, then the company has the ability to pay its short-term liabilities with its short-term assets, as the company has more short-term assets than debt. You want a company with more money than bills to pay. If the ratio is less than 1, then the company may be vulnerable to unexpected events in the economy and it will be hard for them to pay their bills. To calculate, it is found in the balance sheet:
Current Assets / Current Liabilities = Current Ratio

3. Filter for a debt-to-equity ratio less than 0.5 (50%)
This ratio indicates how much debt a company is in related to its shareholders' equity. High debt levels are a huge warning sign, as it relies on debt to finance its growth. If a company has an increasing debt-to-equity ratio, then the investment may become risky because the company cannot meet its debt obligations. Calculated by:
Long-Term Debt / Shareholders' Equity = Debt-to-Equity Ratio

### Step 2: Fundamental Analysis

1. **Are earnings per share stable or growing over time?**

Earnings per share is the profit that a company makes per share of stock. A growing EPS is better than decreasing or stable. Calculated by:
Net Income / Shares Outstanding = EPS 

2. **How does the Price Earnings (PE) Ratio compare to the rest of the industry?**

P/E ratio is the price that you will pay for the stock per dollar of income. This ratio generally differs greatly per industry. A low P/E ratio compared to other stocks in that industry generally means that the shares are trading at value. Calculated by:
Price per Share / Earnings per Share = P/E Ratio

3. **Are free cash flows stable or increasing over time?**

FCF is used for paying debts, dividends, buybacks, or investing in growth for the company. Free cash flow is a very immportant metric for companies as it is hard for companies to manipulate their free cash flows. Also, cash is king! Calculated by taking: 
Cash from Operating Activities – Cash from Capital Expenditures

4. **Are cash and cash equivalents stable or increasing over time?**

Reported on the balance sheet. An increasing value means that there is more cash reserves over time. Even if this metric is decreasing, the company could just be investing the reserve money to improve the business.

5. **Is book value per share steadily growing over time?**

This shows how much money you would receive for your shares of stock if the company liquidates, selling all of its assets after paying off its debts. You want to look for companies with increasing book value per share because they are companies that are creating value. To calculate:
Shareholders' Equity / Shares Outstanding = Book Value per Share

6. **Is the net margin stable or growing over time?**

Net margin is what percent of sales is profit. This figure differs greatly from industry to industry. If a company is able to sustain high profit margins, then the company may have a strong brand name or patented products that competitors can't compete with. The higher the net margin, the better. Calculated by:
Net Income / Revenue = Net Margin or Profit Margin

7. **Has the return on equity been consistently high?**

Return on equity tells us how efficiently a company uses its assets to generate earnings. The higher the return on equity, the better. This is calculated by:
Net Income / Shareholders' Equity = Return on Equity

8. **Has debt-to-equity been consistently low or decreasing?** 

This ratio indicates how much debt a company is in related to its shareholders' equity. High debt levels are a huge warning sign as it relies on debt to finance its growth. If a company has an increasing debt-to-equity ratio, then the investment may become risky because the company cannot meet its debt obligations. Calculated by:
Long-Term Debt / Shareholders' Equity = Debt-to-Equity Ratio 

### Step 3: Valuation

In this step, we calculate the intrinsic value of a stock based upon two various methods: The Price Earnings Multiple Valuation Method and the Discounted Cash Flow Valuation Method.

1. **Price Earnings Multiple Valuation Method**

o	In this method, a five-year price target is determined based on historical P/E valuation. We will take three inputs to calculate a five-year price target for the company.

o	Input 1: Find the median P/E ratio over the past five years. In this example, we will use 19.0

o	Input 2: Find the company’s earnings per share over the most recent four quarters. This may be listed as "EPS (ttm)" or earnings per share trailing twelve months on various sites. This is calculated by just adding these four quarter EPS figures together. In this example, we will use $2.00

o	Input 3: Now estimate a value at which you expect the company will grow its profit each year for the next five years. You can use analysts' growth rate percentage. Make sure to use the Margin of Safety principle to give your estimate room for error. For example, if analysts predict that the company's profit will grow 10% each year, then use a 15-25% margin of safety buffer. This means that your growth rate estimate will be conservative and, if we use a 25% margin of safety buffer, we will arrive at a value of 7.5% (10 percent estimated growth rate * (1 – .25 margin of safety))

o	Now, using the three inputs, we can arrive at this formula for a five-year price target (the exponent represents the number of years):

	19 * $2.00 * (1 + .075) ^5 = $54.55 

	This value is what the stock price would be five years from now. To calculate what the stock is worth today, or its intrinsic value, we need to discount the five-year price target, which gives us the net present value (NPV). 10% is a good discount rate to use because it is equal to the long-term historical return of the stock market. It is the minimum rate of return to justify picking a stock over investing in an index fund.

o	To calculate the Net Present Value:

	$54.55 / (1 + .10) ^5 = $33.87

	This, per the P/E Valuation Model, states that the intrinsic value and NPV of that stock is approximately $33.87. 

2. **Discounted Cash Flow (DCF) Model**

o	The DCF Model projects future cash flows and discounts them back to the present value. This is a valuation method that estimates the intrinsic value of an investment opportunity. The discount rate represents the riskiness of the company's capital. You then add up the net present value of the cash flows, which is the intrinsic value of the company.

o	Cash flows are generally projected 5-10 years. More mature companies who do not expect as much growth in cash flows, such as Coca Cola, will use a 5-year free cash flow projection. In this example we will use a 5-year DCF model.

o	Step 1: Calculate the company's capital expenditures from the last four quarters. Sum it up. In this example, we will use $7,207

o	Step 2: Calculate the company's cash from operating activities. Sum it up. In this example, we will use $53,944

o	Step 3: Take the cash from operating activities and subtract the capital expenditures. This will give us free cash flow (FCF)

	$53,944 - $7,207 = $46,737

o	Step 4: We then decide a growth rate of the company for the next five years. This can be analysts' estimates or your own estimate. If analysts decide that the company will grow at 15.37% each year for the next five years, then use a 25% margin of safety. This means that the conservative growth rate will be (15.37 * (1 - .25)) = 11.53%. **In this application, the automatic selection option is to have the growth rate at a negative value. All this means is that, if the growth rate is negative as shown in the app, then the calculation for the growth rate value is as follows: The slope of the line of best fit through all historic cash flows is calculated. A predicted free cash flow value is predicted based on this slope one year into the future. Then the growth rate is the percent change of the most recent free cash flow (ttm) value to the predicted free cash flow value one year into the future.**

o	Step 5: As a company grows in size, it is hard to maintain a high growth rate, so each year, the conservative growth rate will decline by 5%.

o	Step 6: We take our free cash flow of $46,737 and then multiply it by the conservative growth rate of 11.53% to get the free cash flow one year from now: 

	(46737 * 1.1153) = $52,125 FCF for year one.

o	Step 7: Then we discount this future cash flow value using 10% to get the NPV of the first year's free cash flow

	$52,125 / (1 + .10)^1 = $47,386 NPV FCF

o	Step 7: Then, every year after the first year, we apply the growth decline rate of 5%. Calculating the second year free cash flow:

	$52,125 * (1 + (.1153 * (1-.05))) = $52,125 * 1.1095 = $57,834 FCF for year two

o	Step 8: Then we discount this future cash flow value using 10% to get the NPV of the second year free cash flow

	$52,125 / (1 + .10)^2 = $47,386 NPV FCF

o	Step 9: Continue the process until the 5-year FCF and NPV FCF are calculated.

o	Step 10: Take the value of the year 5 FCF, $76,747.49. You would then need to calculate the terminal value, which is the company's long-term valuation as the company approaches perpetuity.

o	Step 11: To calculate the terminal value using the Gordon Growth Model, you also need to come up with a long-term cash flow growth rate. The long-term growth rate for cash flow in the US economy is around 3%, so we will plug that value in the following formula.

	Terminal value = projected cash flow for final year (1 + long-term growth rate) / (discount rate - long-term growth rate)

	$1,129,284 = $76,747.49 * (1 + .03) / (.1 - .03)

o	Step 11: Now calculate the net present value of the terminal value. The exponent is the last year that you calculated for the terminal value.

	$1,129,284 / (1 + .1)^5 = $701,196

o	Step 12: Now find the cash and cash equivalents on the balance sheet. In this example, we will use $41,350. Now find long-term debt balance on the balance sheet. In this example, we will use $16,962.

o	Step 13: Take the following inputs and add (subtract debt though) to get the company value using the DCF model.  

o	Step 14:  Take the company value and then divide it by the number of shares outstanding, which will give you the value of the stock price using the DCF model.
