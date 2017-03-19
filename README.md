# Drizzle paywall
Drizzle paywall is simple scalable and most user-friendly paywall, subscription and membership product. It's built using React, JS, Meteor, Node, MongoDB. It's compatible with any web technology and stack. Implemented natively, not via external JS file. It takes about 30 min to set up and deploy product, and only 5 min to install it on any type of website. If you are on Wordpress or Drupal, you are in luck, contact Kelly (kelly@getdrizzle.com) and we can provide WP plugin or Drupal module to make installation even smoother (via API key). This product is built mainly by @klyburke, @delgermurun and me with contributions from @lnmunhoz. 

#### Live example: https://coachesonly.breakingmuscle.com/business-development/how-to-stay-ahead-of-changes-in-personal-training

License: General Public License v3.0. We also offer commercial license in case you don't want to publish and distribute your content. Product under commercial license includes extra features, which are needed for particular types of online publishers, for example metered paywall.

# It's built for:
- any size online publisher with premium online content who believes that advertising revenue should be supplemented with direct revenue;
- any startup which sells premium content or digital product (example, videos) or premium features;
- any website owner who has premium, valuable, unique content and wants to sell it via membership and subscriptions.

# Why this product exists?
If you know why this product exists, go read about how you can get more paying users by using this product: https://medium.com/@getdrizzle/how-to-get-more-subscribers-with-a-user-friendly-paywall-part-i-83887372547d#.y1ifi09us

If you are not sure why this product exists, read:
- Why Medium ditched ad-based business model and launches subscriptions: https://medium.com/@getdrizzle/subscriptions-on-medium-f23de6677464#.92s0vj4xa

- Why online ad revenue is declining: https://medium.com/@getdrizzle/big-shifts-in-online-content-monetization-bdebd920bf4b#.oyjvxcqif

- Why it is so hard for ad-supported business to pivot: 
https://medium.com/@getdrizzle/challenges-for-content-monetization-7a1b813ba19d#.wr3ousv2o

# Features
### Open-source license (this repo)
- User-frienly paywall. Login in 2 clicks, pay in 2 more clicks. Screenshots: https://medium.com/@getdrizzle/how-to-get-more-subscribers-with-a-user-friendly-paywall-part-i-83887372547d#.g0sx8k3km
- Paywalled data is hidden via server-side method, not client-side.
- Paywall is server-side rendered.
- Mobile-optimized paywall.
- Content performance. Detailed analytics for every web page with paywalled content:
![screen shot 2017-03-18 at 11 39 01 am](https://cloud.githubusercontent.com/assets/10218864/24074929/93ad21de-0bcf-11e7-98a8-c9e01b9ccd98.png)
- Membership. Detailed analytics for every user, user are segmented into groups, similar sales funnel:
![screen shot 2017-03-18 at 11 40 12 am](https://cloud.githubusercontent.com/assets/10218864/24074944/af9c9348-0bcf-11e7-8969-c59ac1a39b3d.png)
- Payments and Payouts analytics.
- One-click refunds.
- Stripe integration.
- Customizable UI.
- Social proof.
- Curated lists: Newest, Popular lists.
- Footer bar and in-site links.
- Mailgun and Mailchimp integration.
- Welcome email and email notifications.
- Set up single payments.
- Set up subscriptions.
- Set up Free Trial for subscriptions.
- Ability to create single sign-on system accross multiple websites.
- Set up on Wordpress or Drupal site via plugin or module (via API key).

### Commercial license
- Paywall videos
- Metered paywall
- Lead generation (ask for verified email instead of payment)
- Daily pass
- Curated lists: Trending, Similar.
- Referral feature
- Discount code for subscriptions
- Annual and Weekly subscriptions
- Section-specific subscriptions
- Export users data

# Setup of Publishers app (./publishers)
In my local build, I use node v5.7.0 and npm 3.8.2 inside all apps.
To set node version:

```
. ~/.nvm/nvm.sh
nvm use 5.7.0
```

Publishers app is publisher's dashboard app, this is where publisher or website owner sets up subscription plan, monitors content performance and user payments. 

In main folder, run:

```
npm install
```

In ./publishers folder, run:

```
meteor npm install
meteor npm install --save bcrypt
```

Create local-settings.json file, example:

```
{
    "AWSAccessKeyId": "AKIAIVxxxxxxxxxxxxxxxxxxxxxxx",
    "AWSSecretAccessKey": "+BaPedgw1uyb0Exxxxxxxxxxxxxxxxxxxxxxx",
    "S3bucket": "zenmarket",
    "embedlyKey": "e40b9936xxxxxxxxxxxxxxxxxxxxxxx",
    "private": {
    },
    "public": {
    }
}
```
Publishers app can be started locally by:

```
./start-local.sh
```
Publishers app is using remote demo MongoDB. Feel free to specify local or remote MONGO_URL in the start-local.sh file.
Example of deployed Publishers app can be found here: https://app.getdrizzle.com/

When you start app for the first time, DB will be seeded by a few documents: Admin user will be created (**users** collection), website (**products** collection) and paywalled page (**payg_content_walls** collection).

App will be running at `http://localhost:8021/` To find email and password of your Admin user, go to:
`./publishers/imports/startup/server/seeds.js`

You will log in and revisit http://localhost:8021/setup page after we are done with setting up Users apps.

# Setup of Users apps (./users/..)

Remember set up right node version, or later on gulp won't run.

In ./users folder, run:

```
./setup.sh
```

After it's done, make sure that ./users/widgetFile contains settings.json file:
```
{
  "API_URL": "http://localhost:8051"
}
```

In ./users/widget folder, create local-settings.json:
```
{
  "PUBLISHER_ROOT_URL": "http://localhost:8021"
}
```
And run:

```
meteor npm install --save bcrypt
```

To start 2 Users apps (Widget app at http://localhost:8051 and static Publisher app at http://localhost:8060), run 

```
./start-local.sh
```
inside ./users folder. This will also run gulpfile.js, so widget.js file at ./users/widgetFile/src/widget.js and ./publishers/private/widget.js is updated without app restart.

Static Publisher app at http://localhost:8060 is a static website with paywalled content on the homepage.

# Setup of paywall on local website (./users/publisher)

Go to http://localhost:8021/login, log in with your Admin user. Go to http://localhost:8021/setup page. Copy setup code, and paste it at the bottom of ./users/publisher/index.html.

Navigate to http://localhost:8060, you should see: 

![screen shot 2017-03-18 at 6 36 32 pm](https://cloud.githubusercontent.com/assets/10218864/24077416/e6bb4de4-0c09-11e7-8793-0282af325deb.png)

![screen shot 2017-03-18 at 6 36 46 pm](https://cloud.githubusercontent.com/assets/10218864/24077420/ec05130c-0c09-11e7-83b1-c3fa9e082936.png)

To see blue footer bar with call-to-action, go to http://localhost:8021/wall-settings and **Enable call to action footer bar**.

# Deploy
You will need to deploy 2 apps: Publishers app ( ./publishers) and Widget app (./users/widget). There is a detailed description for deployment of Meteor apps with mupx tool: https://github.com/tima101/meteor-deploy-letsencrypt

# Future and Contributions
This section will need more work. The next 3 steps for open-source project:
- Improve UI and UX on Publishers app (./publishers).
- Meteor 1.5 to reduce initial bundle size for Widget app (./users/widget).
- Add Apple pay for easier payments on Mobile.


