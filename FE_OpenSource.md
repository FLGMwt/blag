# Your Front-End is Open Source

This past weekend, I thought I'd poke around and see if there was an alcohol delivery service among the Instacarts and Amazon Prime Nows of the world. Since [avocado delivery in the Bay area](http://www.goavocago.com/) is now a thing, I was thankful to see that [Drizly](https://drizly.com) has taken up the torch of bringing booze to the lazy. 

Their front end is pretty solid, but in the checkout process, there was a "tip amount" field that didn't format currency amounts properly, resulting in the value of "5.7" as opposed to the "5.70" that I would expect. Being a developer, I popped open the console to see if I could find the offending javascript code. Before I switched to the "Scripts" tab, I noticed some ng-* attributes. I haven't done much Angular, but I remembered enough from a couple tutorials to know that number formatting is the perfect match for Angular's filters. I checked the Angular documentation to find that `number:2` would do the trick and verified in a jsfiddle that with the curly brace templating syntax, `{{ tip_amount | number:2 }}` resulted in the expected "5.70". I drafted a brief email to the Drizly support team detailing the bug, a screenshot, and my fix, sandwiched with some complimentary "great service and slick site!" language. 

Surprisingly (this was on a Sunday), I got a message back within a few minutes thanking me for the feedback and included was a coupon code for free delivery on my next order. My first reaction to the support response was "Golly! Wasn't that swell that they gave me a coupon!" ([here's some Twitter evidence](https://twitter.com/stelly_ryan/status/650782128767012865)). Thinking further though, I realized what an opportunity that this is for high-traffic websites to capitalize on the implicit open-sourcing of front-end code. As applications move towards SPAs and client side frameworks, more source is making it to the end user.

I don't want to sound like I'm demanding that services pay all developers who voluntarily spend their time to work on your product. I'm rather saying: developers tend to have an achievement mentality. If you can offer a marginal reward to the relative great value of diverse front-end developers for finding and fixing bugs in the user-facing parts of your application, make it as easy as possible for them to do so. 

I love how some websites put job postings in their page source and even in their [http headers](https://www.maxcdn.com/blog/recruiting-humans-http-headers/). Wouldn't it be cool to have a gamified API in the dev tools console? Imagine I was going through Drizly and after I figured out the bug I could F12 and do something like the following:

    cheevo.report(
    	"bad currency formatting on tip field", 
    	"The value in the tip field doesn't seem to be formatted for currency. It looks like the app is using Angular, so the fix if you're using the curly template syntax might look some thing like `{{tip_amout | number:2}}` Cheers!", 
    	"john.doe@abc.com"
    );

If we find out that people are actually interested in fixing our site, why not help them out? For optimization purposes, most sites serve minified assets which remove whitespace and change variable names to make assets as small as possible. Naturally, these sites have no reason to also serve the unoptimized assets. //blegh