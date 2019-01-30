<!-- TITLE: Opt-In Systems -->
<!-- SUBTITLE: A quick summary of how opt-ins work in Active Campaign -->

## Landing Page
The first step of every opt-in, is the landing page. These pages are made in [Divi](http://wiki.ultimatebundles.com/systems-information/divi), and will have a URL like https://ultimatebundles.com/sale/landing-page-slug.

Somewhere on the page, there will be a code block, and that is where the form code will be embedded.

## Form
Forms are made in [Active Campaign](http://wiki.ultimatebundles.com/systems-information/divi/active-campaign). You can see all the forms there by going to the "Forms" section.

### Fields
A simple opt-in form will only have a first name and email field, but many forms have a hidden field which helps make the form more versatile for more applications. For example, the [Coming Soon / Sale Ended Notify Me](https://ultimatebundles.activehosted.com/app/forms/34) Form has a hidden field for the bundle code, so that the form can be used for all bundles. The hidden field holds the bundle code, and submits it when the customer fills out the form. Using the value in that hidden field, automations can decide how to behave.

### Style
All form styles are set in the Active Campaign form editor. You can reference other forms to see how their styles are set. Some common settings and custom styles:

**Form Style**
* Background: #ffffff
* Font Color: #000000
* Border: 0px
* Corner Radius: 0px
* Width: 800px

**Button**
* Background: #3fb9bc
* Text: #FFFFFF
* Border: 0px
* Corner Radius: 4px
* Padding: 20px

**Custom CSS**
```text
._form-title {
	text-align: center;
	font-family: 'Montserrat',Helvetica,Arial,Lucida,sans-serif;
	font-size: 36px !important;
	line-height: 36px !important;
	margin-bottom: 30px !important;
}
input {
	padding: 10px !important;
	font-size: 22px !important;
	line-height: 22px !important;
	margin-bottom: 20px !important;
}
._submit {
	font-size: 36px;
	background-color:#3fb9bc;
	width:100%;
	margin-top:5px;
	line-height: 36px !important;
	margin-bottom: 20px !important;
}
.ub_disclaimer {
	color: white;
	text-align: center;
}
```

**AC Branding**
Off

### Options
**On Submit**
This setting determines where the contact is sent after submitting the form. Typically "Open URL" is used, and the url of the thank you page is entered.

If a special landing page hasn't been created for this opt-in, you can use `https://ultimatebundles.com/subscribe` or `https://ultimatebundles.com/subscribe/your-subscribe-topic-here`

For actions, it's typically only necessary to apply a tag, although sometimes it's necessary to subscribe to a list. Regardless, it's not incredibly important, becuase typically an automation is triggered after a form submission, in which case any and all actions could also occur there.

### Integration
After editing the form, clicking "Integrate" will display the integration settings. 

Typically the form is embedded using the "Full Embed" Option in the "Embed" tab.

Simply copy and paste the Full Embed code into a code block on the landing page.

If the form has any hidden fields, this is also the time to put the values into those fields. Here's an example from the Notify Me form:

`<input type="hidden" name="field[21]" value="custom value here" />`

Further, if the page doesn't already have an opt-in disclaimer (fine print) and link to the privacy policy, include the following immediately before `<div class="_form-thank-you" style="display:none;">`:

```
<div><p class="ub_disclaimer">Your email is safe with us. We hate spam, too. By providing your email, you'll receive bundle notifications, updates and newsletters from Ultimate Bundles. You can unsubscribe any time you want.
<br><a href="https://ultimatebundles.com/privacy-policy">Privacy Policy</a></p></div>
```

Of course, adjust the wording so that it makes sense with the opt-in and any lead magnet being offered.

## Automation
Typically after a form submit, an automation needs to be triggered. This can be done using a tag (applied in the form action section, and then added as a start trigger for the automation) or using the "contact submits a form" action.

After this point, anything can be done, but usually it's just a matter of applying some basic tags ("Lead", "Newsletter", etc) and sending some emails. See some example automations for guidance:[]

[UHLB Notify Me Coming Soon / Sale Ended](https://ultimatebundles.activehosted.com/series/1354)
[Monthly Lead Magnet Delivery - December 2018](https://ultimatebundles.activehosted.com/series/1535)
[PHOSB2018 Evergreen Lead Magnet Opt-In](https://ultimatebundles.activehosted.com/series/1538)

Usually there's an email that is sent right away, which will include a link to download any lead magnets that were promised.