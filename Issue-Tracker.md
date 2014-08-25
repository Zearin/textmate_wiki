# Issue Tracker

**As of this writing, the Issue Tracker is not public, see <http://macromates.com/support> for how to get support or report issues.**

## Bug Reports

The issue tracker at GitHub is for tracking bugs. If you wish to report a bug, please first read [how we want bug reports written](http://kb.textmate.org/writing_bug_reports).

### Questions, Comments, and Troubleshooting

Use one of the following:

- [the TextMate mailing list][]
- [#textmate][] IRC channel on [freenode.net][]
- [contact MacroMates](http://macromates.com/contact) directly

You can also use any of these for bug reports. 

If you’re not sure if something is really a bug, or how to reproduce it, or if it’s already known, etc., please use one of the above channels (instead of the issue tracker).

### The Issue Tracker

The Issue Tracker has some overhead (for the development team, presently just one person) that the above channels do not. 

With the issue tracker, something as simple as replying to a known issue with _“yeah, we know about that, thanks!”_ becomes surprisingly complex. It requires into visiting the issue in a web browser, assigning it a label, doing a search on [GitHub Issues][] (which is nothing like Google’s) to mark references to the old issue(s), and finally closing the new one. 

Perhaps it doesn’t sound like much, but after about a thousand issues in half a year, it does feel like an unnecessary distraction. It’s also something that is difficult to outsource, as Pull Requests also come in via the Issue Tracker. Further complicating the matter is that we reference Issue numbers for bugfix commits.

## Other Issues

To keep the Issue Tracker useful, we generally close issues which are not bug reports. We may not always comment, but generally a label should be assigned. 

Here’s an explanation of some of the typical labels used to close issues:

* `feedback`: The issue created is considered “general feedback”. While you may have made a specific request, the issue may still be closed, as using the issue tracker as a list of everything everyone ever requested (that has not yet been implemented) is just making the issue tracker less useful for its main purpose: tracking bugs.

* `bundle-issue`: The issue isn’t related to the core application, but instead to some bundle item. We’ll often add a comment pointing to the relevant bundle, though. (Each bundle has its own issue tracker.)

* `too-vague`: The issue created is too vague. Please see [writing bug reports](http://kb.textmate.org/writing_bug_reports).

* `question`: You should have used the mailing list, IRC channel, or contacted MacroMates.

* `won’t fix`: There are a bunch of reasons why even actual bugs won’t be fixed. It’s generally better to close an issue with this label (if we don’t plan to address it), than to keep it open for all of eternity.

Also, please remember that while TextMate is developed in a fairly open way, the program’s evolution is **not** dictated by users (via the issues they open).

[the TextMate mailing list]: http://lists.macromates.com/listinfo/textmate
[freenode.net]:              http://freenode.net
[#textmate]:                 irc://irc.freenode.net/#textmate
[GitHub Issues]:             https://github.com/textmate/textmate/issues/
