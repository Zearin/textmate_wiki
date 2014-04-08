Here are some self-contained projects that shouldn’t require too much knowledge about the codebase, as they are fairly isolated.

6.	**Custom data sources for file browser**
		
	For example: Simplenote support, or sftp. See [FSDataSource.h][].

12. **Implement `OakTabTriggerImage`**
	
	This should be an `NSImage` subclass which simply renders a tab trigger. It would be used in the menus and bundle item selector (and probably, also bundle editor). 
	
	Making it an `NSImage` subclass should allow embedding it in attributed strings. This is what we use for the menu items, since it isn’t really possible to augment menu rendering in Cocoa. (The only workaround is to replace the full item with a custom view.) 
	
	For how to do this, check out the implementation of [OakFileIconImage][].

[FSDataSource.h]:   https://github.com/textmate/textmate/blob/master/Frameworks/OakFileBrowser/src/io/FSDataSource.h
[OakPasteboardSelector.mm]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakPasteboardSelector.mm
[OakFileIconImage]: https://github.com/textmate/textmate/blob/master/Frameworks/OakAppKit/src/OakFileIconImage.mm
