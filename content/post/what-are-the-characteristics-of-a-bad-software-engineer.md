+++
categories = ["开发", "dev", "English", "中文"]
date = "2016-05-12T22:47:39+08:00"
tags = ["翻译"]
title = "Quora：烂程序猿的特征都有啥？"

+++

What are the characteristics of a bad software engineer?
------

> [Originally answered by Nachiket Naik, software developer, artist, reader, writer, thinker and compassionate human being](https://www.quora.com/What-are-the-characteristics-of-a-bad-software-engineer/answer/Nachiket-Naik?srid=3Eg3)

据我观察，烂软件工程师有有以下几种特征：

In my experience, these are some characteristics of bad software engineers:

壹 **Stack Overflow 的搬运机器人**：这类人一发现有报错，就顺手 Google 一下，接着把他们查到的第一个方法拿来试。问题不在于从 stack Overflow 搬运，私以为 SOF 有比任何参考手册和文档都更多的解决方案内容。所以别误会，SOF 即便不是最好也是超好的资源。问题在于不理解这些方案的后果，不清楚应用的适用场景，不确定其是否真正能对应手头的问题，的情况下，就机械地照搬。我看过不止一次，比起近在眼前的代码和系统，人们反而更愿意去相信网络论坛的说法。

1) **The Stack Overflow bot**: This person ran into an error, did a quick Google search and applied the first solution they found. The problem here is not that of copying from Stack Overflow. I think there are more solutions on Stack Overflow than any reference guide or manual. Don't get me wrong, it's a wonderful resource, if not the best. The problem is the robotic application of it without understanding the consequences. The problem is the application of it without fully understanding the context of it and whether it really applies to the current problem at hand. More often than not, I have seen people believe more of what they see on online forums than the code/system in front of them.

贰 **“老子又不是测试人员”**：我不用测试我的代码，那是测试人员的工作。即便在这个敏捷开发的方法论已经无比成熟的年代，我也没觉得吃这种态度的人比之前少了多少。人们依旧对测试十分懈怠。一部分源于他们对部署测试环境不感兴趣；另一方面，他们缺乏测试相关的系统知识。（还部分源于开发者社群对测试人员心照不宣的轻视）

2) **The I-am-not-a-tester**: I don't need to test the code; that is the job of the testers. I don't think that even in this age of mature Agile methodologies, this attitude has waned. There is still an inertia against testing their code. Part of it comes from lacking the interest to set up a testing environment and partly from lack of coherent knowledge of testing. (Is it also partly due to an unspoken stigma against testers in the developer community.)

叁 **“我讨厌文档”**：一些人认为代码文档必须写得很诗意，而他们写不出这种东西，由此推出写文档肯定不是他们的工作。我觉得这是开发长效稳定代码的最大威胁！好的软件不是提供成千上万好功能的软件。好软件是只包含少许功能，却能被众人一直使用，还能被成百上千人查阅、更新、修改。这种对技术交流和精准细致的文档毫不关心的程序猿将成为公司成功的重大阻碍。

3) **The I-hate-documentation**: Some people believe that code documentation must be poetic and hence they lack the skill to do it, ergo not their job. In my opinion, these are the #1 foes of sustainable software. Good software is not software that provides a million cool features. Good software is one that has a few good features that are used consistently by many people and read/updated/modified by a thousand. This brand of developers who believes less in technical communication and precise and detailed documentation is the greatest weed to a company's success.

肆 **丑陋**：我的代码能用，然而：

* 我有表意不明的变量名：x, flag, str, arr 等等
* 我写的大多数代码都包含在一个冗长的方法中
* 没有缩进（译注：还有乱缩进）
* 没有一以贯之的编码规范、风格
* 全局变量到处瞎鸡巴放

这是我个人最反感的一点。这并不代表代码很差，它很可能还是一段颇具巧思的好代码。即便锦帽貂裘，若是丢进了垃圾堆里，也没人找得到它，没人愿意清理它，跟别提佩戴和使用了。

4) **The ugly**: My code works, but:

* I have variables named x, flag, str, arr, etc.
* Most of what I write is in one giant method.
* There is no indentation.
* No consistent coding convention or style.
* Global variables spewed all over the place, etc.

This is the most annoying thing for me personally. It's not the issue that the code is bad. It could potentially be the greatest piece of code written. But if a diamond necklace is buried in the debris of the Titanic, nobody will find it, and nobody will want to clean it, wear it, use it.

伍 **短期投资者**：他写代码。他部署代码。他走了。他不研究业务逻辑，他不在乎学到东西题。给他一段代码，他会连夜搞它一整晚，第二天他回给你的是一个已经修好的的软件。除此之外的东西就一概欠奉了。有时候，开发者要有点自私心，人应该不仅仅在乎交活日期，也要注重经手这个项目你能学到什么。

5) **The short-term investor**: He codes. He deploys. He moves on. No attempt to learn the problem. No interest in the domain. Just give this guy a piece of code, he will slog on it overnight and hand it over. You got a fix/working software. Nothing more achieved from it. Sometimes, it's important that you have certain selfishness in the developer, one who not only cares about the deadline, but also cares about what he/she got to learn from it.

陸 **异议人士**：“这肯定不是老子干的”，“这一团糟”，“反正不是我的问题”，“这跟我的修改无关，是远处的XXX的错”，“我讨厌这个（每天 BB 这句话 10 次)”，“我没法修这东西，谁搞坏的谁来修”
呵呵，写这个代码的已经离职了，你什么时候走？

6) **The protester**: "I didn't do this". "This looks bad". "Not my problem". "This isn't related really to my fix, but someone way over there made a mistake". "I hate this (loop this sentence 10 times a day)", "I can't fix this, get the person who made this code to fix it".
The person who coded that mistake has moved on, when will you?

柒 **独裁者**：“My way or the highway”（要么听我的要么滚）是他们的信条。他们对人不对事，这是场他们的解决方案与你的解决方案之间的对决。我想这里面肯定有不少争吵。他们会回来指责你的代码，即使你的代码运行良好，测试完善，看起来完全没问题，他们也会很不爽。这些人是工作效率的一大制约，并且在压力来临的时候，他们也是最先崩溃的，最先跳起来指指点点。即便他们是很有经验很好的开发者，他们对团队也是不利的。

7) **The dictator**: My way or the highway is their motto. It's their "ideas" vs "your ideas", not "project ideas". It's their solution vs your solution. I bet there will be an argument for sure. Somehow they will keep coming back to a part of code that you implemented. It somehow discomforts them even if it works, tests, and looks perfectly fine. This person is a big bottleneck to productivity and will be the first person to crumble under pressure and start pointing fingers. This person is not good for the team, however experienced/good a developer he may be.

捌 **怕事鬼**：当某位 JAVA 程序猿听到他要被迫写一段 Python 代码时，傻掉了。当某位程序猿发现需要改注册表时，慌掉了。当程序猿发现必须往数据库里添些东西的时候，吓哭了。这些人会竭尽所能地避免走出他们的舒适区。他们对触碰系统的某些部分有着非同寻常的迷信忌讳。见得多了，我就明白了，这些现象对新手开发者而言还挺常见的。好的程序猿则更倾向于或快或慢地探索舒适区之外世界。

8) **The overcautious**: The Java developer who just froze when he learned that he would have to write a Python script. The developer who panicked on learning that something in the registry needs changing. The developer who cringes at having to input things in the database. These people will do anything to avoid getting out of their comfort zone. They have weird superstitions related to having to touch certain parts of the system. I have learned, from personal experience, that this phenomenon is common with new developers. Good developers show a tendency to slowly/swiftly move out of their comfort zone in exploration.

玖 **一芥莽夫**：忘了备份，快照，同时开好多代码的工作目录，忘记登出系统，把生产环境的代码乱放等等。这些是菜鸟的常见错误，等他们慢慢成长，会变得越来越专业的。

9) **The careless**: Forgets to take a backup, snapshots, has multiple working directories of code, leaves system out, prints in production code, etc. Again, this is a newbie tendency and gets better with more professional exposure.

拾 **懒惰的默认式程序猿？**他们骄傲于能够快速找到窍门让系统恢复正常。他们总能给目测无比复杂的问题，找到魔法一般的解决办法。我的经验是，这些花招十个里有九个是银样蜡枪头，就表面功夫而已。这些差劲的花招早晚有一天会坏掉，而且被迫修复他们的代价会比立刻认认真真地修好它所花的时间更高。

10) **The lazy pseudo-hacker**: They pride themselves at being able to trick the system into working. They find magical solutions to seemingly complex problems. My experience says that 9 out of 10 times, it's just a facade. The hack is bad and will crash sooner or later and will cost much more than having to deal with it, with extra time right now.

补充：留言，点赞，开新楼之类的废话，不翻译了。
EDIT: Please drop in comments. Maybe we could start a new follow-up question as to how a managers/peers/colleagues could handle these cases because almost all of them can be helped to become better. A design pattern of sorts for fixing programmer smells. :-)

<small>Updated Dec 5, 2014</small>

> 后记： 我觉得这个篇文章的作者的确点出了几个点，不过就我个人感觉这完全是一种基于过往经验的偏见。举例而言，Linus 就是独裁者；而好的程序猿对代码都有洁癖；天天做恶心的代码，没有人不抱怨的。情商的养育是一个系统的话题，情商不行，干什么都不行，也不光是程序猿了啊。扯多了就扯远了。总之这是篇有水分的文章，尽信书不如无书。
另外，程序猿一言不合，拔键盘相向我觉得也挺好理解的吧。不说了，我和同事去医院缝针了。Yes, My patch wins!
好吧，我就是 dictator 型的，my way or no way，我的必然是最简单最好懂也最好维护的方案，不过我一般不强迫他们，如果 Design pattern 的基础不牢固，有些抽象方法你解释给他们，他们也听不懂。