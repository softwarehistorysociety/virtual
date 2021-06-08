# "A brief history of Dell UNIX"

*07-06-2021 07:11* 

> [update December 2020: Dell Unix on 86Box “Today let me present Dell Unix more properly, with 1024×768, 256 colors video and proper networking using emulated VGA and NIC.” update  March…
\[update December 2020: [Dell Unix on 86Box](https://virtuallyfun.com/wordpress/2020/12/01/dell-unix-on-86box/) “Today let me present Dell Unix more properly, with 1024×768, 256 colors video and proper networking using emulated VGA and NIC.”  
update  March 2012: [Antoni Sawicki](http://virtuallyfun.superglobalmegacorp.com/?p=1878) has Dell SVR4 running  
under Qemu/Bochs, and subsequently reports that he has  
Dell Unix “working correctly”  under VirtualBox. CHS\]

“Dell UNIX? I didn’t know there was such a thing.”

A couple of weeks ago I had my new [XO](http://laptop.org/) with me for breakfast at a nearby [bakery café](http://web.archive.org/web/20140308210557/http://www.kneadedpleasures.com/). Other patrons were drawn to seeing an XO for the first time, including a Linux person from Dell. I mentioned Dell UNIX and we talked a little about the people who had worked on Dell UNIX. He expressed surprise that mention of Dell UNIX evokes the above quote so often and pointed out that [Emacs](http://www.gnu.org/software/emacs/) source still has #ifdef for Dell UNIX.

Quick Googling doesn’t reveal useful history of Dell UNIX, so here’s my version, a summary of the three major development releases.

***Dell UNIX System V Release 1.x*** (1988-1989)

In 1988, [Glenn Henry](http://www.youtube.com/watch?v=kAonOmb8l3o) joined Dell as VP of R&D with the mission of building a much larger team and advanced products. That team embarked on the ill-fated “[Olympic Project](https://web.archive.org/web/20160418183450/http://www.achievement.org/autodoc/page/del0int-6),” intended to span “desktop, workstation and server markets, with single and dual processors and many different operating systems”, in Michael’s words.

For some of the Olympic processor configurations, *e.g.*, multiprocessor and/or [i860](http://en.wikipedia.org/wiki/Intel_i860), some form of UNIX was the only realistic operating system. So Glenn started a UNIX development project, partly with some sharp “old-timers” (*e.g.*, Craig Jones, Tony Overfield, and James Van Artsdalen), partly with other ex-IBMers (*e.g.*, Dewey Coffman, Ken Jeffries, Tom Lang, John Lay, and Kenneth Smith), and partly with other new folks (Randy Howard and Todd Nix).

[![Dell UNIX tote bag](https://technologists.com/images/tn19890227DellUnixToteBag.jpg)](https://technologists.com/images/sm19890227DellUnixToteBag.jpg)The first release was based on System V Release 3.2 as available from Interactive Systems Corp. However, it was hardly the standard ISC product. Most notably, it included “DOS Merge” from ISC rival Locus Computing instead of ISC’s VP/ix DOS compatibility subsystem. Dell SVR3.2 also included the Motif window-manager, X Windows support for higher performance graphics cards and emphasis on Xenix compatibility. When Dell UNIX was first publicly demonstrated at the 1989 UniForum Conference, the most prominent handouts were tote bags touting [Xenix](https://technologists.com/images/sm19890227DellUnixToteBag.jpg) compatibility.

All of that was while I was still working on AIX. In April I asked Glenn and Michael to hire me and I became director of product planning for Olympic. With my encouragement, Tom Lang became aggressive about recruiting. When Tom suggested that Kendall Witte might be interested in coming over from IBM, I was pleasantly surprised. I had high regard for Ken from his AIX “orange book” efforts and knew that he’d had prior PC UNIX experience with the ISC PC/ix project for IBM. I’m not exactly sure when they joined, but some of the other developers to come on board were Richard Amberg, Donn Baumgartner, Jeremy Chatfield, Alan Davis, George Durden, Dave McCracken and Ron McDowell.

Dell UNIX System V Release 1.1 was introduced November 1, 1989. Though the Olympic project was terminated that winter, Dell UNIX survived.

***[DELL Station](https://technologists.com/sauer/DellStation.txt)*** (1990)

Microsoft Windows had still not quite yet become dominant. Mac OS was the graphical user interface of choice in the personal computer world. Dell seemed to be the leader in X Windows for the PC, and Dell Station attempted to extend that leadership. “Dell has added IXI’s X.desktop, that provides the user with a Macintosh-like screen with icons that represent applications or functions. … The DELL Station includes a comprehensive suite of integrated office applications from Uniplex.  Uniplex X Windows applications include word processing, a spreadsheet, the Informix SQL (structured query language) relational database, advanced business graphics, electronic mail and more.”

The real excitement in the UNIX development group was not Dell Station, but the first release of Dell’s SVR4, which was [announced](https://technologists.com/sauer/DellSVR4.txt) on Halloween 1990.

***Dell System V Release 4*** (1990-1993)

[![Dell SVR4 Box](https://technologists.com/images/tn1992DellSVR42.2Box.jpg)](https://technologists.com/images/sm1992DellSVR42.2Box.jpg)Dell SVR4 finally seemed like real UNIX on a PC. We were justifiably proud of the quality and comprehensiveness, especially considering that our team was so much smaller than those of our perceived competitors at ISC, SCO and Sun(!). The reviewers were impressed. Reportedly, Dell SVR4 was chosen by Intel as their reference implementation in their test labs, chosen by Oracle as their reference Intel UNIX implementation, and used by AT&T USL for in house projects requiring high reliability, in preference to their own ports of SVR4.0. (One count showed Dell had resolved about 1800 problems in the AT&T source.) I was astonished one morning in the winter of 1991-92 when Ed Zander, at the time president of SunSoft, and three other SunSoft executives arrived at my office, requesting Dell help with their plans to put Solaris on X86.

Besides all of the features enumerated in the press release, we were pioneering in bundling all sorts of “geeky” free software. Some time before, I’d bought a couple of binders of man(1) pages, etc., of free software. I’d wanted to include much of that software in AIX, but couldn’t. “Open source” had not yet been coined, but these were prototypical examples of what would be called “open source”, programs like elm, Emacs, gcc, mh, [NNTP](http://en.wikipedia.org/wiki/Network_News_Transfer_Protocol) readers and servers, PERL 4, TeX,  … that “everyone” wanted but had to fetch/build/install/test on other versions of UNIX. Today, it is expected that this kind of software is part of a complete Linux|UNIX system, but I think we were the first to adopt this attitude in a packaged release.

Perhaps the most important Dell addition was auto-configuration of device drivers. This was at least two years before Intel & Microsoft devised “[Plug and Play ISA](http://download.microsoft.com/download/1/6/1/161ba512-40e2-4cc9-843a-923143f3456c/PNPISA.rtf)” for Windows *et al*. Reportedly, the auto-configuration feature accounted primarily for approximately 90% reduction in calls for support in the first 90 days of Dell SVR4 use, versus Dell UNIX based on SVR3.

Kendall Witte proved his “guru” mettle as the technical lead of the first three releases. I cannot overstate the importance of Ken’s contributions to the entire project and related hardware projects. Jeremy Chatfield was also heroic as the first line manager and tireless negotiator within and outside of Dell. We were able to get [Thomas Roell](http://en.wikipedia.org/wiki/XFree86) to join us for the summer of ’91 and contribute his prodigious X Windows expertise.

Unfortunately, there seemed to be no way for Dell to profit financially from our UNIX. The business rationale for Dell UNIX was to sell Dell hardware. But the majority of the copies of Dell UNIX ended up running on other vendors’ machines. Not only was Dell not getting the planned hardware revenue, the support costs for non-Dell hardware were unreasonably high. The biggest complaint from our advocates outside of Dell was that the purchase price was too high, yet our royalty costs, not to mention development and support costs, made it very hard to make a profit at what we were charging, or consider a lower price.

The UNIX project was divisive in development, marketing and sales. The advocates were certain Dell UNIX was a great product. Even the detractors often acknowledged the technical strengths. But marketing and selling a more recognized UNIX, particularly SCO UNIX, seemed likely to cost much less in development, marketing, sales and support, and to better reach markets, for example, multi-user “dumb terminal” environments, where SCO was preeminent.

Compaq’s June 1992 product announcements and price cuts were singular in internal Dell transformation that summer and the end of Dell UNIX, in my opinion. Key members of the UNIX team, most notably Kendall Witte, moved to other departments.

[![Dell 2.2 distribution tape](https://technologists.com/images/tn1992DellSVR42.2QIC.jpg)](https://technologists.com/images/sm1992DellSVR42.2QIC.jpg)Dell SVR4 Issue 2.2 came out in 1992 as the crowning achievement of a great development effort, but the writing was on the wall. 2.2 would be the last major release. Jeremy left Dell. Others, notably Selina Johnson and Stan McHann, admirably provided management support internally and externally, which was no fun, especially after the public end of life announcements.

I left Dell in the Fall of 1993. At the end of that year, the final support tape, Issue 2.2.1, was released to customers with support contracts.

I asked Jeremy to read a draft of this article. With his usual insight and thoroughness, he pointed out all sorts of things that I had omitted, some of which I never knew before, and I have revised accordingly.

I can still boot Issue 2.2 on a 1991 Dell 450 DE/2 DGX and referred to files on that machine to write some of this. Last I heard from Ken, he was still working at Dell, still running Dell UNIX, and wishing it had DHCP support.

This entry was posted on Thursday, January 10th, 2008 at 9:09 pm and is filed under [operating systems](https://notes.technologists.com/notes/category/operating-systems/). You can follow any responses to this entry through the [RSS 2.0](https://notes.technologists.com/notes/2008/01/10/a-brief-history-of-dell-unix/feed/) feed. Both comments and pings are currently closed.
***

==**8956**== Words

- **[Technologists Notes » Blog Archive » A brief history of Dell UNIX](https://technologists.com/notes/2008/01/10/a-brief-history-of-dell-unix/)**
