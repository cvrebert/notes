## Why Bootstrap?
So, let's start at the beginning. Why start using Bootstrap in the first place? Bootstrap appeals to a few different audiences, but for me as a backend developer, I started using it for internal apps because:
* I would like my app to not look completely plain/barebones, as it would without any CSS (or barely any CSS).
* Since this is an internal app, I don't have any significant branding or exact look-and-feel requirements that I'm required to adhere to.
* I am not an artist/designer and don't have one at my disposal. It would be difficult to come up with a pleasing visual design on my own from scratch.
* CSS can be rather arcane. Outwardly, the common "Holy Grail Layout" looks simple and reasonable, yet there are entire articles on how to achieve it in CSS with varying degrees of kludginess. There are several other examples of simple things requiring unnecessary complexity.
  * (Yes, [flexbox now makes this particular case pretty simple](http://philipwalton.github.io/solved-by-flexbox/demos/holy-grail/) and sane, but browser support limitations (and [bugs in some versions of the implementations](https://github.com/philipwalton/flexbugs)) prevent it from being a option for lots of folks.)
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

And thus I had the germ of the idea for [LMVTFY](https://github.com/cvrebert/lmvtfy) and [Bootlint](https://github.com/twbs/bootlint)
I was (and still mostly am) enfatuated with Scala at the time, so I used this as an excuse to learn and try out Akka and Spray (I mean, the actor model is the future, right?)
Also [the HTML5 validator](https://github.com/validator/validator) is in Java, so a JVM language seems like an easy way to integrate with it.

[Rorschach](https://github.com/twbs/rorschach)
The basic problem is folks who don't understand the project structure and try to make changes directly to the compiled CSS instead of the source Less. Rorschach has seen less action than I'd anticipated, having lived through the pre-v3 era, but I speculate that contributions will ramp up in the pre-v4 era.

For such a large project, the testing was fairly basic. The closest thing to CSS testing is looking through the docs. Mostly relied on hordes of users manually testing by finding issues in their own apps.

[Savage](https://github.com/twbs/savage)
  the Sauce/Travis bug

Most recently, I wrote [Gruntworker](https://github.com/twbs/gruntworker/), a simple script to keep our dist files up to date (if we're gonna have generated artifacts in the repo, we might as well completely automate the generation and keep it from ever getting too outdated).

Future: No Carrier
Future: [WebdriverCSS](https://github.com/webdriverio/webdrivercss-adminpanel) or Gemini

customer service, jaded, soul-sucking

## Tangent: The Web stack sucks

[all] [these] [browser] [bugs]
[how did this pass QA?]
"leave your sense of logic at the door" indeed
N different vendors
design by committee prog langs in general

### JS sucks
  preface: Python
  `this` craziness
  no integers craziness
  weak typing
  N different module systems
  Wat.

JS tooling ecosystem
  puzzle solving
  perverse incentives
  self-inflicted/artificial problems

### CSS sucks
  no module system
  all the selectors suck
  it's the future, where's my damn "has X child" selector yet
  or perhaps, IE sucks

### HTML sucks
an advanced video game system with an obtuse and either primitive or oversimplified interface
"semantic"
  ARIA kinda sorta
  mdoml
but it's popular
but, Web Components!
  damn overcomplicated

## Tangent: designer hate
  native vs. custom
  they give you the world, and you toss it aside
  you vs. Apple/Microsoft/GoogleAndroid
  folks are familiar with native anyway

## Tangent: The GitHub issue tracker is mediocre
The GitHub issue tracker is very simple and lightweight. Aside from its search and milestone features, and its commit message integration, it's close to a minimal viable bug tracking product. It's missing some a few features that would alleviate a lot of pain for projects that get lots of issues.
* Unlike Bugzilla or Chromium's issue tracker, we can't present a template for the user to fill out when reporting their issue. Thus, issue triagers must waste time posting follow-up comments asking the OP for information that they really ought to have included in the initial post (e.g. What version of the program are you using? What platform are you using? Example that demonstrates the problem (screenshots don't count!)?)
* No explicit tracking of duplicates.
* A "similar issues" prompt when reporting new bugs. Bugzilla has this. This makes the "search for duplicates" step of the bug reporting process easier & mandatory. You will quickly learn that without this, many folks won't bother searching for duplicates, or will neglect to include closed issues in the search (Guess what? Your issue was already reported and has been fixed in `master`! We just haven't rolled a release yet.).
