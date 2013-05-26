By default TextMate write errors to the standard error file descriptor.

Unfortunately this means that it is no longer visible anywhere (AFAIK) unless you run TextMate from a terminal, e.g.:

    /path/to/TextMate.app/Contents/MacOS/TextMate

To redirect logging you can set the `LOG_PATH` environment variable (prior to launching TextMate) which will make TextMate create `TextMate.log` in the location given.

The easiest way to set this variable for TextMate is to run the following in a terminal:

    launchctl setenv LOG_PATH "$HOME/Library/Logs"

Then simply launch (or relaunch) TextMate. Possibly running the following additional command in your terminal:

    tail -f ~/Library/Logs/TextMate.log

Be aware that each time you launch TextMate, the log file is re-created, so output from previous sessions is lost.