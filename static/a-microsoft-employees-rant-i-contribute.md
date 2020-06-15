---
title: 'A Microsoft Employees Rant: “I Contribute to the Windows Kernel. We Are Slower Than Other Operating Systems. Here Is Why.”'
date: 2013-05-12T13:56:00.001-05:00
draft: false
aliases: [ "/2013/05/a-microsoft-employees-rant-i-contribute.html" ]
---

  

![Image result for windows logo png](https://upload.wikimedia.org/wikipedia/commons/c/c7/Windows_logo_-_2012.png)

  

I was having a discussion in a forum with Marc Bevand about how windows is still slow despite of the “fast” windows 8.

  

And out of nowhere an anonymous Microsoft developer who contributes to the Windows NT kernel wrote a fantastic and honest response acknowledging this problem and explaining its cause.

  

The post has since been deleted.

But I am re-posting it since it’s too insightful.

  

  

_PS: The anonymous poster himself deleted his post as he thought it was too cruel and did not help make his point, which is about the social dynamics of spontaneous contribution. However he let me know he does not mind the re-post at the condition I redact the SHA1 hash info, which I did_

  

  

"I’m a developer in Windows and contribute to the NT kernel. (Proof: the SHA1 hash of revision #102 of \[Edit: filename redacted\] is \[Edit: hash redacted\].) I’m posting through Tor for obvious reasons.

Windows is indeed slower than other operating systems in many scenarios, and the gap is worsening. The cause of the problem is social. There’s almost none of the improvement for its own sake, for the sake of glory, that you see in the Linux world.

Granted, occasionally one sees naive people try to make things better. These people almost always fail. We can and do improve performance for specific scenarios that people with the ability to allocate resources believe impact business goals, but this work is Sisyphean. There’s no formal or informal program of systemic performance improvement. We started caring about security because pre-SP3 Windows XP was an existential threat to the business. Our low performance is not an existential threat to the business.

See, component owners are generally openly hostile to outside patches: if you’re a dev, accepting an outside patch makes your lead angry (due to the need to maintain this patch and to justify in in shiproom the unplanned design change), makes test angry (because test is on the hook for making sure the change doesn’t break anything, and you just made work for them), and PM is angry (due to the schedule implications of code churn). There’s just no incentive to accept changes from outside your own team. You can always find a reason to say “no”, and you have very little incentive to say “yes”.

There’s also little incentive to create changes in the first place. On linux-kernel, if you improve the performance of directory traversal by a consistent 5%, you’re praised and thanked. Here, if you do that and you’re not on the object manager team, then even if you do get your code past the Ob owners and into the tree, your own management doesn’t care. Yes, making a massive improvement will get you noticed by senior people and could be a boon for your career, but the improvement has to be very large to attract that kind of attention. Incremental improvements just annoy people and are, at best, neutral for your career. If you’re unlucky and you tell your lead about how you improved performance of some other component on the system, he’ll just ask you whether you can accelerate your bug glide.

Is it any wonder that people stop trying to do unplanned work after a little while?

Another reason for the quality gap is that that we’ve been having trouble keeping talented people. Google and other large Seattle-area companies keep poaching our best, most experienced developers, and we hire youths straight from college to replace them. You find SDEs and SDE IIs maintaining hugely import systems. These developers mean well and are usually adequately intelligent, but they don’t understand why certain decisions were made, don’t have a thorough understanding of the intricate details of how their systems work, and most importantly, don’t want to change anything that already works.

These junior developers also have a tendency to make improvements to the system by implementing brand-new features instead of improving old ones. Look at recent Microsoft releases: we don’t fix old features, but create new ones. New features help much more at review time than improvements to old ones.

(That’s literally the explanation for PowerShell. Many of us wanted to improve cmd.exe, but couldn’t.)

More examples:

  

*   We can’t touch named pipes. Let’s add %INTERNAL\_NOTIFICATION\_SYSTEM%! And let’s make it inconsistent with virtually every other named NT primitive. 
*   We can’t expose %INTERNAL\_NOTIFICATION\_SYSTEM% to the rest of the world because we don’t want to fill out paperwork and we’re not losing sales because we only have 1990s-era Win32 APIs available publicly. 
*   We can’t touch DCOM. So we create another %C#\_REMOTING\_FLAVOR\_OF\_THE\_WEEK%! 
*   XNA. Need I say more? 
*   Why would anyone need an archive format that supports files larger than 2GB? 
*   Let’s support symbolic links, but make sure that nobody can use them so we don’t get blamed for security vulnerabilities (Great! Now we get to look sage and responsible!) 
*   We can’t touch Source Depot, so let’s hack together SDX! 
*   We can’t touch SDX, so let’s pretend for four releases that we’re moving to TFS while not actually changing anything! 
*   Oh god, the NTFS code is a purple opium-fueled Victorian horror novel that uses global recursive locks and SEH for flow control. Let’s write ReFs instead. (And hey, let’s start by copying and pasting the NTFS source code and removing half the features! Then let’s add checksums, because checksums are cool, right, and now with checksums we’re just as good as ZFS? Right? And who needs quotas anyway?) 
*   We just can’t be fucked to implement C11 support, and variadic templates were just too hard to implement in a year. (But ohmygosh we turned “^” into a reference-counted pointer operator. Oh, and what’s a reference cycle?) 

  

Look: Microsoft still has some old-fashioned hardcore talented developers who can code circles around brogrammers down in the valley. These people have a keen appreciation of the complexities of operating system development and an eye for good, clean design. The NT kernel is still much better than Linux in some ways — you guys be trippin’ with your over-commit-by-default MM nonsense — but our good people keep retiring or moving to other large technology companies, and there are few new people achieving the level of technical virtuosity needed to replace the people who leave. We fill headcount with nine-to-five-with-kids types, desperate-to-please H1Bs, and Google rejects. We occasionally get good people anyway, as if by mistake, but not enough. Is it any wonder we’re falling behind? The rot has already set in."