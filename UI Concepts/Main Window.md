*Please use the [TextMate Developers mailing list](http://lists.macromates.com/listinfo/textmate-dev "textmate-dev Info Page") to discuss these UI concepts.*

[![Main Window](UI Concepts/images/main_window_v12.png)](UI Concepts/images/main_window_v12.png "Main Window")

*Click image to see full size.*

## Overview

The goal behind this design was to create a clean new look for TextMate while sticking with standard recognizable widgets whenever possible. Buttons/menu sizes have increased to provide easier mouse targets.

## Sidebar

[[images/sidebar_menu_v1.png|align=right|float]]

The top bar contains a menu with the filepath in addition to any items pertaining to the directory as a whole. This is where you would be able to toggle a directory to be a project and be able to open the `.tm_properties` file or create a new one.

In the file list you have a close icon beside open tabs which switches to a circle when the file contains unsaved changes, this is to mirror the closebox of the tabs above. Otherwise the file list functions the same as it does currently.

Along the bottom:

* Add a new file to the current directory.
* An action menu that has commands that effect the currently selected file(s), this would be the same as the contextual (right-click) menu.
* Show the favorites directory.
* Show the SCM status overview, would be grayed out when not in a directory under source control.

The favorites and SCM status buttons would be toggles that would return the user to the previous directory if clicked while already active.

## Bottom Bar

* Split-view, to be covered on another page later.
* Line/Column
* Language Grammar Menu
* Bundles Menu (Needs a different icon.)
* Symbol List Menu

## Incomplete / Todo

The gutter is rendered plainly here as I would like to work on a redesign of it separately.

While split-view and fullscreen buttons are present I plan to address their implementation separately as they are very complicated concepts.

Project directories should be highlighted in some fashion, both in the file list and when you are in one, haven't come up with a good method to do this. A way to to go up to the root of the project might be a good addition as well.

I have a concept for a warning when you are freehand or overwrite mode, or are currently recording a macro, I will be posting that soon.

– [Infininight](https://github.com/infininight/)