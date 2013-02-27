A bug report should contain these 4 things:

1. **Steps to reproduce**: You should give **detailed** steps on how someone can reproduce the problem.
	* Start from scratch (e.g. _“1. Create a new document, 2. Change language to Ruby, 3. …”_).
	* Explicitly mention every action involved and how it is invoked, e.g. say _“Select Cut from the Edit menu”_ or alternatively _“Press <kbd>⌘X</kbd>”_ rather than _“delete the text”_.
	* Keep the steps to a minimum.

2. **Expected result**: It’s important to include the result you are expecting as it might differ from how the program was designed to work.

3. **Actual result**: This is also important because it could be that following your steps on a different system does not reproduce your issue.

4. **Environment**: This would be OS version, version of TextMate, the language you are working in, and other possibly relevant information, for example if you are seeing graphics artifacts and you are on a retina Macbook Pro, then you should include that.

## Writing the Title

See [this great article by Jakob Nielsen on writing headlines, page titles, and subject lines](http://www.nngroup.com/articles/microcontent-how-to-write-headlines-page-titles-and-subject-lines/).

## Crashes or Hangs

Unless you have steps to reproduce, there is generally no need to report a crash, as we already get crash reports from users who haven’t opted out. You can change this in Preferences → Software Update.

If you are opening an issue about TextMate crashing then you should include the corresponding crash report. You can find a list of submitted reports in notification center. Click an entry to see the online version, which gives you a link that can be included in the issue. You should also be able to find crash reports for your system online under [my crashes](https://api.textmate.org/crashes/myip).

If the program locks up, that is different from a crash and you should find or create a “spin report”. These can normally be found as:

    /Library/Logs/DiagnosticReports/TextMate_«time»_«host».hang

You can generate one while the program is locked up by launching Activity Monitor, selecting TextMate, and then _Sample Process_ (<kbd>⌥⌘S</kbd>).

Since GitHub’s issue tracker does not allow attaching files, you should paste the spin report online via https://gist.github.com/

## Adding Pictures

If you include pictures or movies then be sure that the bug report can stand on its own even without these. For example opening an issue stating that “syntax highlight is incorrect” and only including an image is not useful.
