By default, TextMate writes errors to the standard error (STDERR) file descriptor.

Unfortunately, this means that it is no longer visible anywhere (AFAIK) unless you run TextMate from a terminal, e.g.:

    /path/to/TextMate.app/Contents/MacOS/TextMate

To redirect logging, you can set the `LOG_PATH` environment variable (prior to launching TextMate), which will make TextMate create `TextMate.log` in the location given.

The easiest way to do this is:

1. Run the following in a terminal:
    `launchctl setenv LOG_PATH "$HOME/Library/Logs"`
2. Then (re-)launch TextMate. 

Possibly running the following additional command in your terminal:

    tail -f ~/Library/Logs/TextMate.log

**Note** that each time you launch TextMate, the log file is re-created (so output from previous sessions is lost).
