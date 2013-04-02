# Issue Tracker

## Bug Reports

The issue tracker at GitHub is for tracking bugs. If you wish to report a bug, please first read [how we want bug reports written](http://kb.textmate.org/writing_bug_reports).

For questions, comments, troubleshooting, and similar you can use [the TextMate mailing list][], [#textmate][] IRC channel on [freenode.net][] or [contact MacroMates](http://macromates.com/contact) directly.

Any of the above channels can also be used for bug reports. In fact, if you think something is already known, not sure if it really is a bug, how to reproduce it, or similar, then it’s preferred you use the above channels (instead of the issue tracker).

The issue tracker has some overhead (for the development team, presently consisting of one person) that the above channels do not. With the issue tracker, something as simple as replying _“yeah, we know about that, thanks!”_ is turned into visiting the issue in a web browser to assign it a label, doing a search on [GitHub Issues][] (which is nothing like Google’s) to add a reference to the old issue and then close the new one. Perhaps it doesn’t sound like much, but after about a thousand issues in half a year, it does feel like an unnecessary distraction, one that is difficult to outsource, as pull requests also come in via the issue tracker, plus we do reference issues when doing bug fix commits.

## Other Issues

To keep the issue tracker useful we generally close issues which are not bug reports. We may not always add a comment, but generally a label should be assigned, here’s an explanation of some of the typical labels used to close issues:

* `feedback`: The issue created is considered “general feedback”. While you may have made a specific request, the issue may still be closed, as using the issue tracker as a list of everything everyone ever requested (that has not yet been implemented) is just making the issue tracker less useful for it’s main purpose (tracking bugs).

* `bundle-issue`: The issue created is not related to the core application but instead some bundle item. Often though we will add a comment pointing to the bundle that is related to the issue (each bundle has its own issue tracker).

* `too-vague`: The issue created is too vague. Please see [writing bug reports](http://kb.textmate.org/writing_bug_reports).

* `question`: You should have used the mailing list, IRC channel, or contacted MacroMates.

* `won’t fix`: There are a bunch of reasons why even actual bugs won’t be fixed. It’s generally better to close an issue with this label, if we don’t plan to address it, than to keep it open for all of eternity.

Also, please remember that while TextMate is developed in a fairly open way, how the program evolves is **not** dictated by users (via the issues they open).

[the TextMate mailing list]: http://lists.macromates.com/listinfo/textmate
[freenode.net]:              http://freenode.net/
[#textmate]:                 irc://irc.freenode.net/#textmate
[GitHub Issues]:             https://github.com/textmate/textmate/issues/
