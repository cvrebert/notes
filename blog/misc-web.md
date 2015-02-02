## Not as simple as you thought: the humble `<input type="text">`
* Doing the bare minimum is trivial. Doing it with optimal UX isn't.
* https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input
* `autocapitalize`: `none`/etc. E.g. Stop trying to capitalize my username
* `autocomplete="off"` (if you want to avoid the Firefox persistent disabledness bug)
* I know how my username is spelled, dammit!
  * `autocorrect="off"`
  * `spellcheck="false"`
* `inputmode`
  * `verbatim` for non-prose
  * `numeric` for ID "numbers"
* `autofocus`, on a page-wide basis
* Griping about `:invalid`
* Leading/trailing spaces
* Masking out invalid characters
* Ignoring punctuation

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
