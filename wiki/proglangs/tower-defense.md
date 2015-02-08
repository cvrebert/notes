> The Tower Defense model is an approach to software reliability that focuses on catching bugs at the lowest level, to avoid the inevitable combinatorial explosion in test coverage surface area. In other words, deal with problems like these at the language level, so there is NO NEED to deal with them at a higher process-level.
>
> No one is disputing that processes, QA or Devops couldn't/shouldn't hypothetically catch these bugs before entering production. The problem of course is that they usually don't, because the lower level defenses are allowing too many bugs through, that they really shouldn't and the higher level processes become overwhelmed, fail, and allow bugs to cross the critical production threshold.
>
> This means always giving higher priority to lower-level methods of reliability. For example,
>
> * Language rules are more important than
> * Unit tests are more important than
> * Integration tests are more important than
> * Code reviews are more important than
> * QA is more important than
> * Monitoring is more important than
> * Bug reports
> 
> -- [eldude](https://news.ycombinator.com/user?id=eldude) in https://news.ycombinator.com/item?id=7599717
