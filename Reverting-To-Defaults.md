Many problems can be solved by reverting to default settings. This is done by quitting TextMate and then removing the following files and folders:

 1. `~/Library/Application Support/Avian`
 1. `~/Library/Application Support/TextMate`
 1. `~/Library/Caches/com.macromates.TextMate/BundlesIndex.plist`
 1. `~/Library/Preferences/com.macromates.textmate.plist`
 1. `~/.tm_properties`

Be aware that not all files/folders listed may exist, and any potential customizations will be lost.

As `.tm_properties` files can be in arbitrary folders, you may have more than the one in your home folder. Though TextMate doesn’t create these by itself, so if you never created any, there is no reason to go hunting for them.

See also [troubleshooting for TextMate 1.x](http://wiki.macromates.com/Troubleshooting/).