TextMate has a few settings which are not exposed in the GUI.

You can change these with the [`defaults`](http://developer.apple.com/documentation/Darwin/Reference/ManPages/man1/defaults.1.html) shell command. (Make sure you do this while TextMate is **not** running!)

- **Set a key:**

		defaults write com.macromates.TextMate.preview «key» «value»

- **Reset a key to its default:**

		defaults delete com.macromates.TextMate.preview «key»

- **Read a key’s value:**

		defaults read com.macromates.TextMate.preview «key»


## Disabling Extended Attributes

TextMate use extended attributes to store caret position, etc.

On file systems which don’t support extended attributes (most network file systems), OS X will create an auxiliary file with a dot-underscore prefix (e.g. `._filename`).

If you don’t want these files, you can disable the use of extended attributes. This is presently controlled with the `volumeSettings` key. Its values are (1) an associative array with path prefix; and (2) another associative array with settings for that path. (Presently, only `extendedAttributes` is supported.)

So, if we wanted to disable extended attributes for files under `/net/`:

	defaults write com.macromates.TextMate.preview volumeSettings '{ "/net/" = { extendedAttributes = 0; }; }'


## Changing Line Height

You can adjust line height by changing the `fontLeadingDelta` and `fontAscentDelta` defaults keys.

These *must* be set as floats or integers--*not* strings.

    defaults write com.macromates.TextMate.preview fontLeadingDelta -float 0

Both keys’ default value is `1`.


## Disabling Anti Alias

Anti-alias can be disabled like so:

	defaults write com.macromates.TextMate.preview disableAntiAlias -bool YES


## Disabling Clipboard History

When you relaunch TextMate, it remembers the clipboard history from your last session. This is stored in its user defaults.

If you dislike this (for example, if you often copy & paste passwords), you can disable this feature:

	defaults write com.macromates.TextMate.preview disablePersistentClipboardHistory -bool YES

## Inheriting Environment Variables

When TextMate run commands, it creates a “clean” environment, which only inherits a select few variables from its parent process. 

You can alter the whitelist via the `environmentWhitelist` defaults key. This is a colon-separated list of variables to inherit. If an item in the list contains an asterisk, then it is treated as a glob.

Example:

	defaults write com.macromates.TextMate.preview environmentWhitelist '$default:MANPATH:*EDITOR'

Here, `$default` will expand to TextMate’s default whitelist.

Normally, TextMate sets up `HOME`, `PATH`, `TMPDIR`, `LOGNAME`, and `USER`. If you whitelist any of these, then the variable (if set) will inherit from the parent process instead.


# Keybindings

Key bindings are consulted in the following order (first file with a binding wins):

	~/Library/Application Support/TextMate/KeyBindings.dict
	/path/to/TextMate.app/Contents/Resources/KeyBindings.dict
	~/Library/KeyBindings/DefaultKeyBinding.dict
	/Library/KeyBindings/DefaultKeyBinding.dict
	/System/Library/Frameworks/AppKit.framework/Resources/StandardKeyBinding.dict

If you edit any these files, you’ll need to relaunch TextMate (<kbd>⌃⌘Q</kbd>) for changes to take effect.


## Find and extend selection

These two action methods find the next/previous occurrence of the Find clipboard’s contents and selects it--while simultaneously preserving the existing selection.

	findNextAndModifySelection:
	findPreviousAndModifySelection:

One could, for example, add this to the key bindings:

	"@d" = ( "copySelectionToFindPboard:", "findNextAndModifySelection:" );


## Indent-aware movement

If you want <kbd>⇧⌘⇠</kbd>/<kbd>⇧⌘⇢</kbd> and <kbd>⌘⌫</kbd>/<kbd>⌘⌦</kbd> to ignore leading indentation, add the following to your key bindings file:

	"@\UF702"  = "moveToBeginningOfIndentedLine:";
	"$@\UF702" = "moveToBeginningOfIndentedLineAndModifySelection:";
	"@\UF703"  = "moveToEndOfIndentedLine:";
	"$@\UF703" = "moveToEndOfIndentedLineAndModifySelection:";
	"@\U007F"  = "deleteToBeginningOfIndentedLine:";
	"@\UF728"  = "deleteToEndOfIndentedLine:";
