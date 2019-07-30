<!-- TITLE: Bundle Sale Counter -->
<!-- SUBTITLE: A quick summary of Bundle Sale Counter -->

# Bundle sale counter

The bundle sale counter is a set of utilities that work together to display the number of bundles sold during a sale on a sale page. This provides social proof to potential customers.

## Requirements

To display a bundle sale counter on a sales page, a number of steps must be completed.

### Page elements

The actual display of the counter is built in divi on the sales page. This allows us to design it however we'd like, as long as it meets a few requirements. These are...

1. A parent element which houses the entire bundle sale counter. It must have the class `.counter-row` and have the styles `display: none`. This makes the bundle sale counter hidden by default. More on that later.
2. A span somewhere in the counter which contains ONLY the number of bundles sold. It must have the class `.bundles-sold-count`. For example, `<span class=".bundles-sold-count">0</span>` is acceptable, while `<span class=".bundles-sold-count"><div class="foo"><p>The number sold is 0</p></div></span>` is not. This is because the script which powers the counter will look for all elements with the class `.bundles-sold-count` and replace their *entire* contents with the number of bundles sold. If the elements contain any markup, it will be deleted.

A key requirement of this feature is that the number of bundles sold is only displayed if a certain threshold has been met. Obviously it doesn't offer any social proof if we say something like "2 bundles sold!". We want to wait until that number is much higher, then display the number of bundles sold.

This is the reason that the container is hidden by default. The script will target that container, and if the threshold has not been met, simply leave it alone. If the threshold has been met, that means the counter can be displayed, and the script will display it.

### Stats API Configuration

The actual system works on a simple API that exposes the number of bundles sold under certain conditions. The data that is returned can be [configured in Divi here](https://divi.ultimatebundles.com/wp/wp-admin/admin.php?page=acf-options) under the "Bundles Sold API" tab.

In this tab, you can configure "preset", which are kind of like endpoints of the API. You specify a label for the preset, as well as some other details, and this allows the bundle-sale-counter.js script to contact the API and get the number of bundles sold.

These are the settings and how you can configure them:

#### Label

This determines the endpoint that you will use to contact the API and get the number of bundles sold. Choose a label which is simple, unique, and all lower-case. Usually the bundle code is ideal.

The endpoint used is determined by this label like so: If the label is `uhlb2019`, then the endpoint to access it is `GET /stats/uhlb2019`.

#### Display Criteria

These settings determine under what conditions the counter will be displayed. It can be always enabled, always disabled, or use conditions to decide whether it should display or not. These conditions include a minimum number of sales which must be made before it will display, as well as a date range that controls when it can be displayed.

#### Search Criteria

Ultimately the API works very simply. When the bundle-sale-counter.js script hits the endpoint, the application makes a query to Ontraport for the number of sales. However, it must include some search criteria to find the correct number. These settings determine how the application will search for valid sales to add to the count.

You can specify a date range, which will make the search only count sales that happened between the two dates, and you can specify the exact products that count towards this bundle. It's most common to simply choose the dates of the sale itself, and base products of the sale like the main bundle, early bird, gift bundle, and affiliate version. Do not include any ugprades, bump products, add-ons, or upsells, since these artificially inflate the count of bundles sold.

### bundle-sale-counter.js

This is the actual script which connects the elements on the sale page with the stats API. Most of the time you can simply copy/paste it into a code block at the bottom of the sales page in divi, changing only the API endpoint it will use to get the updated stats.

It works very simply, contacting the stats API on page-load, and if it gets a valid response it will display the counter on the page and update the count of bundles sold. If it gets and invalid response, it will do nothing, thereby leaving the counter hidden.
