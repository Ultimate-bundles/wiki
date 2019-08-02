<!-- TITLE: Bundle Reporting -->
<!-- SUBTITLE: A quick summary of Bundle Reporting -->

https://docs.google.com/spreadsheets/d/1t52zGj4R9WE0mtNXnT8gZL8faQBXL6ntmifjrKf9FKk/edit#gid=29081565
# Bundle Reporting
The Bundle Reporting Spreadsheet is a tool designed to provide standardized insight into past and current bundle sale performance. It allows all team members to view the exact same sales numbers, combined with relevant metrics from all related systems.

This article describes it's functions

## Overview

The spreasheet has a number of important tabs. 

The **Dashboard** tab provides a place for all the useful metrics to live. If you only care about reading the data from the sheet, this is the only tab you ever need to use. It has 2 sections, allowing you to display 2 bundles' stats side-by-side for comparison. 

The **Bundles** and **Products** tabs are for describing bundles and their properties so the rest of the system can calculate their metrics properly. To add a new bundle to the sheet, the new details are entered in these tabs

The **GA Clicks**, **OP Orders**, and various Bundle **Top Affiliates** tabs are the storage locations for the data that is pulled in from outside sources. Google Analytics, Ontraport, and Post Affiliate Pro respectively.

The** PAP API Settings** tab stores settings used by the automation scripts for accessing Post Affiliate Pro.

The **Sale Groups** and **Chart Driver** tabs are the primary drivers for the "Dope Chart" seen on the dashboard. They organize and synthesize the data required to display those charts.

## Dashboard
The Dashboard displays a number of important metrics. This section will describe them in detail.

For each bundle displayed, there's some descriptive info near the top in rows 1 and 2. This includes the bundle name, open date, launch date, close date, and a setting which affects whether the sales numbers below will include purchases by affiliates, purchases by customers, or both. 

You can click on the name of the bundle and choose a different bundle from the dropdown menu to see different metrics. Ensure you wait long enough for the bundle to finish calculating, since this can take some time. A progress bar in the top right will tell you when it's ready.

The following describes the data by row and column. Since the two bundle dashboards are identical in their function, only the primary leftmost bundle dashboard will be described.

### Rows

Row 4 through 19 describe all the sales metrics for the bundle. 

Row 5 shows all the statistics for any sales made between the D-28 and D-4 dates. That is, the period of time between 28 days before the bundle opens, and 4 days before the bundle opens. This is mostly affiliate purchases, since any pre-launch sales to the public are usually closer to the bundle

Occasionally, a bundle will have a kind of pre-launch period before the official launch. These periods are almost always within the 4 days before the official launch, but ultimately are determined by the "open date" and "launch date" settings on the bundle (and displayed on row 2). You can adjust these dates in the Bundle tab to account for other scenarios.

Next, the actual bundle sale dates are displayed, usually starting in row 10, and going as far as there are days in the sale. A 6-day sale would have 6 rows, obviously.

In total there are 12 rows available for all the days between the open date and the close date. Ensure that these dates are no more than this distance apart, or else the spreadsheet will need to be expanded to account for the additional open-cart time.

Row 18 shows stats for all the days after the sale (up to 1 week after close). This helps account for time-zone differences and ensure we capture stats on any late sales.

Finally row 19 summarizes stats for all days from 28 days before the bundle to 8 days afterwards.

### Columns

Column A indicates which day the metrics belong to. Pay close attention to this since depending on the length of the sale the days may appear in different rows than you expect.

Column B is Page Views. This describes the total number of page visits to the main sales page, as determined by the Regex in the GA Clicks tab for this bundle. These page views are non-unique.

Column C is Orders. This is the number of orders of "main" bundle products as reported by Ontraport. A "Main" product is any product which is the core bundle being offered, not including bumps or upsells. Alternate versions, gifts, and affiliate versions all count towards this number, because although they are non-standard, they are still purchases of the core product. You can see which products are counted as "main" in the Products tab.

Column D is Revenue. This describes the revenue earned from the entire bundle offering, not just main products.

Column E is Bumps. This shows the number of bumps sold, for the purposes of determining how successful the bump is. If our conversion rate is low, that means very few people are choosing to take the optional bump charge, and instead going with the cheapest option.

Column F shows the bump percentage.

Column G is Upsells. This shows the number of upsells sold, for the purpose of determining how successful the upsell is. After buying the bundle, the upsell is our best attempt at convincing the customer to purchase a different related bundle. If our conversion rate is low, that means very few people are choosing to take the upsell, and are instead moving on only with their original purchase.

Column H shows the upsell percentage.

Column I shows the conversion rate of the sales page. It is essentially just Orders / Page Views. If this is low, it means our sales page isn't doing a good job of convincing visitors to buy the bundle.

Column J shows Earning Per Click. This is helpful for determining the value of each page view, mostly for calculating advertising cost. It is calculated simply with Revenue / Page Views.

Column K shows Cart Value. This is the Revenue / Orders, and shows a wholistic view of the health of our product offering. If the cart value is low (close to the base price of the bundle) that means we're not selling many bumps or upsells. Both of those actions will raise the cart value, which makes each customer more valuable to us. If the cart value is high, we might be more willing to accept lower sales numbers and still hit our targets.

### Affiliate Metrics

Below all the sales metrics are the Affiliate metrics. These show similar stats, but often with slight changes making them more useful for managing the affiliate network. All these stats are pulled directly from Post Affiliate Pro.

Each row is an affiliate, and there are 10 rows to show the top 10 affiliates. The basis of who is "top" is simply the number of sales made. If there is a tie, the results are essentially random.

These are the metrics shown for this list of top 10 affiliates:

Column A is the affiliate name.

Column B is Link Clicks. Note that this is very different from the Page Views in the same column above. Link Clicks are pulled from Post Affiliate Pro based only on how many times a visitor has clicked one of that affiliate's links in the bundle's campaign. The intricacies of this calculation are beyond the scope of this article, but essentially each affiliate link belongs to a "campaign". This is determined by a URL parameter in the link itself. When a visitor clicks that link, a click is tracked for that affiliate, in the related campaign. However, the destination of that link is not considered here. This is the most important caveat. The link clicks counted here could be going anywhere, most often the sales page, but also to pre-launch pages, or the home page.

Column C is Orders. Again note that these are not orders reported by Ontraport, but rather by Post Affiliate Pro. Since PAP has no concept of what is or is not a "main" bundle purchase, it simply counts all the 1st-tier commissions in the date range that match the campaign. The vast majority of the time, this will match the actual number of main bundles sold, but could be slightly inflated due to duplicate purchases, or if customers purchase the base bundle first, and then upgrade to include cheat sheets later. Note that this does *not* include upsells, since those are counted in a different campaign than the main bundle.

Column D is Revenue. This is the revenue earned by all the sales, as described above in the explanation of Orders. This is not the revenue earned by the affiliate, but rather the revenue earned by us, which their commissions are calculated on.

Column E is Commission Dollars earned. This is the amount of money earned via commissions on all the orders described above.

Column F is the effective commission rate of this affiliate. It will almost always be 40%, 60% or 70%, since upsells are counted in a different campaign. However, there was a time when this percentage would vary as affiliates earned different amounts for different products. The actual calculation is simply Commission / Revenue.

Column I is the conversion rate for the affiliate. The calculation is Orders / Link Clicks, but as discussed above, doesn't always provide meaningful insights. It also does not account for volume at all, so early in the sale the numbers will fluctuate wildly. Also note that since a customer does not need to click an affilaite's link and then *immediately* purchase in order to count as a commission for that affiliate, sometimes you'll see affiliates with a 0% conversion rate since they have no link clicks but a number of sales. This is caused by customers who have clicked that affiliate's link in the past, and then landed on this bundle's sales page by other means. This results in a commission for the affiliate, even though they may not even be promoting this bundle.

Column J is the Earning per Click for the affiliate. Again this is not the revenue earned by the affiliate for each of their clicks, it is the revenue earned by us for each of their clicks. It's calculation is Revenue / Link Clicks.

Column K is again cart value, calculated by Revenue / Orders.

## The "Dope Chart"

Below all the sales and affiliate metrics is a chart. It's called the "Dope Chart", but a more accurate title would be "Actual revenue over time, compared with budget and target". It has 3 lines:

Black: This line shows the actual and projected revenue for a bundle. If the line is solid, it's showing actual revenue that actually happeend. If it's dotted, that is a projection based on how past similar bundles have behaved.

Blue: This line shows the budgeted revenue over the course of the sale. That is, it shows what the black like *should* look like, if we're heading towards exactly the budgeted total revenue amount. It's shape is determined by how past similar bundles have behaved.

Orange: The orange line is the target. It works exactly the same as the blue line, but heads towards a higher number; the targeted revenue for the bundle, not just budget.

This chart is used for a single purpose: to see how close we are to achieving budget or target based on how many sales we've made so far in the sale, and how past similar sales have behaved. We predicte how this sale will go using past data. It's a simple calculation but quite effective.

## Data Sources



## Loading New Bundles

## Automatic Data Collection

## Maintenance