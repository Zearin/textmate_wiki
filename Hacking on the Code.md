Here are some self-contained projects that shouldn’t require too much knowledge about the code base, as they are fairly isolated:

1.	Enhancing the syntax for format strings 
	The format string syntax allows replacements for variables as follows:

		${«variable»/«regexp»/«replacement»/«flags»}

	For example, to replace spaces with dashes in the `$TM_FULLNAME` variable we might do:

		${TM_FULLNAME/ /-/g}

	It would be useful to support variables in the regular expression part of the expression. This is for `.tm_properties` where we e.g. can set `windowTitle` to a format string, and would like to set it e.g. to:

		windowTitle = "$TM_DISPLAYNAME — ${TM_FILEPATH/^$TM_PROJECT_DIRECTORY\///}"

	Here we wish to chop off the `$TM_PROJECT_DIRECTORY` path prefix of `$TM_FILEPATH`.

	The support for format strings is in the [regexp][] framework. Look at [parser.cc][] and [format_string.cc][].

2.	New (native) commit window.

	The current commit window is a separate application which is “always on top” and by not using the OakTextView we miss out on all the nice features of the Git commit message grammar like `fix→` for `fixup!`’s and highlights of too long summary lines.

6.	Custom data sources for file browser, e.g. Simplenote support or sftp, see [FSDataSource.h][].

7.  There is a pasteboard subclass which maintains a history ([OakPasteboard.h][]). This is used both for find and copy clipboards. This history is presently stored in user defaults which is bad (can grow big and affect performance). Instead it might be useful to use CoreData (if we were in the App Store then we could even offer users the facility to sync their clipboard history).

8.  The clipboard history pop-ups (⌃⌥⌘V and ⌃⌥⌘F) are very crude ([OakPasteboardSelector.mm][]). It would be nice if one could “type to search”. Perhaps similar to Adium, where if you type a letter (with focus in the contact list) a search field appears above the list, which is what then filters the list.

9.  Don’t store transient data in the clipboard history: <http://nspasteboard.org/Site/Transient.html>

12. Implement `OakTabTriggerImage`. This should be an `NSImage` subclass that simply renders a tab trigger. This would be used in the menus and bundle item selector, probably also bundle editor. Making it an `NSImage` subclass should allow embedding it in attributed strings (which is what we use for the menu items as augmenting menu rendering is not really possible with Cocoa, only to replace the full item with a custom view). For how to go about this look e.g. at the implementation of [OakFileIconImage][].

13. Look at [open issues][] — also look at [bundle issues][].

[regexp]:           https://github.com/textmate/textmate/tree/master/Frameworks/regexp
[parser.cc]:        https://github.com/textmate/textmate/blob/master/Frameworks/regexp/src/parser.cc
[format_string.cc]: https://github.com/textmate/textmate/blob/master/Frameworks/regexp/src/format_string.cc
[FSDataSource.h]:   https://github.com/textmate/textmate/blob/master/Frameworks/OakFileBrowser/src/io/FSDataSource.h
[OakPasteboard.h]:  https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboard.h
[OakPasteboardSelector.mm]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboardSelector.mm
[open issues]:      https://github.com/textmate/textmate/issues
[bundle issues]:    https://github.com/organizations/textmate/dashboard/issues
[OakFileIconImage]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakFileIconImage.mm
