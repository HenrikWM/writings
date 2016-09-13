There's no getting around the fact that handling identity in web apps can be challenging. New services and frameworks emerge at a fast pace, giving customers hard choices to make about platform strategies while developers inherit implementation challenges based on these choices. Choosing an **IaaS** (Identity as a Service) provider or even building your own identity platform, based on the open authentication and authorization standards **OpenID Connect** and **Oauth2.0**, are two options to consider when choosing an identity strategy for your web apps in today's enterprise segment.

This year we saw some promising new services and frameworks which applies to both of these options. 

* **Microsoft** released **Azure AD B2C** - building on the existing **Azure AD** (Active Directory) platform
* **IdentityServer**, a popular **Microsoft**-endorsed **ASP.NET** implementation of **OpenID Connect** and **OAuth2.0**, now support **Microsoft's** new open-source web framework **ASP.NET Core 1.0**.
 
**Microsoft** used to recommend **IdentityServer** for those looking at an identity platform based on **ASP.NET**. Now that they built their equivalent in **Azure**, there's a new exciting **IaaS** option to choose from. 

**IdentityServer's** port to **ASP.NET Core 1.0** is a big step into the future for **ASP.NET** web apps. As it matures it will be a natural place to start for those looking to build their identity platform based on **IdentityServer**. 

## Introducing Microsoft Azure Active Directory Business-to-Consumer

[![BUILD 2016 - Microsoft Identity](https://raw.githubusercontent.com/HenrikWM/writings/bc68a2ab65d6c3ef60fed7dec3d0eed24a7ef678/identity%20in%20web%20apps%20in%202016%20and%20looking%20ahead/images/IMG_1159_t.jpg "BUILD 2016 - Microsoft Identity")][BUILD-MicrosoftIdentity]

At BUILD this year I saw Microsoft talk about the current [state of Microsoft Identity][BUILD-MicrosoftIdentityVideo] and [Azure AD B2C][BUILD-AzureADB2CVideo]. Later in July, Microsoft [announced][AzureADGA] that **Azure AD B2C** is already Generally Available in the North America region. This is great news and meets a need I see in the B2C identity space for both **Azure** and on-premise web apps. Let me explain why.

**Azure AD**, has already been around for a few years and has served well as the identity provider for company employees, i.e. internal users. This enabled employees to log in and use company services such as **Office365** and internal websites.

### Why did we miss B2C?

But there was really no good story for a company's customers, the Business-to-Consumer (B2C) users. Lets say a company has an extranet or an e-commerce website. Do the users of these websites belong in **Azure AD** along with internal employee users? Ideally not. For many reasons; spam-accounts and increased attack surface on a central business-critical service to name a few. So until now what you would have to do is to put these external users in separate databases with a membership-framework for the B2C-website sitting on top. Now, you're probably doing authentication and authorization on these websites as well, duplicating the responsibilities that you're already paying **Azure AD** to do for your internal users and services!

### What do we get from B2C?

[![BUILD 2016 - Azure AD B2C](https://raw.githubusercontent.com/HenrikWM/writings/bc68a2ab65d6c3ef60fed7dec3d0eed24a7ef678/identity%20in%20web%20apps%20in%202016%20and%20looking%20ahead/images/IMG_1161_t.jpg "BUILD 2016 - Azure AD B2C")][BUILD-AzureADB2C]

So Microsoft created **Azure AD B2C**. It targets these misplaced and "homeless" external users, giving them a place to exist so that the already existing platform of **Azure AD** can be applied to this user segment as well.

**Azure AD B2C** offers the expected **IaaS** benefits for the B2C-segment, including:

* Built on a well-established authentication platform
* Runs on the same infrastructure as **Azure AD**, which means scalability, security & auditing, support, standards-compliance and more are already in place.
* Use local accounts, social providers, email verification
* Fully customizable UX (very important for not breaking user context during login!)

### Alternatives to Azure AD B2C

In addition to building your own identity platform, [Auth0] is a great **IaaS** provider that offer many of the same benefits as **Azure AD B2C**, including:

* Set up social identity providers (e.g. Facebook, Google, Microsoft)
* Customize UX
* A rich API
* Based on open standards
* Enterprise level integration with **AD** 

[Auth0] can be used for both external users and internal users, which is convenient for customers looking for a single **IaaS** platform for both user segments.

## IdentityServer on ASP.NET Core 1.0

*Just last week* one of the authors of **IdentityServer**, [Dominick Baier], [announced][IdSrv4RC1] that **IdentityServer4** was **RC1**. This version targets **Microsoft's** new open web framework **ASP.NET Core 1.0**, bringing the popular open-source identity platform to a new framework for cross-platform and cloud-optimized web apps. **IdentityServer4** has been [in development][IdSrv4] for some time already.

### What changes in version 4?

The announcement explains in more technical detail all of the internal architectural changes and benefits from **ASP.NET Core 1.0**. Overall, version 4 is a porting of version 3 with big upgrades in key areas along with several deep architectural re-writes. 

In my opinion, one of the biggest improvements is the increased separation between UI and back-end. This makes it easier and much more efficient to bring in a separate front-end developer to do pure UX work.

The highlights include:

* Customizing UX is easier due to more separation in the architecture
* Integrates well with the built-in middleware for logging, configuration etc. in **ASP.NET Core 1.0** 
* Improved integration with the standard **ASP.NET** identity framework, **ASP.NET Core Identity**
* Extended compliance with the **OpenID Connect** and **OAuth2.0** standards 

### Will MembershipReboot be ported as well?

[Brock Allen], the other author of **IdentityServer**, originally built the **[MembershipReboot]** user management framework out of frustration for lacking functionality in the **ASP.NET Identity** framework. Today, **MembershipReboot** seems to be the go-to user management framework for not only **IdentityServer**, but also any **ASP.NET** web app not using **ASP.NET Identity** and needs user management features such as:

* social identity providers
* email verification
* notification system
* reset/forgot password
* custom user attributes
* multi-tenancy

But looking ahead, the **ASP.NET Core 1.0** ships with the new **[ASP.NET Core Identity]** framework for user management, replacing the old **ASP.NET Identity** framework. [Brock has stated][MembershipRebootOnCore] that this framework will most likely replace **MembershipReboot** for **ASP.NET Core** web apps, because of improvements made to the **ASP.NET Core Identity** framework. Improvements which he himself and Dominick have contributed with, based on lessons learned from **MembershipReboot** and **IdentityServer**.

So no, it doesn't look like **MembershipReboot** will be ported but instead be replaced by **ASP.NET Core Identity**, and customers and developers looking at building **IdentityServer** on **ASP.NET Core** should explore **ASP.NET Core Identity** for user management. 

## Summary

For those who have already built an identity platform because **Azure AD** or other  **IaaS**-providers didn't yet have a good B2C-story, exploring **Azure AD B2C** to get the  mentioned **IaaS**-benefits would be time well spent. If you already are invested in **Microsoft Azure** and have yet to make an identity decision for your web apps, **Azure AD** and the new **Azure AD B2C** are excellent services to explore. As I mentioned, there are also great **IaaS**-alternatives.

On the other hand, for those who are comfortable with building their own identity platform and are taking a close look at where **ASP.NET** is heading, **IdentityServer** is still an industry leader in identity and offers a great open-source alternative.

[BUILD-MicrosoftIdentityVideo]: https://channel9.msdn.com/events/Build/2016/B868
[BUILD-AzureADB2CVideo]: https://channel9.msdn.com/Events/Build/2016/P423
[BUILD-MicrosoftIdentity]: https://raw.githubusercontent.com/HenrikWM/writings/master/identity%20in%20web%20apps%20in%202016%20and%20looking%20ahead/images/IMG_1159.JPG
[BUILD-AzureADB2C]: https://raw.githubusercontent.com/HenrikWM/writings/master/identity%20in%20web%20apps%20in%202016%20and%20looking%20ahead/images/IMG_1161.JPG
[AzureADGA]: https://azure.microsoft.com/en-us/blog/azuread-b2c-ga-announcement/
[Auth0]: https://auth0.com
[Dominick Baier]: https://twitter.com/leastprivilege
[Brock Allen]: https://twitter.com/BrockLAllen
[IdSrv4]: https://leastprivilege.com/2016/01/11/announcing-identityserver-for-asp-net-5-and-net-core/
[MembershipReboot]: https://github.com/brockallen/BrockAllen.MembershipReboot
[MembershipRebootOnCore]: https://github.com/brockallen/BrockAllen.MembershipReboot/issues/568#issuecomment-222208300
[IdSrv4RC1]: https://leastprivilege.com/2016/09/06/identityserver4-rc1/
[ASP.NET Core Identity]: https://docs.asp.net/en/latest/security/authentication/identity.html#introduction-to-identity