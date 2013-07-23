## Editing

### Completion considers `$var`, `@var`, and `var` as different

[This article](http://blog.macromates.com/2012/clever-completion/ "TextMate Blog » Clever Completion") explains how (word) “units” are setup in 2.0. This is what completion uses. For example ‘:symbol’ is different than ‘symbol’, so one isn’t suggested when completing the other.

The way to change this is to change what TextMate considers a unit. The source bundle has the default settings. You can add a new setting scoped to `punctuation`, and make it `{ characterClass = 'punctuation'; }`, that way all the punctuation (like leading `$` in a `$variable`) is assigned a different character class than the rest of the unit, effectively making it two different units.

Be aware though that definition of units are also used for word movement (<kbd>⌥←</kbd>/<kbd>⌥→</kbd>) and word selection (<kbd>⌃W</kbd>).

### How to strip trailing whitespace on save?

There are currently two possible ways to do this (both of which use the semantic class system):

1. You can use `callback.document.export`, which will filter the document that’s saved to disk (but *won’t* update the copy inside TextMate)
1. The inverse is also possible: `callback.document.will-save` (which will update the copy in TextMate *before* saving)

Here is [a bundle to strip whitespace](https://github.com/bomberstudios/Strip-Whitespace-On-Save.tmbundle) that makes use of the `callback.document.will-save` class.

### How to disable soft wrap?

The **View** menu has a setting to toggle soft wrap. (It stores the setting for the “current file type”.)

Even with soft wrap disabled, there are settings in the Source bundle to enable indented soft wrap for comments in source files. These can be disabled by unchecking the “Enable this item” checkbox in the bundle editor.

For more info see this [mailing list post about indented soft wrap](http://lists.macromates.com/textmate/2011-December/033547.html).

### How to disable auto-paired characters?

See [hidden settings](https://github.com/textmate/textmate/wiki/Hidden-Settings#disabling-auto-paired-characters).

### In TextMate 1.x, a return between `{}` was treated specially, giving you an indented caret on a blank line. This no longer works in the alpha.

This is a complicated issue, explained best in [this mailing list post](http://lists.macromates.com/textmate/2012-January/034108.html "[TxMt] Re: Indentation (TM2 R bundle)").

### Indentation isn’t behaving correctly in some languages. How can I correct this?

The indentation rules have been given a higher importance in TextMate 2. As a result, some language rules aren’t up-to-date with the new precedence. For bundle authors (and those that want to get their hands dirty) [the guide to indentation rules](http://manual.macromates.com/en/appendix#indentation_rules.html "TextMate Manual » Appendix") is in the 1.x manual.

Of course, indentation rules make no sense in certain languages--Python’s indentation, for example, is based on whitespace, rather than other delimiters. For these languages, you can disable the auto-indentation entirely by adding a new settings item (scoped to the language) as follows:

	{ disableIndentCorrections = :true; }

If you’d rather disable the indentations entirely, do the same thing without giving it a scope.


## Projects

### Where have the project files from 1.x gone?

Explicit project files aren’t currently supported. When you open a folder, the folder is treated as a project.  I.e. the file chooser (<kbd>⌘T</kbd>) and folder search (<kbd>⇧⌘F</kbd>) default to the folder.

You can customize settings for a folder with a [.tm_properties file](http://blog.macromates.com/2011/git-style-configuration/ "TextMate Blog » Git Style Configuration").

Allan’s written a couple posts in a longer thread about this:

- [On how project files no longer are needed](http://lists.macromates.com/textmate/2011-December/033403.html "[TxMt] Re: Projects are gone in TM2?").
- [Some background on this choice](http://lists.macromates.com/textmate/2011-December/033522.html "[TxMt] Re: Projects are gone in TM2?").

### How do I create a project with files/folders from different locations in the file system?

With the directory-centered focus, this is no longer directly possible. However, you can simply add symlinks to the various other directories and files.

**Note:** By default, *Find in Folder* does not follow symlinks. (See other FAQs on how to make it follow symlinks.)


## Interface

### Aliased/linked folders in the file browser aren’t expandable.

This is similar to how Finder treats links. There’s currently no way to have them expand inline.


## Known Limitations

### I cannot get my bundles to appear inside TextMate. 

For standard bundles you should install via Preferences → Bundles.

Third party bundles can be double-clicked which installs them in:

	~/Library/Application Support/Avian/Pristine Copy/Bundles

If you wish to edit the bundles and share your changes you should install (git clone) them to:

	~/Library/Application Support/Avian/Bundles

This way TextMate won’t create delta files (which are not useful for sharing).

If you manually install bundles and they do not show up, your file system may lack support for fs-events. In this case you will need to delete the cache and relaunch TextMate:

	rm ~/Library/Caches/com.macromates.TextMate/BundlesIndex.plist

### I am seeing incorrect results after using a Replace All in Find in Folder.

Find in Folder currently expects all files to be UTF-8 encoded. If your files aren’t, you should avoid using this feature for now.

### How do I get a web preview window that updates as I edit an HTML document?

The current plan is to generalize the update mechanism through the semantic class system, so it can be used in more cases. However, this isn’t yet implemented, and subject to change.

### Can [rmate](http://blog.macromates.com/2011/mate-and-rmate/ "TextMate Blog » mate and rmate") be used to open directories?

No — `rmate` simply sends a file back and forth. Opening a folder is way more complex.


## Search

### Is it possible to have Find in Folder follow symlinks?

Within the *Find in Folder* window, there’s a drop-down menu above the results. Enable “Follow Symbolic Links” in this menu.

This *will not* resolve aliases created with Finder.

## Bundle Items

### Using Duplicate Line with multiple carets produces an error.

Duplicate Line is implemented as a command. Currently, these aren’t supported (per se) for multiple carets.