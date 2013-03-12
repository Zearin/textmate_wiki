TextMate has a few settings which are not exposed in the GUI.

You can change these with the [`defaults`](http://developer.apple.com/documentation/Darwin/Reference/ManPages/man1/defaults.1.html) shell command but you need to do this while TextMate is not running.

You set a key to a given value with the following syntax:

	defaults write com.macromates.TextMate.preview «key» «value»

You can always reset a key to its default value using:

	defaults delete com.macromates.TextMate.preview «key»

Or you can read the value of a key using:

	defaults read com.macromates.TextMate.preview «key»

## Disabling Extended Attributes

TextMate use extended attributes to store caret position and similar.

On file systems which don’t support extended attributes (most network file systems) OS X will create an auxiliary file with a dot-underscore prefix, e.g. `._filename`.

If you don’t want these files, you can disable the use of extended attributes, this is presently controlled with the `volumeSettings` defaults key which value is an associative array with path prefix and another associative array with settings for that path (presently only `extendedAttributes` is supported).

So if for example we wish to disable extended attributes for files under `/net/` we can do:

	defaults write com.macromates.TextMate.preview volumeSettings '{ "/net/" = { extendedAttributes = 0; }; }'

## Changing Line Height

You can adjust line height by changing the `fontLeadingDelta` and `fontAscentDelta` defaults keys.

These must be set as floats or integers (not strings), e.g.:

    defaults write com.macromates.TextMate.preview fontLeadingDelta -float 0

The default value for both keys is `1`.

## Disabling Anti Alias

Anti-alias can be disabled using the following:

	defaults write com.macromates.TextMate.preview disableAntiAlias -bool YES

## Disabling Clipboard History

If you relaunch TextMate it will remember the clipboard history from last session. This is stored in its user defaults.

If you dislike this, e.g. if you copy/paste a lot of passwords, then you can disable the feature like this:

	defaults write com.macromates.TextMate.preview disablePersistentClipboardHistory -bool YES

## Inheriting Environment Variables

When TextMate run commands it creates a “clean” environment, only inheriting a select few variables from its parent process. You can alter the whitelist via the `environmentWhitelist` defaults key. This is a colon-separated list of variables to inherit. If an item in the list contains an asterisk, then it is treated as a glob.

Example:

	defaults write com.macromates.TextMate.preview environmentWhitelist '$default:MANPATH:*EDITOR'

Here `$default` will expand to TextMate’s default whitelist.

Normally TextMate will setup `HOME`, `PATH`, `TMPDIR`, `LOGNAME`, and `USER`. If you whitelist any of these, then the variable (if set) will instead be inherited from the parent process.

## Disabling File Browser Auto-resize

When you show/hide the file browser, the window will adjust its width accordingly. This can be disabled using:

	defaults write com.macromates.TextMate.preview disableFileBrowserWindowResize -bool YES

# Keybindings

Key bindings are consulted in the following order (first file with a binding wins):

	~/Library/Application Support/TextMate/KeyBindings.dict
	/path/to/TextMate.app/Contents/Resources/KeyBindings.dict
	~/Library/KeyBindings/DefaultKeyBinding.dict
	/Library/KeyBindings/DefaultKeyBinding.dict
	/System/Library/Frameworks/AppKit.framework/Resources/StandardKeyBinding.dict

If you edit any of the above files you will need to relaunch TextMate (⌃⌘Q) before the changes take effect.

## Find and extend selection

These two action methods find the next/previous occurrence of what’s on the find clipboard and selects that, but preserves the existing selection.

	findNextAndModifySelection:
	findPreviousAndModifySelection:

One could e.g. add this to the key bindings:

	"@d" = ( "copySelectionToFindPboard:", "findNextAndModifySelection:" );

## Indent-aware movement

If you want (⇧)⌘⇠/⌘⇢ and ⌘⌫/⌘⌦ to ignore leading indent, you can add the following to your key bindings file:

	"@\UF702"  = "moveToBeginningOfIndentedLine:";
	"$@\UF702" = "moveToBeginningOfIndentedLineAndModifySelection:";
	"@\UF703"  = "moveToEndOfIndentedLine:";
	"$@\UF703" = "moveToEndOfIndentedLineAndModifySelection:";
	"@\U007F"  = "deleteToBeginningOfIndentedLine:";
	"@\UF728"  = "deleteToEndOfIndentedLine:";
