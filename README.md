# Gourmand Rising

Are gourmand fragrance terms (vanilla, chocolate, caramel) becoming a lasting trend in the Netherlands, and what does the next year look like?

I used Google Trends data to find out, built a forecast, tested it, and put the result in a Power BI report.

## The question
Gourmand scents smell like food: vanilla, chocolate, caramel. I wanted to know whether interest in them is a one-off or a steady climb, when it peaks each year, and what a beauty brand should expect in 2027.

## Data
- Google Trends, Netherlands, monthly, November 2021 to October 2026
- Four English search terms: vanilla perfume, chocolate perfume, caramel perfume, gourmand perfume
- Google Trends shows relative interest on a 0 to 100 scale. It is not sales data.

## What I did
1. Cleaned and explored the data in Python (pandas), including a SQL check in DuckDB.
2. Looked at seasonality: when does interest peak each year?
3. Checked the September 2026 spike. It hit all four terms at once, so I treated it as a one-off instead of letting the model learn a fake September peak.
4. Forecast to December 2027 with an exponential smoothing model (statsmodels ETS, damped trend, yearly seasonality).
5. Tested the forecast on the last 6 months and compared it with a simple guess of "same as last year".
6. Built a Power BI report with actual and forecast, a year-over-year chart and a term selector.

## What I found
- Vanilla perfume is the most searched of the four terms.
- Its yearly average rose from about 8 in 2022 to about 45 so far in 2026 (January to October, including the September spike).
- Its winter peak (October to January) has grown every year: 7, 17, 24, 35, 56.
- The forecast expects 2027 to cool but stay well above 2022 levels: an average of about 35, with November (about 57) and December (about 44) the highest months.

## How I checked it
On the last 6 months, the forecast error was **19.6** against **28.3** for "same as last year". The test months include the September 2026 spike, which no model can predict, so this is a conservative test.

## Limits
- Google Trends measures search interest, not sales. I can't say whether searches turn into purchases.
- I don't know what caused the September 2026 spike. It could be a launch, a viral post or a small group of enthusiasts. I left it as an open question.
- From November 2026 the year-over-year chart compares forecast months with actual months, so the dip in 2027 is what the model expects, not observed data.
- The year-over-year chart only makes sense for terms with steady volume. Gourmand perfume peaks at about 12, so its percentages are noise.
- The forecast band shows statistical uncertainty only. It can't know about launches, viral moments or new rules.

## Files
- `gourmand_rising_trends.ipynb`: the Python notebook with all steps and outputs
- `powerbi_trends_monthly.csv`: the cleaned data used in Power BI
- `gourmand_rising.pbix`: the Power BI report
- `*.png`: chart exports

## Tools
Python (pandas, statsmodels), DuckDB SQL, Power BI, Google Trends
