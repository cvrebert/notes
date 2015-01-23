## Why Bootstrap?
So, let's start at the beginning. Why start using Bootstrap in the first place? Bootstrap appeals to a few different audiences, but for me as a backend developer, I started using it for internal apps because:
* I would like my app to not look completely plain/barebones, as it would without any CSS (or barely any CSS).
* Since this is an internal app, I don't have any significant branding or exact look-and-feel requirements that I'm required to adhere to.
* I am not an artist/designer and don't have one at my disposal. It would be difficult to come up with a pleasing visual design on my own from scratch.
* CSS can be rather arcane. Outwardly, the common "Holy Grail Layout" looks simple and reasonable, yet there are entire articles on how to achieve it in CSS with varying degrees of kludginess. There are several other examples of simple things requiring unnecessary complexity.
  * (Yes, [flexbox now makes this particular case pretty simple](http://philipwalton.github.io/solved-by-flexbox/demos/holy-grail/) and sane, but [browser support limitations](http://caniuse.com/#feat=flexbox) (and [bugs in some versions of the implementations](https://github.com/philipwalton/flexbugs)) prevent it from being a option for lots of folks.)
* I want to avoid having to directly deal with browser bugs and inconsistencies as much as possible. Bootstrap works around (or at least documents) these so I don't have to.

## Getting involved

How first involved

First somewhat nontrivial commit
```
fixes #5494: style invalid fields as invalid regardless of required-ness
commit 76f9c9128e95f55efee66ade30b7f8a31b34208e
Author: Chris Rebert
Date:   Sun Nov 4 18:26:25 2012 -0800
```
First refactoring commit
```
refactor tables.less to use nesting more
commit da072fff21f565521d3dbe1f5f4f42550ecc989e
Author: Chris Rebert
Date:   Tue Jul 2 11:25:57 2013 -0700
```

### Triage
* [3,326 issues commented on](https://github.com/twbs/bootstrap/issues?q=commenter%3Acvrebert+type%3Aissue+-author%3Acvrebert) (as of 2014-01-16, excludes PRs, excludes issues I opened)
  * Assuming I started triaging with the first refactoring commit on 2013-07-02, that equates to:
    * ~5.9 issues per day
    * approx one issue every 4 hours
    * TL;DR: Bootstrap is crazy popular

  inundated with issues
  maintainers not active enough
  Haunt script horribleness
  debug stuff
  JS Bin is nice

## Sending patches

Simple refactorings to reduce duplication in Less source
The first patches I submitted were simple refactorings to reduce redundancy in the Less source code. Very little Less or CSS knowledge required.
I also started submitting documentation patches to answer FAQs and common pitfalls that were coming up repeatedly on the issue tracker.
Build system, since fat went AFK
Testability
Sauce Labs

## Going meta

By this point, the number of spurious bug reports starts to get to me. They tend to fall into a few general categories:
* Malformed HTML
* Not adhering to the DOM structure prescribed by the docs
* Not including jQuery
* Many duplicate issues
  * Duplicates of issues fixed in `master` and thus closed

And thus I had the germ of the idea for [LMVTFY](https://github.com/cvrebert/lmvtfy) and [Bootlint](https://github.com/twbs/bootlint)
I was (and still mostly am) enfatuated with Scala at the time, so I used this as an excuse to learn and try out Akka and Spray (I mean, the actor model is the future, right?)
Also [the HTML5 validator](https://github.com/validator/validator) is in Java, so a JVM language seems like an easy way to integrate with it.

As for Bootlint, it needed to work on the command line to be able to interact with people on the issue tracker, and having folks be able to use it in the browser is a plus, thus, it's in JavaScript (sigh), although very strictly linted and pretty well unit-tested JS.
Had to dig through a couple layers of Cheerio's dependency stack to get my main feature [outputting the line (and column) number where each mistake is](https://github.com/twbs/bootlint/issues/29)

[Rorschach](https://github.com/twbs/rorschach)
The basic problem is folks who don't understand the project structure and try to make changes directly to the compiled CSS instead of the source Less. Rorschach has seen less action than I'd anticipated, having lived through the pre-v3 era, but I speculate that contributions will ramp up in the pre-v4 era.

For such a large project, the testing was fairly basic. The closest thing to CSS testing is looking through the docs. Mostly relied on hordes of users manually testing by finding issues in their own apps.

[Savage](https://github.com/twbs/savage)
  the Sauce/Travis bug
  Sauce claimed to be working on it a while ago, but there have been no public updates since then.

Most recently, I wrote [Gruntworker](https://github.com/twbs/gruntworker/), a simple script to keep our dist files up to date (if we're gonna have generated artifacts in the repo, we might as well completely automate the generation and keep it from ever getting too outdated).

Future: No Carrier
Problems of the issue tracker:
* overall, folks expecting responses to posts on long-closed issues that aren't really being monitored anymore. 
* people thinking a long-closed issue is related to a current bug that they're seeing
  * often it's only superficially related
  * if it's a real regression, we'd much rather open a new bug to specifically track a regression anyway
  * +1's and "thanks" noise

Future: [WebdriverCSS](https://github.com/webdriverio/webdrivercss-adminpanel) or Gemini

customer service, jaded, soul-sucking
