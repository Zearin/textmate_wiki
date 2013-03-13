# Snippets

1. Allow hierarchical snippets
 * i.e., ${1:lists{|subone,subtwo|}coding{subone,subtwo|}}
2. Allow key:value snippets (so user can see a label rather than the snippet itself)
 * i.e., ${1:<get help>?#help(withfun(1)}
2. Allow snippets to disallow tab expansion of placeholders with a !
 * i.e., ${!1:dont_expand_this}

# Commands
1. Provide a method so tht commands in any language can call a dialog for user input.
 * perhaps a $TM_USERINPUT which calls a dialog (maybe written as an html form) and returns the output

# Macros

1. Allow setting of Pboards in a macro:

<pre>
    setFindPboard:='(?&lt;! )=(?! )'
    setReplacePboard:=' = '
    ReplaceAllInSelection:
</pre>

Probably not needed given the ability to do [this](http://pastie.org/private/jhzsmadg4m3rjns6bsfg)


# $TM_* variables

1. Add a TM_FILEPATHS_IN_WINDOW returning a list of paths to files open in a window
2. 
