Welcome to the textmate wiki!

[command_line_tools without xcode (Mountain Lion download for support egetmobile.com usa mirror)](http://wsc.egetmobile.com/command_line_tools_for_xcode_os_x_mountain_lion_aug_2012.dmg)

Apple clang version 4.0 (tags/Apple/clang-421.0.60) (based on LLVM 3.1svn) Target: x86_64-apple-darwin12.0.0 

Here are particaly changed instructions for installing it with homebrew:

* ```curl -LsSf http://github.com/mxcl/homebrew/tarball/master | sudo tar xvz -C/usr/local –strip 1```

* ```brew install ragel boost pgrep multimarkdown hg```

* ```brew install --HEAD https://raw.github.com/adamv/homebrew-alt/master/head-only/ninja.rb```

* ```git clone --recursive https://github.com/textmate/textmate.git textmate```

* ```cd textmate```

* ```./configure && ninja```

## Automate updating your build to the latest origin/master.

* [textmatesparkle.sh](https://gist.github.com/3346357)