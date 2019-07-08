<!-- TITLE: Referral Program -->
<!-- SUBTITLE: A quick summary of Referral Program -->

# Overview
The referral program is a new system used to encourage customers to tell their friends about bundles. Customers who do this may earn rewards in the form of coupons. Here's how the system works

# New Customer Referrers
Whenever a customer purchases a bundle, they'll become a "Referrer". This simply distinguishes them from other past customers who purchased before the system was in place, and is also the name of the entries created in the database. It comes up occasionally in the systems, code, and documentation. The Referrer object stores information about the customer (for identification purposes) as well as a master record for Referral Codes, Referrals, and Rewards.

All new Referrers are issued one Referral Code, which is available to be used immediately. Technically, there is a small chance this referral code will not yet be created in the database by the time the customer earns their first referral click, so most of this is handled client-side, reducing load and accounting for any back-end lag.

If the Referrer was also referred by someone else, that purchase can also generate a reward for the original referrer.

# Referral Codes
Referral Codes are the core of the system. They are an 8-digit string containing mostly upper and lower case letters (although numbers are valid, they are currently not being included when generating new codes).

Here's how Referral Codes are generated.

1. A potential customer visits the order form. Silently, some JS on the order form generates a random 8-digit string. It sends a message to the Referral Program server to check if it's available, although the odds of a collision are 1:53,459,728,531,456 (1 in 53 Trillion).
2. The code saves the code in the user's browser with the cookie `ub_referral_code`
3. The code enters the code into a hidden field on the order form. This will pass it through to ontraport if the user purchases, saving it on their profile.
4. The code also checks for a value in the `ub_referred_by` cookie, and if there is a value there, passes it through the form in the same way.
5. The user purchases the bundle, submitting the order form.
6. The regular purchase actions are triggered, including a request to the Referral Program, which registers the referral code.

# Referral Links
There are two types of referral links, Standard and Redirect.

## Standard Links
Example: https://ultimatebundles.com/sale/heosb2019-main?ub_rid=abcd1234

This is simply a link to the sales page with a URL parameter containing the Referral Code. Upon arrival at the sales page some code on that page will read the value and set a `ub_referred_by` cookie on the user's browser. This is useful because any number of other url parameters can be added to the link without impacting the Referral Program systems whatsoever. For example, this is also a valid Standard Link: https://ultimatebundles.com/sale/heosb2019-main?ub_rid=abcd1234&a_aid=a1234

## Redirect Links
Example: https://ultimatebundles.com/r/abcd1234

When Referral Codes are created, some additional information is passed through to the Referral Program API. This includes a sales page URL and an Affiliate ID (from Post Affiliate Pro). If this data is set, then a Redirect Link can be used (in addition to Standard Links). 

They work very simply. When a user goes to a Redirect Link address, the controller first does a search for the referral code. If it finds one, it then checks for a destination and affiliate code stored on the Referral Code in the DB. If it finds them, it will construct a new Standard Link in memory and redirect the user to it. 

For example, the Redirect Link above uses the code `abcd1234`. Lets say that in the DB, this Referral Code contains the destination `https://ultimatebundles.com/sale/stsb2019-main` and the affiliate ID `a0987`. That means any time anyone visits that Redirect Link, they'll automatically be sent to `https://ultimatebundles.com/sale/stsb2019-main?a_aid=a0987&ub_rid=abcd1234`.

In short, Redirect Links allow a short, pretty URL to be used instead of a Standard Link, but are a bit more limited since the link is constructed on the fly.

# Referrals
Whenever someone clicks on a referral link, they are cookied with the Referral Code it contains. The Referral Code itself is saved in the `ub_referred_by` cookie.

If that user purchases a bundle, the value of the cookie is passed through the order form and will trigger a reward to the Referrer who owns that Referral Code.

# Rewards
Whenever a purchase is triggered which was referred, a reward is triggered as well.

These rewards are in the form of $10 coupon codes in Ontraport. When issuing a reward, the system will first check if the user has any $10 coupons already. If so, it'll add the new coupon to that total resulting in a new, single $20 coupon. If they have no coupons, or no $10 coupons already, a new $10 coupon is granted.

These rewards can be managed here: https://app.ontraport.com/login.php#!/coupon/listAll

The name of the reward will contain the best information we have about who owns it. Either an email address (in most cases) or a referral code if something went wrong along the way.

# Training
A slide deck about the referral program is here: https://docs.google.com/presentation/d/1fpQHioe9zCGcXSOKNN4a8XIvy7EC-4jQ36TS-LiwnyM/edit#slide=id.p

The above information, and much more was covered in a recorded training session, visible here: https://drive.google.com/open?id=1FWs-IdEXtwuNNqXadkzU0o8NoObukgkU