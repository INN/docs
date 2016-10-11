# Notes - INN Chicago Workshop, Tuesday, September 27, 2016

## Attendees

Amanda K - formerly Texas Tribune
Marc P - public media platform
Ryan S - chalkbeat, formerly gannett
Fernando D - Reveal/CIR
Robert W - MotherJones
Jahna B - MotherJones
Julia S - INN
Jonathan S - MinnPost
Jack B - INN
Rebekah M - WhereBy.Us
Lauren F - Wisconsin Center for Investigative Journalism
Kyle E - SND, American City Business Journals
Sue C - INN
Adam S - INN

## Let’s hear from each organization what your tools are, what your staff looks like, what you contract out, what problems you run into, what kind of help you need...

AK - Texas Tribune is about 50 people. Django tech stack for main site. The news apps team uses Django for data-heavy apps and Node.js for static apps. Google ads, Mailchimp, Basecamp…

RS - Are people using Salesforce for fundraising or for sources/audience/bucketing readership/etc?

AK - Oh we use basecamp for that

RS - Chalkbeat is a network of local news sites that focus on issues of equity in education. Very mission driven. We’re in 4 cities (NY, Denver, Memphis, Indianapolis, almost have funding for Detroit). Nearly 4 people on the product team. Hired a fulltime dev in April so we cut back on agencies. Merged 4 sites into 1. Wordpress stack, GA, mailchimp, Salesforce, DFP. Presspoint/PauPress for editorial CRM previously, trying to figure out what to do now. We want to be able to customize email newsletters better (this story would be good for this list, push a button and go).

FD - Wordpress. News apps team uses Django. AWS for longterm storage of master podcast assets and for hosting apps. 90% in google docs, to Wordpress. It’s not a great workflow, and it’s not automated. Just got everyone on encrypted email. Mailchimp for newsletters. Salesforce belongs to development department, which uses it for donor tracking. Radian6. Can Salesforce replace mailchimp? Instead of 3 tools, could we have 1? Can editorial use it instead of just development? Our content is a product - shouldn’t we be architecting our user story around conversion instead of just publishing? Can Salesforce help with that? Pardeau for user flow management. We don’t do ads. HootSuite for social management. Can we use Salesforce instead, again? Contextly and Parse.ly. We have our own meme generator that we host. Our podcast workflow is in a radio production system called Shotgun. Impact Tracker is in Drupal. GA, using Google AdWords, but we don’t spend on Google for Display. Managed hosting with Pantheon. Podio for project management.

RW - Drupal6 but moving to Wordpress. Hosted by Auckly, uses Acemi CDN for Drupal. AdTech/ONE by AOL (adserver). Youtube for Videos. GA and chartbeat. Print subscriptions are all entwined with other customers. Looking to see what we can bring into Salesforce. What version of a membership model works for us? Different departments are using SF for different things, relying on consultants for that. Mirapost for email

JB - Mirapost. Looking at better workflow tools. Desk-Net. Currently using Google Docs. Also looking for project management solutions. What are other people using?

JS - Drupal 6 to Wordpress migration. Salesforce. Mailchimp with SF integration (new subscribers are automatically added to SF). Realtime Ads. Data apps (python, node, ajax) dumped into Drupal. Managed hosting with BlackMesh (both WP and Drupal). Image management is difficult. Fastly CDN. GA.

RW - folks from Wired love Fast.ly

RS - Cloudflare is saving our butts

AK - Fastly charged for HTTPS, so we stopped using them

RM - Wordpress. Managed hosting on WPEngine. Mailchimp to send newsletters. SF for client and sales work. Adding editorial stuff next. Editorial team builds everything they write in Google Docs and janky plugins to integrate with WP. Stripe for payments. Trello for project management, split up by team. Don’t do ad serving in traditional way. We sell sponsored spaces attached to specific pieces of content. We have a story formats UI thing to help avoid iframe problems. How do I give them things so they don’t have to talk to me? We make small revenue on promotional placements in the newsletter (a rails app to handle that). Sales proposal generation app. We do most of our work through agency work, and then it tracks if we delivered to that client on time, etc. Text signup apps. Early experiments on middleware to track user flows through multiple touchpoints (events, social, etc). Hootsuite switch to Sprout. 

LF - WP Largo, Presspoint, Google drive/apps, tableau and carto, neon crm but migrating to SF and Stripe. Buffer, TweetDeck, Mailchimp, Slack, Meltwater, Wisconsin news tracker as clipping service. Podio and CIR Impact Tracker. GA, testing super metrics in google drive. 

AS - Wordpress, building and maintaining Largo framework. Experimented with Presspoint, We’ve run into some normal issues with that - the user management piece is a mess. Looking at SF as our CRM. Stripe and Gravity Forms → Stripe → Mailchimp workflow. Wrote plugins for link curation and newsletter creation. DFP and WP ad placement, ad targeting, etc. We use slack and Asana, FreshDesk, and Harvest. We use GitHub a bunch. Buffer for social. WPEngine for managed hosting for now. We’ve had scaling issues with them. Some BitBucket. We used Atlassian for a long time but just moved off of it. 

Jack - GitHub? We all use it. 

[Some discussion about trying to write in GitHub and how it’s bad.]

RS - we do so much collaborating and editing in Google Docs.

AS - Workflow, collaborative editing is a problem everywhere. There’s early-stage experiments about how to do collaborative editing in WP. There’s definitely more we can talk about there. 

JB - Also how to integrate print workflow with online workflow and the collaboration there.

------

ADAM - What do you have sitting on a shelf or open sourced already that may be applicable or useful for other organizations, now that you’ve heard what other people are using. I’m interested in just capturing what everyone else in the room might not know about that you’ve got.

AK - We really don’t have a lot. We’re not trying to solve anyone else’s problems. It’s Texas-focused. Not open sourced, in part because we include passwords and keys because it’s saves time and money for our team. 

AS - What are the obstacles? Just time and money and resources? What would it take to, say, take one state’s work and make it applicable for everyone else?

AK - I think it would depend. 

SC - That’s true for data apps, not necessary for internal tools

AK - We build stuff in Django, I’m not sure how applicable that would be for anyone not on Django. We do build some microservices, and those might be more applicable.

RS - We’re open sourcing our Impact Tracker. We’ve used it for a couple years and now that we have a full-time dev on staff, we can strip out all the broken API integrations and custom stuff for our CMS and now we’ve made it into a plugin and it’ll be available on GitHub soon. We’re behind CIR’s obviously, but...

FD - It’s an arms race for impact trackers

RS - the CMS is on wordpress and the impact tracker is built in drupal? How’s that going for you? 

FD - about as good as you’d expect. I proposed building it as a plugin, but that project was funded by one group, and digital is funded by another one, so there’s fences there. 

RS - Our impact taxonomy is directly sourced from CIR

SC - Do you have any funding to maintain the open source software you build?

RS - I don’t think there’s anything right now that’s directly for this project [MORI]. I know we’ve been talking with Knight, but I don’t know where we are right now.

SC - I know there’s a lot of funding for things to get built, but not after. It’s not a good way to go about these open source projects.

RS - That’s part of the reason why we stripped it down to the bare minimum. This is just an impact tracker plugin for wordpress. No bells and whistles. And then we’ll see how much interest we generate from there.

FD - Impact Tracker. The documentation isn’t there yet though. How does someone actually implement it? That’s definitely something that CIR is very interested in continuing to promote. If I was to come back home and say there are a ton of people interested in optimizing it and developing it further...I think that would be the impetus for us to keep developing it. … I hate vendors, generally. You pay by the hour. There’s usually a 20% tax on communication. There’s 20% on bug squashing. You’re only going to get maybe 60% value. And we build things without foresight. We just get them to build the things we need now without looking about how it’s more broadly applicable or could be open sourced. We want to move to a creative commons and have everybody republish our stuff. We’re trying to do that around our main investigations but later for the rest of our content. We had Alley build us an export button, but if there had been a plugin, we would’ve used it. How do I have the conversation with Alley to say we want to turn it into a plugin for broader use?

AS - How is it actually structured? As a plugin or is it built into the theme?

FD - Not sure. We also have an app template, but I’m not sure how usable that is for other organizations.

Julia - The app template is actually pretty good for a broader user base.

FD - We’re trying to do more with our analytics. There’s no baseline - like GA for news publishers.

AS - It’d be good to have more back and forth about what people are actually doing.

RM - Now lots of our stuff is through FB video, etc. We’re working on a little dashboard-y thing for analytics.

AK - We need something like that. Parsley does some of that, but…We thought about Sprout but it’s really expensive

LF - Google SuperMetrics does some of that. 

(Some conversation about FB videos, more analytics, etc.)

RW - We don’t have a lot that’s out there. We had a small project that our interactives team built and threw some stuff up on GitHub but they ultimately decided not to go in that direction. We had one for a quiz, one for a choose your own adventure thing. There were issues with pulling data from Google, when the API changes, and then trying to paste javascript, etc into your CMS and getting that to work consistently and long-term. Once we get into wordpress, we’d love to collaborate on analytics, homepage layout enhancements...

JB - I think analytics dashboards would be a really fruitful collaboration.

RM - I’m also worried about the “one dashboard to rule them all” concept.

SC - Is benchmarking important to you or not? Is there a set of core analytics that would be helpful to know across the whole field?

RM - I want every reporter to feel responsible for their metrics. They need a more granular level of data than I do as their editor. 

AS - There are different sets of data. Competitive metrics, or is it more internally focused.

FD - Benchmark is not the most appropriate term, maybe baseline is better. If there’s a baseline that says, “audience, uniques, pageviews, by author, by topic” there are certain areas where, performance-wise, we’re on the same level. And then it gets trickier with conversion

AK - We have different interdepartmental needs. We have a most-read widget that broke, and suddenly we realized that the reporters really do care.

RM - Pageviews matter less than time-on-site. Site recirculation is what’s important to me. They’re glued to Chartbeat all day, but getting them to look at it in aggregate is a different story.

AK - What is engagement? How are we defining it? Each organization might have a different focus.

RS - We tried some Slack integration to show reporters their metrics without pulling them out of their own workflow.

RM - I wonder if you could set that up with Zapier. I use the crap out of Zapier. 

AK - It’s how you deal with APIs if you don’t do coding. I love it.

RM - If you’re doing little API integrations, it’s perfect for that. We can set up a series of slackbots just to see if they’re useful before we invest real time into it. 

JS - We have lots of random data projects that we’ve done over the years that are on GitHub. I’ve heard talk that our mailchimp connector will be packaged, but no word on that. I’m writing a whole bunch of SQL to migrate from Drupal to Wordpress - I can give people access to that. I’m writing a thing to connect SF to WP, object-to-object. It’s probably 80% ready for someone else to test it. I’d love to give that away. It’s already open source but no one has used it but me. 

AS - There’s a lot of opportunity there.

JS - I don’t know how realistic it is that we’ll get funding for it, but it is almost ready for an alpha. We have a bunch of little analytics tracking things - most of them all drupal-integrated and jquery. We have one that tracks conversion rates - the funnel. I don’t know if it works. I think it does. We have this other thing that tracks how far users scroll. We have a thing that tracks how often no one clicks on our popups so we can stop using them. We have an ad-blocker tracker. And a sidebar click tracker. A thing that tracks the share buttons and forward this buttons. And we have a python app that Texas built that connects Stripe and SF. It requires Heroku and SSL and everything...but it works. My guess is that it’ll get folded into WP at some point. 

RS - We need a little scroll-depth widget.

FD - That’s the one thing we used Contextly for.

RM - Maybe that’s what we all need a plugin for. Just a jquery plugin that sends over click tracking, scroll depth, author, terms, etc.

RW - We tried something like that but had a lot of trouble with naming conventions based on the elements on the page.

RS - Our event tracking system at Gannett that required a lot of institutional knowledge

RM - I’m hesitant right now to open things up. We’re building things for our purposes and not thinking much broader. We’re building things for UI and homepage management that maybe could be more broadly applicable. Same thing with story format stuff. Like how to make audio files nicer for users. I think that stuff could be possible to open up. It’s all done through metadata, and it would also still have to be styled on everyone’s end, but if that’d be useful to people I could definitely try to share some of that. We’re doing weird guide products. How do we relate posts to each other. Aggregation formats. We made this thing that uses OG data and different topic verticals like the Marshall Project’s “what the reporters are reading” thing.

AK - There is one thing that you might be interested in. It’s Code Grabber that lets people build the HTML for their stories before putting it into the CMS. Because our CMS is so terrible and people didn’t have the ability to put in images to without it being terrible for them, we built this thing that writes the code for them for images, embeds, etc. You have to host it yourself, but it is opensource. 

LF - We don’t have any coders, so I’m always happy to share the work that I’ve done on our tracker. I need help getting traffic tags set up because I’m still having trouble estimating audience size and things like that. We’re not a destination site, but we want a way to see how broad an audience our story reaches.

RM - Like a pixel tracker.

RW - Propublica had something like that but it was really hard to get running. Pixel Painter. [AK agrees]

FD - I’ve been talking to Ted Han about it because we want to do that too. That’s how DocumentCloud tracks all their docs on every website they’re posted on. It’s so much lighter than a custom GA code. We’re having active conversation about it, so if you’re interested too then we’ll add you to the list.

RS - [Story about itjohn.com’s pixel and difficulty getting legit orgs to put the tracker on their site.]

SC - If there is a unified approach, it’s going to help a hell of a lot. “We are making this content available to your readers and this is why we need you to use it.”

FD - Use the logo as the tracker instead of a pixel.

SC - That’s so much better for branding too. It’s not going to be a perfect measure even if it’s uniform

RM - We should try to standardize it too. That would be huge for small publishers.

JB - Does the pixel work on FB instant and AMP? You have to strip out so much to get things to work on that. If a ping that works on mobile web, but that’s not how people are reading our stuff now.

RW - I’m sure if it was an image, FB would strip that out and into their system.

----

## Analytics

Internal: org tracking (big pic/granular)
External: partners and re-tracking
- Reporter custom dashboards
- Parallels
- Super in-depth
- Biz, social, co. roles
Data on groups of content
- Member only
- Section pages
- Tags, categories, metadata
- How do you break down topically
- Naming things
- Ecommerce tracking
External
- AMP, apple news, FB instant article
- Metadata
- How users interact/scroll depth
- Naming things
- Click trackers
- Individual user interactions and personalization
- Ethics
- “Super fans”
- definitions/segmentation/aggregate
- Convert (readers) to (shares) to (subs) to (podcast) listeners to (donors)
- Article page
- Beyond pageviews
- How do we measure reach in a distributed world?
- Goals/financial value of conversion
Funnels
- Social, Parse.ly, GA, EventBrite
- Dashboards only so far
- Data analytics (the more you know, the harder it is to understand the value)

Republication
- Comscore
- Manually enter pickups
- Newspaper association
C- alculate estimated audience/reach

------

FD - Could INN host an ACLS fellow?

----

#### How might we use analytics to develop a better understanding of our superfans and use those insights to develop the business? (funnels)
Skimmbassador program is simple, cool and effective.
How well are people tracking user acquisition costs?


#### How might we use analytics to provide different stakeholder groups relevant and strategic actionable insights?

A/B Testing:
- Less helpful than watching users do something
- If your sample size isn’t large enough if hard to draw a clear conclusion
- It’s hard to design a good A/B test
- NPR had some success with A/B tests when they tested funnels/workflows rather than small UI changes

A need for a tool with better custom dashboards. Is there an add-on that can make reports better/more custom for different types of users?
If I’m a reporter, I want to know how well my story did, but I also want to know who the influences were who helped drive traffic back to our site (by tweeting, writing follow-up, sharing on fb, etc)?
Establishing a best practice baseline
Unique users, time on site, page views…
Stats aren’t concrete - we have a lot of unquestioned assumptions in our business

Stakeholder Groups:
- Editorial Users
- Business
- Grant Writers (pageviews, impact)
- Advertisers (pageviews)
- Membership Departments (engagement)

Can we make a report that defines engaged vs unengaged readers? Does that correspond to donations? 

Strategic actionable insight is an event or initiative that satisfies a goal that established by a stakeholder. So your stakeholder group needs to define their goals and evaluate/verify that the goals they’ve defined are even good goals to have.

There are a lot of assumptions that we make about analytics - it’s important to clearly define the stakeholder groups and then clearly define their goals.

Develop a tool that can more easily create a custom dashboard

Baseline Metrics:
Pageviews, uniques, time on site, desktop vs mobile, social buttons, donation funnel, scroll depth

User testing

#### How might we effectively measure reach in a distributed world?

Is there a way to just have basic metrics like fb or twitter in one place?
Can you just scrape your server logs for your tracking pixel/logo?

----

## CRM Discussion

How might we de-anonymize our users? (Or should we…)
How might we protect the data we’re collecting?
How might we learn more about what makes a good membership program? What incentives work and which ones don’t?
How might we automate outreach to users interested in a particular topic?
How might we keep data in our CRM clean and up to date? Could we develop the expertise ourselves? (Salesforce consultant for news specifically)
How might we improve documentation and knowledge-sharing of CRM insights and best practices among INN members?
How might we better connect our other services into our CRM?

How might we automate outreach to users interested in a particular topic?
Answer: Don’t. Alternatively: Use FB ads.

### ON PLATFORM:
How do we get them into salesforce? 
- Opt into topical subscription via button or other action item (make specialized lists)

What are all the ways we can determine topical interest?
- Shares, click throughs, newsletter, events
- Have a taxonomy around topics that you can use to tag different content types as a certain topic. Also need a counter.

How narrow are we trying to target?
- Politics vs Conservative/Liberal or vs a particular campaign

### OFF PLATFORM
Do we buy data on members?
- FB segmentation via oauth login
- Twitter data

Funnel that data into SF
Segment data based on your custom taxonomy
At time of publication, grab segment from SF and then email/text/etc

#### Questions:
- When do we record a term? What’s the trigger?
- How do we segment?
- Do we weigh users?
- Do you even need SF for this? Can/should you do it with MailChimp alone?

-----

### Next Steps
Slack channels
Calls
Needs for next Largo
