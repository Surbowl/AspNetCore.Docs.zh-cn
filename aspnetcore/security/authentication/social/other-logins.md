---
title: 外部 OAuth 身份验证提供程序
author: rick-anderson
description: 发现适用于 ASP.NET Core 应用的外部 OAuth 身份验证提供程序。
ms.author: riande
ms.custom: mvc
ms.date: 11/11/2018
no-loc:
- ASP.NET Core Identity
- cookie
- Cookie
- Blazor
- Blazor Server
- Blazor WebAssembly
- Identity
- Let's Encrypt
- Razor
- SignalR
uid: security/authentication/otherlogins
ms.openlocfilehash: f410f9ade34c3ffb19dc9f6e5409f44d0a6e5d32
ms.sourcegitcommit: 65add17f74a29a647d812b04517e46cbc78258f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88634236"
---
# <a name="external-oauth-authentication-providers"></a>外部 OAuth 身份验证提供程序

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Pranav Rastogi 撰写](https://github.com/rustd)和 [Valeriy Novytskyy](https://github.com/01binary)

下面的列表包含与 ASP.NET Core 应用一起使用的常见外部 OAuth 身份验证提供程序。 第三方 NuGet 包（如由 [contrib](https://www.nuget.org/packages?q=owners%3Aaspnet-contrib+title%3AOAuth)维护的包）可用于对由 ASP.NET Core 团队实现的身份验证提供程序进行补充。

* [LinkedIn](https://www.linkedin.com/developer/apps) ([说明](https://developer.linkedin.com/docs/oauth2)) 

* [Instagram](https://www.instagram.com/developer/register/) ([说明](https://www.instagram.com/developer/authentication/)) 

* [Reddit](https://www.reddit.com/login?dest=https%3A%2F%2Fwww.reddit.com%2Fprefs%2Fapps) ([说明](https://github.com/reddit/reddit/wiki/OAuth2-Quick-Start-Example)) 

* [Github](https://github.com/login?return_to=https%3A%2F%2Fgithub.com%2Fsettings%2Fapplications%2Fnew) ([说明](https://developer.github.com/v3/oauth/)) 

* [Yahoo](https://login.yahoo.com/config/login?src=devnet&.done=http%3A%2F%2Fdeveloper.yahoo.com%2Fapps%2Fcreate%2F) ([说明](https://developer.yahoo.com/bbauth/user.html)) 

* [Tumblr](https://www.tumblr.com/oauth/apps) ([说明](https://www.tumblr.com/docs/api/v2#auth)) 

* [Pinterest](https://www.pinterest.com/login/?next=http%3A%2F%2Fdevsite%2Fapps%2F) ([说明](https://developers.pinterest.com/docs/api/overview/?)) 

* [袖珍](https://getpocket.com/developer/apps/new) ([说明](https://getpocket.com/developer/docs/authentication)) 

* [Flickr](https://www.flickr.com/services/apps/create) ([说明](https://www.flickr.com/services/api/auth.oauth.html)) 

* [Dribble](https://dribbble.com/signup) ([说明](https://developer.dribbble.com/v1/oauth/)) 

* [Vimeo](https://vimeo.com/join) ([说明](https://developer.vimeo.com/api/authentication)) 

* [SoundCloud](https://soundcloud.com/you/apps/new) ([说明](https://developers.soundcloud.com/blog/we-love-oauth-2)) 

* [VK](https://vk.com/apps?act=manage) ([说明](https://vk.com/pages?oid=-17680044&p=Authorizing_Sites)) 

[!INCLUDE[Multiple authentication providers](includes/chain-auth-providers.md)]

[!INCLUDE[Forward request information when behind a proxy or load balancer section](includes/forwarded-headers-middleware.md)]
