Linking a custom domain to a deployed application is confusing and at times you don't get a route on how to link the domain with the website. 😫 

In this article, I will be explaining how to link a *Custom domain brought in Google Domains service to an application hosted on Vercel*. 

Perks of using vercel is that it allows adding domain without any verification unlike Heroku/Netlify, which means you don't have to add your billing details to add a domain to your application. Moreover, it is fast, efficient, and easy to use.😁

### What is Vercel?

> ​Vercel is a deployment and collaboration platform for frontend developers. ​Vercel enables developers to host websites and web services that deploy instantly and scale automatically – all without any configuration. Source -  [Official Docs](https://vercel.com/docs) 

### What is Google Domain Service?

> Google Domains is a domain name registrar operated by Google. Google Domains offers domain registration, DNS hosting, DNSSEC, Dynamic DNS, domain forwarding, and email forwarding. It also offers a one-click DNS configuration that connects the domains with Blogger, Google Sites, Squarespace, Weebly, and Shopify. Source -  [Wikipedia](https://en.wikipedia.org/wiki/Google_Domains) 

Without wasting much time, let us go deep on how to do it. 🤔

- Firstly, you need to make sure your application is deployed and running well on vercel under the `.vercel.app` domain. Suppose your application name is `xyz` then the domain on which your application currently running would be `xyz.vercel.app`.

- Go to the `Settings` section in your application workspace and then go to `Domains`. Under this section, you would see your domains which are currently linked with the application. You would also find the one mentioned above by default.

- Type the custom domain that you have purchased from `Google domains` to the Input field in the `View Domains` section and add the domain.

- A popup like the one below would appear and you would be asked to choose one of the options. You can choose any of the options among the 3 given ones. *Recommended* one is the first option, so we will choose that as we want our website to work on both `xyz.com` and `www.xyz.com.

![vercel_popup.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1619718995429/oEW54x4cI.png)

- Currently both the domains would show *Invalid configuration* and you need to configure them on the Google Domains Dashboard. So, let us do it.

- Go to Google Domains Dashboard and choose your domain that you have purchased. Under, the domain workspace, go to the `DNS` option on the tab to the left of your screen.

![gd_dns.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1619719184146/xHLqBljzf.png)

- Under the `DNS` section, scroll below and you would get the `Custom resource records` section. 

![gd_cdm.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1619719310167/PxL9Mr1dm.png)

- Now, we will add the `A` record for the domain `xyz.com` and `CNAME` record for the `www.xyz.com` as this has an alias `www` in it.

- Copy the `A record` Value from your vercel domain section where you added your domain and add it to the `Custom resource records`. While adding it, leave the default name the same as `@`, Type as `A`, and TTL as `1h`. Only add the IPv4 address which you copied from the Vercel Domain section. Click on Add.

- Copy the `CNAME record` Value from the vercel domain section where you added your domain and add it to the `Custom resource records`. While adding it, make sure the Name is `www`, Type is `CNAME`, and leave TTL as `1h`. Only add the Domain name value which you copied from the Vercel Domain section. Click on Add.

- Once the above step is configured correctly, wait for some time and you will see `Blue ticks` under your domain configs in the Vercel dashboard. This means that the configuration and linking were successful and the domain would be linked to your application soon. 🎊 This may take time for some of the users because in general, the DNS propagation takes 24-48hrs. ⌚ But in my case, it hardly took 5 minutes. 😄

- You can check whether your URL has propagated with this awesome tool  [DNS Checker](https://dnschecker.org/).

Kudos 👏👏 your domain is configured successfully and is linked to your Vercel app successfully. 

<p align="center">
    <a href="https://www.buymeacoffee.com/khushal87" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 220px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>
</p>

### Follow and support me -
Github 👨‍💻 -  [khushal87](https://github.com/khushal87) 

LinkedIn 👨‍💻 - [Khushal Agarwal](https://www.linkedin.com/in/khushal87/)
