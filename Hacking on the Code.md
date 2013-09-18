Here are some self-contained projects that shouldn’t require too much knowledge about the codebase, as they are fairly isolated.

2.	**New (native) commit window.**

	The current commit window is a separate application which is “always on top”. By not using `OakTextView`, we’re missing out on all the nice features of the Git commit message grammar—like `fix→` for `fixup!`’s, and highlights from summary lines that are too long.

6.	**Custom data sources for file browser**
		
	For example: Simplenote support, or sftp. See [FSDataSource.h][].

7.	**Update clipboards to use CoreData**  
	
	There’s a pasteboard subclass which maintains a history ([OakPasteboard.h][]). It’s used for both *find* and *copy* clipboards. 
	
	Presently, this history is stored in user defaults. This is bad! It can grow big, and worsen performance. Instead, it might be useful to use CoreData. (If we were in the App Store, we could even offer users the ability to sync their clipboard history.)

8.  **Update clipboard history pop-ups**
	
	The clipboard history pop-ups (<kbd>⌃⌥⌘V</kbd> and <kbd>⌃⌥⌘F</kbd>) are very crude ([OakPasteboardSelector.mm][]). A “type to search” functionality would be much better.
	
	Adium provides a useful example. When the contact list has focus, typing a letter opens a search field above the list. As the user continues typing, the list is filtered accordingly.

9.  **Don’t store transient data in the clipboard history**
	
	[http://nspasteboard.org/Site/Transient.html]

12. **Implement `OakTabTriggerImage`**
	
	This should be an `NSImage` subclass which simply renders a tab trigger. It would be used in the menus and bundle item selector (and probably, also bundle editor). 
	
	Making it an `NSImage` subclass should allow embedding it in attributed strings. This is what we use for the menu items, since it isn’t really possible to augment menu rendering in Cocoa. (The only workaround is to replace the full item with a custom view.) 
	
	For how to do this, check out the implementation of [OakFileIconImage][].

[FSDataSource.h]:   https://github.com/textmate/textmate/blob/master/Frameworks/OakFileBrowser/src/io/FSDataSource.h
[OakPasteboard.h]:  https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboard.h
[OakPasteboardSelector.mm]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboardSelector.mm
[OakFileIconImage]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakFileIconImage.mm
