Welcome to the textmate wiki!

[command_line_tools without xcode (Mountain Lion)](http://adcdownload.apple.com/Developer_Tools/command_line_tools_os_x_mountain_lion_for_xcode__august_2012/command_line_tools_for_xcode_os_x_mountain_lion_aug_2012.dmg)

Apple clang version 4.0 (tags/Apple/clang-421.0.57) (based on LLVM 3.1svn) Target: x86_64-apple-darwin12.0.0 Thread model: posix

Here are particaly changed instructions for installing it with homebrew:

* ```brew install ragel boost pgrep multimarkdown hg brew install --HEAD https://raw.github.com/adamv/homebrew-alt/master/head-only/ninja.rb```

* ```git clone https://github.com/textmate/textmate.git```

* ```cd textmate```

* ```./configure && ninja```