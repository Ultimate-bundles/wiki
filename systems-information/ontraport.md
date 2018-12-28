<!-- TITLE: Ontraport -->

# Overview
Ontraport handles payment processessing and some parts of sales campaign management.

When a user buys a bundle, Ontraport is the first system that processes the request and either puts it through Stripe or PayPal.  Once a successful purhase has been confirmed, Ontraport sends off requests to our custom system (Laravel) to grant bundle access to the customer and start sending off emails.  It also sends a confirmation message back to PostAffiliatePro to say the transaction has been successful and a sale/commission can be recorded.

# Reporting
Ontraport processes all sales, so it's the place to go when you want to look at raw numbers.  The most useful reporting information is under:
Sales > Reports > Product Sales Logs.

# Customer Records
The form a customer fills out on the website is made and hosted with Ontraport.  Once the form is submitted, the customer's details are recorded in Ontraport along with their purchase history.

# Login
URL: https://app.ontraport.com

Login credentials for Ontraport are stored in LastPass.

