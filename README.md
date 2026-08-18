# Online Retail II: Tableau Storytelling Dashboard

**[View the live interactive story on Tableau Public](https://public.tableau.com/app/profile/joseph.rodriguez6265/viz/online_retail_II/TheHeadline)**

This is a four slide narrative dashboard built in Tableau, using real UK e commerce transaction data spanning roughly two years, from late 2009 into late 2011. Instead of an open ended dashboard where you click around and explore on your own, this is built like a guided story. It walks you through what's happening in the business, where the friction is, and what a leadership team would actually want to take away from it.

## Data Source

This data comes from [Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii) on the UCI Machine Learning Repository, created by Daqing Chen. It covers real transactions from a UK based online retailer between December 1, 2009 and December 9, 2011.

It's licensed under Creative Commons Attribution 4.0 International (CC BY 4.0), which basically means it's fine to use and adapt as long as you give proper credit, which is what I'm doing here.

Citation: Chen, D. (2012). Online Retail II [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5CG6D

## Story Breakdown

### 1. The Headline
Revenue spikes hard every November as the holidays approach, then swings up and down the rest of the year.

This is a line chart of monthly revenue across the full date range. The point here is that the business isn't steadily growing, it's seasonal, with a sharp holiday driven spike every November.

### 2. Where It's Coming From
While the UK is the dominant home market, Ireland leads among international markets at roughly $610K, just barely ahead of the Netherlands.

This bar chart shows the top international markets by revenue. The UK is left out of the chart itself since including it at its real scale makes every other country basically invisible. Its dominance is called out in the caption instead.

### 3. What's Driving It
The Regency Cakestand 3 Tier and White Hanging Heart T Light Holder are the top two individual products by revenue, but the rest of the top 10 items combined bring in nearly 45% more, showing that demand is broad rather than resting on just a couple bestsellers.

This is a bar chart of the top 10 products by revenue. The 45% figure was double checked against the actual summed revenue for the top two products versus the remaining eight.

### 4. The Friction Point / Takeaway
Returns stay pretty steady month to month, except for one thing in January 2011: a customer placed an order for 74,215 units of the same item and cancelled it just 16 minutes later. That single cancelled order, worth about $77K, is a one off, not a real return trend.

This is a bar chart of monthly return totals, styled in its own accent color to set it apart from the first three slides. What looked at first like it might be a "returns spike after the holidays" story turned out, once I dug into the actual rows, to be one wholesale order that got placed and cancelled almost immediately. That's a finding backed by the data rather than an assumption.

## Data Quality and Analysis Fixes

A handful of issues came up while building this, both in the data itself and in some of the story's early claims.

**Partial trailing month.** The dataset actually ends on December 9, 2011. The last data point on both the revenue and returns charts originally included that partial month, which showed up as a misleading drop or spike at the very end. I trimmed both charts to end at November 2011, the last full month.

**Discrete versus continuous date field.** The Monthly Return Trends chart was originally built on a discrete Month field, which was quietly summing every instance of the same month name (every December, for example) across all three years into a single bar. I switched it to a continuous Month, Year field so each bar now represents one real calendar month.

**UK scale distortion.** Including the UK in the international markets chart, at roughly 16M compared to around 1M for the next highest country, made every other country unreadable. I excluded it from the chart and kept it in the caption for context instead.

**Verified rather than eyeballed headline numbers.** Two of the original claims turned out to be wrong once I actually checked the numbers. I had assumed the Netherlands led internationally, but Ireland actually does at around $610K. I'd also estimated the product revenue gap at nearly 50%, but the real number came out closer to 45% once I summed the actual figures.

**The January 2011 returns anomaly, checked at the row level.** Rather than take "returns spike in January" at face value, I pulled the underlying transaction rows to see what was actually going on. It traced back to one customer's wholesale order (Invoice 541431) for 74,215 units, cancelled 16 minutes later (Invoice C541433), same stock code, quantity, and price on both sides. I reframed the caption around that as an isolated cancelled order instead of a seasonal pattern.

**Caption and chart mismatches.** I also caught and fixed a duplicated sentence in the Slide 2 caption, along with a few stale axis labels that were still showing raw field names ("Description" became "Product," "Month of Invoice Date" became "Date," and "Revenue" became "Returns ($)" on the returns chart). I also relabeled the raw country code "EIRE" to "Ireland" on the chart itself, since a viewer unfamiliar with the dataset would likely read that as a typo rather than a country name.

## Tools

Tableau Desktop, Tableau Public

## Screenshots

## The Headline
<img width="815" height="772" alt="Screenshot 2026-08-18 162104" src="https://github.com/user-attachments/assets/0227cb7a-b21f-4f94-8e1f-55f164a86fc6" />

## Where It's Coming From
<img width="818" height="772" alt="Screenshot 2026-08-18 162114" src="https://github.com/user-attachments/assets/e189df4b-814b-4648-bed2-c9cfce69053a" />

## What's Driving It
<img width="817" height="770" alt="Screenshot 2026-08-18 162122" src="https://github.com/user-attachments/assets/be076497-5c2f-477c-bb12-2622c8670028" />

## The Friction Point
<img width="816" height="772" alt="Screenshot 2026-08-18 162130" src="https://github.com/user-attachments/assets/09b42497-02f0-4dbf-98d1-9595954f7d29" />

