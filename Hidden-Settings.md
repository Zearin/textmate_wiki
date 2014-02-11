TextMate has a few settings which are not exposed in the GUI.

You can change these with the [`defaults`](http://developer.apple.com/documentation/Darwin/Reference/ManPages/man1/defaults.1.html) shell command. (Make sure you do this while TextMate is **not** running!)

- **Set a key:**

		defaults write com.macromates.TextMate.preview «key» «value»

- **Reset a key to its default:**

		defaults delete com.macromates.TextMate.preview «key»

- **Read a key’s value:**

		defaults read com.macromates.TextMate.preview «key»


## Disabling Auto-paired Characters

When you type an opening brace, parenthesis, quote character, or similar, TextMate will insert the closing character, this can be configured per scope or globally disabled using:

    defaults write com.macromates.TextMate.preview disableTypingPairs -bool YES

## Disabling Extended Attributes

TextMate use extended attributes to store caret position, etc.

On file systems which don’t support extended attributes (most network file systems), OS X will create an auxiliary file with a dot-underscore prefix (e.g. `._filename`).

If you don’t want these files, you can disable the use of extended attributes. This is presently controlled with the `volumeSettings` key. Its values are (1) an associative array with path prefix; and (2) another associative array with settings for that path. (Presently, only `extendedAttributes` is supported.)

So, if we wanted to disable extended attributes for files under `/net/`:

    defaults write com.macromates.TextMate.preview volumeSettings '{ "/net/" = { extendedAttributes = 0; }; }'

## Disabling Tab Re-ordering

When opening a document it will be placed to the right of the current one (in the tab bar) even if the document being opened is already in the tab bar, this is to make ⌘W work to “close and go back” without having to keep a list of previously selected tabs.

This feature can now be disabled using:

    defaults write com.macromates.TextMate.preview disableTabReordering -bool YES

Note though that if one selects multiple documents to open then it will potentially re-order the tab bar so that the documents selected are adjacent.

## Disabling Restore of Open Tabs

When opening a folder TextMate will restore open tabs and file browser state from the last time you had this folder open. The behavior can be disabled using:

    defaults write com.macromates.TextMate.preview disableFolderStateRestore -bool YES

## Searching “Selection” Instead of “Document” by Default

Previously using <kbd>⌘F</kbd> with a multiline selection would automatically set the “in” pop-up to “selection”. This is no longer the case, but can be brought back by running:

    defaults write com.macromates.TextMate.preview findInSelectionByDefault -bool YES

## File Browser Single Click to Open

Opening files in the file browser can be done by single-clicking the icon. If you think the click-target is too small, you can make it open by clicking the text instead, this is activated by running the following in a terminal:

    defaults write com.macromates.TextMate.preview fileBrowserSingleClickToOpen -bool true

If you wish to select items you either need to click to the left of the text, or hold down command (⌘) when clicking the item’s text.

Holding down command (⌘) while clicking the icon will reveal the file in Finder regardless of the above setting.

## File Browser Source List Styling

The file browser can use the “source list” style as seen in Finder’s sidebar:

    defaults write com.macromates.TextMate.preview fileBrowserStyle SourceList

If you want to revert to the standard look, delete the `fileBrowserStyle` key.

## File Browser Open (Zoom) Animation

The zoom animation shown when opening items can be disabled by running this in a terminal:

    defaults write com.macromates.TextMate.preview fileBrowserOpenAnimationDisabled -bool YES

## Changing Line Height

You can adjust line height by changing the `fontLeadingDelta` and `fontAscentDelta` defaults keys.

These *must* be set as floats or integers--*not* strings.

    defaults write com.macromates.TextMate.preview fontLeadingDelta -float 0

Both keys’ default value is `1`.


## Controlling Font Smoothing

Font smoothing refers to sub-pixel anti-alias on LCD screens. The algorithm Apple uses will often make light text on dark backgrounds appear bolder than the same text on a bright background.

For this reason TextMate disables font smoothing when using dark themes and the user is on a high-DPI display (retina Mac).

You can control the behavior with:

	defaults write com.macromates.TextMate.preview fontSmoothing «value»

Here `«value»` can be:

 * `0`: Always disabled.
 * `1`: Always enabled.
 * `2`: Disabled for dark themes.
 * `3`: Disabled for dark themes on high-DPI displays (default).

If you wish to restore the default value (`3`) it’s better to run the following, rather than explicitly setting the value to `3`:

	defaults delete com.macromates.TextMate.preview fontSmoothing


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

If you want <kbd>⌘⇠</kbd>, <kbd>⇧⌘⇠</kbd>, <kbd>⌘⇢</kbd>, <kbd>⇧⌘⇢</kbd>, <kbd>⌘⌫</kbd>, and <kbd>⌘⌦</kbd> to ignore leading indentation, add the following to your key bindings file:

	"@\UF702"  = "moveToBeginningOfIndentedLine:";
	"$@\UF702" = "moveToBeginningOfIndentedLineAndModifySelection:";
	"@\UF703"  = "moveToEndOfIndentedLine:";
	"$@\UF703" = "moveToEndOfIndentedLineAndModifySelection:";
	"@\U007F"  = "deleteToBeginningOfIndentedLine:";
	"@\UF728"  = "deleteToEndOfIndentedLine:";