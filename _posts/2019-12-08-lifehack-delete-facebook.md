---
title: 'Lifehack: Delete Facebook'
date: 2019-12-08 02:31 -0600
---

# Lifehack: Delete Facebook

People who know me personally know that I don't have a Facebook account. I used to have one, from 2007 to 2017: from before I started high school to after graduating in college.

The main reason that drove me to delete my Facebook account was that I had read that its use makes us less happy. I don't have the original article, [but you can read a scholarly one here](http://web.stanford.edu/~gentzkow/research/facebook.pdf).

> deactivating Facebook for the four weeks before the 2018 US midterm election [...] increased subjective well-being

I deleted my account after deactivating it for a few months. It was quite a spectacle to delete it, wading through several pages, complete with emotional appeals such as "(user) will miss you" alongside pictures of several of my Facebook friends.

Of course, I have no assurance that they actually deleted my data, but it feels better than having a deactivated account ready to come online anytime. Now I can simply say "I don't have a Facebook". People are less likely to pressure me to use the service than if I were to say "my account is deactivated". Furthermore, if my password were to be exposed in a data breach such as [this one](https://techcrunch.com/2019/04/18/instagram-password-leak-millions/), the attacker still would not be able to harvest my data.

Since then, I have read about [illicit data harvesting](https://en.wikipedia.org/wiki/Facebook%E2%80%93Cambridge_Analytica_data_scandal), [unauthorized camera use](https://www.cnet.com/news/facebook-bug-has-camera-activated-while-people-are-using-the-app/), [questionable terms of use](https://en.wikipedia.org/wiki/Criticism_of_Facebook#Terms_of_use_controversy) and [tax avoidance](https://en.wikipedia.org/wiki/Criticism_of_Facebook#Tax_avoidance). I also take issue with Facebook owning would-be competitors Instagram and WhatsApp. But research showing social media can make people less happy was enough to get me off in the first place, and I'm glad that I did.

## Blocking Facebook domains

By adding known Facebook domains to my `/etc/hosts` with a local address, I prevent web traffic from going to them. Among the benefits are that I am not tracked, I save bandwidth on the requests, and Facebook content like "Like" buttons simply don't appear.

Here's a sample of what that looks like:

```
0.0.0.0 apps.facebook.com
0.0.0.0 connect.facebook.net
0.0.0.0 facebook.com
0.0.0.0 fbcdn.com
```

[Take a look at the entire list and how to install them here](https://github.com/razzius/blocked-hosts#blocked-hosts).

## Gratitude

I'm fortunate my livelihood does not depend on activity on these platforms. I do not depend on Facebook for advertising reach, for example. If I were to release content that would benefit from wide reach, like a book, I'd certainly be missing out on attention by steering clear of Facebook. But for my activities thus far, Facebook is a clear negative tradeoff.

I'm grateful to my friends who continually include me in their events, even though they can't send event invitations to Facebook or messages through Messenger.
