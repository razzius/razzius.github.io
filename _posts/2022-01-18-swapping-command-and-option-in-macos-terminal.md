---
title: Swapping command and option in MacOS Terminal
date: 2022-01-18
---

I've been using a new [Framework](https://frame.work) laptop for my day-to-day personal computing, but for whatever reason I ended up on my old 2014 Macbook Air tonight.

Only one issue: on Ubuntu (which I use on my Framework), the Alt key, where Command is on Mac, acts as the Meta key and can be used for terminal shortcuts. Mac uses the Option key, but it's in an awkward position and I want to have my muscle memory translate between my devices.

I found a [Stack Overflow post](https://stackoverflow.com/questions/1856437/command-key-as-meta-key-in-os-x-terminal-app) about doing precisely this and tried to get it working in [Karabiner](https://karabiner-elements.pqrs.org/). For whatever reason this did not work (key remapping is a dark art) and I considered giving up, but decided to try some alternatives first. (Side note: it looks like there is a [modification somebody else made](https://ke-complex-modifications.pqrs.org/#swap_alt_cmd_in_term))

Somebody mentioned a program called [cmd-key-happy](http://github.com/aim-stuff/cmd-key-happy) and it looked like it'd sort my use case. It also hadn't been updated since 2017, and the last MacOS version it referenced was Mavericks.

I installed it and it didn't work, unsurprisingly. I read the `INSTALL` note about having to enable accessiblity support, and considered that might be the issue; unfortunately there was no listing of the program in "Security & Privacy" > Privacy > Accessibility to check the box for. But what if I dragged and dropped the executable into the "Allow the apps below to control your computer." pane?

I opened Finder with `open /usr/local/bin/` and found the `cmd-key-happy` executable, and sure enough, I could drop it into the accessibility window.

<img alt="I enabled the cmd-key-happy program in the Accessibility controls" src="/img/cmd-key-happy-restart-setting.png">

Then, when I restarted it with `./cmd-key-happy-restart.sh` it worked :)
