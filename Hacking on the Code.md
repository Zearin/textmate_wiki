Here are some things that shouldn’t require too much knowledge about the code base, as they are fairly isolated:

1.	The syntax for format strings include replacements for variables like this:

		${«variable»/«regexp»/«replacement»/«flags»}

	For example to replace spaces with dashes in the `$TM_FULLNAME` variable we might do:

		${TM_FULLNAME/ /-/g}

	It would be useful to support variables in the regular expression part of the expression. This is for `.tm_properties` where we e.g. can set `windowTitle` to a format string, and would like to set it e.g. to:

		windowTitle = "$TM_DISPLAYNAME — ${TM_FILEPATH/^$TM_PROJECT_DIRECTORY\///}"

	Here we wish to chop off the `$TM_PROJECT_DIRECTORY` path prefix of `$TM_FILEPATH`.

	The support for format strings is in the [regexp][] framework. Look at [parser.cc][] and [format_string.cc][].

2.	New (native) commit window.

	The current commit window is a separate application which is “always on top” and by not using the OakTextView we miss out on all the nice features of the Git commit message grammar like `fix→` for `fixup!`’s and highlights of too long summary lines.

4.	Improvements to the ⌘T window (more decorative, like show file icons with SCM badging, show path to file as “second row” for each file, etc.).

	This is the [OakFilterList][] framework.

6.	Custom data sources for file browser, e.g. Simplenote support or sftp, see [FSDataSource.h][].

7.  There is a pasteboard subclass which maintains a history ([OakPasteboard.h][]). This is used both for find and copy clipboards. This history is presently stored in user defaults which is bad (can grow big and affect performance). Instead it might be useful to use CoreData (if we were in the App Store then we could even offer users to sync clipboard history).

8.  The clipboard history pop-ups (⌃⌥⌘V and ⌃⌥⌘F) are very crude ([OakPasteboardSelector.mm][]). It would be nice if one could “type to search”. Perhaps similar to Adium, where if you type a letter (with focus in the contact list) a search field appears above the list, which is what then filters the list.

9.  Don’t store transient data in the clipboard history: <http://nspasteboard.org/Site/Transient.html>

10. Expand/collapse in [Find][] window.

11. Switch codebase to use ARC.

12. Migrate to Cocoa auto-layout.

12. Implement `OakTabTriggerImage`. This should be an `NSImage` subclass that simply renders a tab trigger. This would be used in the menus and bundle item selector, probably also bundle editor. Making it an `NSImage` subclass should allow embedding it in attributed strings (which is what we use for the menu items as augmenting menu rendering is not really possible with Cocoa, only to replace the full item with a custom view). For how to go about this look e.g. at the implementation of [OakFileIconImage][].

13. Look at [open issues][] :)

[regexp]:           https://github.com/textmate/textmate/tree/master/Frameworks/regexp
[parser.cc]:        https://github.com/textmate/textmate/blob/master/Frameworks/regexp/src/parser.cc
[format_string.cc]: https://github.com/textmate/textmate/blob/master/Frameworks/regexp/src/format_string.cc
[OakFilterList]:    https://github.com/textmate/textmate/tree/master/Frameworks/OakFilterList
[scm]:              https://github.com/textmate/textmate/tree/master/Frameworks/scm
[api.h]:            https://github.com/textmate/textmate/tree/master/Frameworks/scm/src/drivers/hg.cc
[hg.cc]:            https://github.com/textmate/textmate/tree/master/Frameworks/scm/src/drivers/api.h
[FSDataSource.h]:   https://github.com/textmate/textmate/blob/master/Frameworks/OakFileBrowser/src/io/FSDataSource.h
[OakPasteboard.h]:  https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboard.h
[OakPasteboardSelector.mm]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboardSelector.mm
[Find]:             https://github.com/textmate/textmate/tree/master/Frameworks/Find
[open issues]:      https://github.com/textmate/textmate/issues
[OakFileIconImage]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakFileIconImage.mm
