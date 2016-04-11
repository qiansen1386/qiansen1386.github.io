+++
categories = [ "开发", "dev", "English", "中文"]
date = "2016-04-09T05:05:53Z"
tags = ["Vagrant", "Shell", "DevOps", "Ruby"]
title = "frontend learning note 3 - Vagrant, VM & Shell"

+++

The Lesson I Learnt
---------

### Line-ending issue

Make sure the line ending of your provision script is LF-only(unix-style), otherwise the behaviors would be very unpredictable.
Unwated `\r` will appears everywhere...

### scripts heading

`#!/bin/bash` is not omissible. Of course, you can use `#!/bin/sh` or `#!/bin/zsh`.

### Symlinks are huge problem! 

[npm-issues#7308](https://github.com/npm/npm/issues/7308) => Symlinks within shared folder could not be sync between Win and Posix OS. However many NPM packages would like to create bin-links(symlinks of executable file within bin folder). So whenever you tried to install some packages, it is very likely to fail. So there are 3 potential solutions: 1. try to make it work by proper config virtualbox. 2. Move the node_modules out of synced-folder. 3. use `--no-bin-links` flag for `npm install`.
Let me just reveal the final answer. Only No.3 works, with side-effect though. 

Firstly, there is script provided by [drmyersii](https://github.com/drmyersii)(The author of [vagrant-node-env](https://github.com/drmyersii/vagrant-node-env))

```Ruby
config.vm.provider "virtualbox" do |v|
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/vagrant", "1"]
end
```
It doesn't work at least for Windows 7 Host. I didn't investigated further, due to tied schedule. You can try it if you want, I'd like to know if it works on you :P

Then, I tried to created a `node_modules/` folder under `/tmp/`, but another unexpected issue supprised me. [npm-issue#10013](https://github.com/npm/npm/issues/10013) It turns out the NPM 3 introduced some special checks, causing the breaks of `npm install`. If npm fixed this in further versions, or if you can roll back to a ealier version, It could be the best choice. With no side effects, and can be easily setup using provision scripts. I would continue following on.


The end, I am afraid that I have to go for the `--no-bin-links` approach. Em, that means there will be no more bin links. peroid. That would make cli operations much more undesirable. If you need those short-cuts, try to install them globally as well. So that when you call them, the global version can still response to u. Dirty, but works.

### Ruby

Nothing to share, just to show off how I learnt a new language! (@ beginer level..) Ruby is like PHP, lovers love it, haters hate it. I love PHP, but I hate Ruby at the first place. Its unique syntax caused me so many frustration. To be clear, it is my problem, not Ruby's. Because I am not only new to it, but also too anxious. Whereas, Ruby's syntax is so distinctive(also complicated). But hey, I tried it, and it was fun when I start to get it! I didn't get chance to practice `Metaprogramming` much. What I can still tell is, the syntax suger is super handy. On the other hand, it is not as terse as golang/python, meaning that there is still a significant learning curve for coder who use other languages. 

Time for Referances
-----------

### Vagrant


### VIM

>

- [How I boosted my Vim](http://nvie.com/posts/how-i-boosted-my-vim/)
- [Learn VIM interactively with openvim](http://www.openvim.com/)
- [Vim Is Awesome: Make It Better With These 5 Customizations](http://www.makeuseof.com/tag/5-things-need-put-vim-config-file/)