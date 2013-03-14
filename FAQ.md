## Editing

### The new completion method gets confused when variables, etc are prefixed with a character in some cases but not others. Is there a way to improve this?

[This article](http://blog.macromates.com/2012/clever-completion/ "TextMate Blog » Clever Completion") explains how (word) “units” are setup in 2.0 and this is what completion uses. I.e. ‘:symbol’ is a different unit than ‘symbol’ so one is not suggested when completing the other.

There is no way to “fix” this other than make changes to what is considered a unit. The source bundle has these settings, but it also affects word movement, double-click, etc.

### Is is possible to have trailing whitespace removed when a file is saved?

There are currently two possible ways to do this both using the semantic class system:

You can use `callback.document.export` which will filter the document that is saved to disk, but not update the copy inside TextMate. The inverse is also possible with `callback.document.will-save` where the copy inside TextMate will be updated before saving.

### Is it possible to disable soft wrap?

There is a toggle in the View menu to turn on/off soft wrap. This stores the setting “for the current file type”.

Even with soft wrap disabled there are setting items in the Source bundle to enable indented soft wrap for comments in source files. These can be disabled by unchecking the "Enable this item" checkbox in the bundle editor.

### Is it possible to disable auto-paired characters?

There is presently no global setting for disabling this, but you can create a new settings item that disables them.

 1. Open Bundle Editor: _Bundles → Edit Bundles…_ (<kbd>⌃⌥⌘B</kbd>).
 2. Create a new bundle: File → New (<kbd>⌘N</kbd>) and select _Bundle_.
 3. Create a new setting in that bundle: File → New (<kbd>⌘N</kbd>) and select _Setting_.
 4. Set _Scope Selector_ to `*` (matches everywhere).
 5. Set the content to the following property list:

		{   
			smartTypingPairs = ( );
		}

 6. Save the new item: _File → Save_ (<kbd>⌘S</kbd>).

### In 1.x a return between `{}` was treated specially giving you an indented caret on a blank line, this no longer works in the alpha.

This is a complicated issue that was explained best in [this mailing list post](http://lists.macromates.com/textmate/2012-January/034108.html "[TxMt] Re: Indentation (TM2 R bundle)").

### Indentation isn't behaving correctly in some languages, how can I correct this?

The indentation rules have been given a higher importance now which means that some languages have rules that aren't quite good enough anymore. For bundle authors and those that want to get their hands dirty [the guide to indentation rules](http://manual.macromates.com/en/appendix#indentation_rules.html "TextMate Manual » Appendix") is in the 1.x manual.

There are of course some languages where having indentation rules at all doesn't make sense like Python where the indentation is based on whitespace rather than other delimiters. For these languages you can disable the automated indentation entirely by making a new settings item, scoped to the language, containing:

	{ disableIndentCorrections = :true; }

If you'd rather disable the indentations entirely you can do the same and just not give it a scope to make it global.


## Projects

### Where have the project files from 1.x gone?

Explicit project files are currently not supported. When you open a folder then that folder is treated as a project, i.e. the file chooser (⌘T) and folder search (⇧⌘F) will default to this folder.

You can customize settings for a folder with a [.tm_properties file](http://blog.macromates.com/2011/git-style-configuration/ "TextMate Blog &raquo; Git Style Configuration").

Allan has made a couple posts in a longer thread about this topic:

- [On how project files no longer are needed](http://lists.macromates.com/textmate/2011-December/033403.html "[TxMt] Re: Projects are gone in TM2?").
- [Some background on this choice](http://lists.macromates.com/textmate/2011-December/033522.html "[TxMt] Re: Projects are gone in TM2?").

### How do I have a project containing files/folders from different locations of a file system?

With the directory-centered focus this is no longer directly possible, however you can use a directory containing symlinks to the various other directories and files.

Note that by default Find in Folder does not follow symlinks. See other FAQ item on how to make it follow symlinks.


## Interface

### Aliased/linked folders in the file browser are not expandable.

This is similar to how Finder treats links and there is presently no way to have them expand inline.


## Known Limitations

### I cannot get my bundles to appear inside TextMate?

First make sure you are placing them in the [right location](http://blog.macromates.com/2011/locating-bundles/ "TextMate Blog » Locating Bundles"). Second is to make sure they are on a drive that supports fs-events, generally this means a local HFS+ drive. There does however seem to be a bug with HFS+ where fs-events fails to work after a user has been using Dropbox to sync folders.

### I am seeing incorrect results after using a Replace All in Find in Folder.

Find in Folder currently expects all files to be UTF-8 encoded, if your files do not match this assumption you should presently avoid using this feature.

### How do I get a web preview window that updates as I edit an HTML document?

The current plan is to generalize the update mechanism through the semantic class system so it can be used in more cases. This is however not implemented yet and is subject to change.

### Will printing support be improved from 1.x?

If it’s not there and was there in 1.x, it’s most likely that we haven’t gotten around to doing it yet. Of course 2.0 will get a printing feature.

### Can [rmate](http://blog.macromates.com/2011/mate-and-rmate/ "TextMate Blog &raquo; mate and rmate") be used to open directories?

No — `rmate` simply sends a file back and forth. Opening a folder is way more complex.


## Search

### Is it possible to have Find in Folder follow symlinks?

In the Find in Folder window is a drop-down menu button placed above the results. Enable “Follow Symbolic Links” in this menu.

This will not resolve aliases created with Finder.

## Bundle Items

### Using Duplicate Line with multiple carets produces an error.

Duplicate Line is implemented as a command. Presently these are not supported (per se) for multiple carets.
