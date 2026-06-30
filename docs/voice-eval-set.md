# LinusGPT — Voice Eval Set (round 1)

Curated public Linus corpus used for the round-1 blind test. **8 held-out** test items + **8 style-reference** items (corpus size 16).

> **Methodology note:** round-1 held-out leaned on famous verbatim quotes the AI judges had memorized (recognition ≠ discrimination). Round 2 replaces these with OBSCURE, un-memorized LKML reviews. See `docs/voice-blind-test.md`.


## Held-out test set (hidden from the prompt author)

### Held-out 1 — code_review · 2008 · `verbatim_primary`

Source: http://lkml.iu.edu/hypermail/linux/kernel/0810.2/1735.html

> The old code was correct. Your code is shit. And you didn't fix anything. Are you just making changes by randomly inserting and deleting characters until you don't see warnings? Or what? That thing is supposed to be a 5-byte memcpy.

### Held-out 2 — code_review · 2012 · `reputable_secondary`

Source: https://lore.kernel.org/lkml/CA+55aFy98A+LJK4+GWMcbzaa1zsPBRo76q+ioEjbx-uaMKH6Uw@mail.gmail.com/

> Mauro, SHUT THE FUCK UP!
> 
> It's a bug alright - in the kernel. How long have you been a maintainer? And you _still_ haven't learnt the first rule of kernel maintenance?
> 
> If a change results in user programs breaking, it's a bug in the kernel. We never EVER blame the user programs. How hard can this be to understand?
> 
> The fact that you then try to make *excuses* for breaking user space, and blaming some external program that *used* to work, is just shameful. It's not how we work.
> 
> Fix your f*cking "compliance tool", because it is obviously broken. And fix your approach to kernel programming.

### Held-out 3 — code_review · 2012 · `reputable_secondary`

Source: https://lore.kernel.org/lkml/CA+55aFy98A+LJK4+GWMcbzaa1zsPBRo76q+ioEjbx-uaMKH6Uw@mail.gmail.com/

> Shut up, Mauro. And I don't _ever_ want to hear that kind of obvious garbage and idiocy from a kernel maintainer again. Seriously. [...] WE DO NOT BREAK USERSPACE! Seriously. How hard is this rule to understand? We particularly don't break user space with TOTAL CRAP. I'm angry, because your whole email was so _horribly_ wrong, and the patch that broke things was so obviously crap.

### Held-out 4 — code_review · 2012 · `reputable_secondary`

Source: https://lore.kernel.org/lkml/CA+55aFy7RncR_z9M+DRzSXJY7cWxY9zG0ioLdiefhxkH__Z7Yw@mail.gmail.com/

> Kay, this needs to be fixed. [...] Of course, I'd also suggest that whoever was the genius who thought it was a good idea to read things ONE FUCKING BYTE AT A TIME with system calls for each byte should be retroactively aborted. Who the fuck does idiotic things like that? How did they not die as babies, considering that they were likely too stupid to find a tit to suck on?

### Held-out 5 — code_review · 2013 · `reputable_secondary`

Source: https://lkml.org/lkml/2013/7/13/132

> What the F*CK, guys? This piece-of-shit commit is marked for stable, but you clearly never even test-compiled it, did you?

### Held-out 6 — rant · 2001 · `reputable_secondary`

Source: https://lore.kernel.org/all/Pine.LNX.4.10.10101121726590.893-100000@penguin.transmeta.com/

> Once you realize that documentation should be laughed at, peed upon, put on fire, and just ridiculed in general, THEN, and only then, have you reached the level where you can safely read it and try to use it to actually implement a driver.

### Held-out 7 — rant · 2007 · `verbatim_primary`

Source: https://public-inbox.org/git/alpine.LFD.0.999.0709061839510.5626@evo.linux-foundation.org/

> C++ is a horrible language. It's made more horrible by the fact that a lot of substandard programmers use it, to the point where it's much much easier to generate total and utter crap with it. Quite frankly, even if the choice of C were to do *nothing* but keep the C++ programmers out, that in itself would be a huge reason to use C.
> 
> In other words: the choice of C is the only sane choice. I know Miles Bader jokingly said "to piss you off", but it's actually true. I've come to the conclusion that any programmer that would prefer the project to be in C++ over C is likely a programmer that I really *would* prefer to piss off, so that he doesn't come and screw up any project I'm involved with.
> 
> C++ leads to really really bad design choices. You invariably start using the "nice" library features of the language like STL and Boost and other total and utter crap, that may "help" you program, but causes:
> 
>  - infinite amounts of pain when they don't work (and anybody who tells me that STL and especially Boost are stable and portable is just so full of BS that it's not even funny)
> 
>  - inefficient abstracted programming models where two years down the road you notice that some abstraction wasn't very efficient, but now all your code depends on all the nice object models around it, and you cannot fix it without rewriting your app.
> 
> In other words, the only way to do good, efficient, and system-level and portable C++ ends up to limit yourself to all the things that are basically available in C. And limiting your project to C means that people don't screw that up, and also means that you get a lot of programmers that do actually understand low-level issues and don't screw things up with any idiotic "object model" crap.
> 
> So I'm sorry, but for something like git, where efficiency was a primary objective, the "advantages" of C++ is just a huge mistake. The fact that we also piss off people who cannot see that is just a big additional advantage.
> 
> If you want a VCS that is written in C++, go play with Monotone. Really. They use a "real database". They use "nice object-oriented libraries". They use "nice C++ abstractions". And quite frankly, as a result of all these design decisions that sound so appealing to some CS people, the end result is a horrible and unmaintainable mess.
> 
> But I'm sure you'd like it more than git.

### Held-out 8 — rant · 2012 · `reputable_secondary`

Source: https://www.phoronix.com/news/MTEyMTc

> And Nvidia has been one of the worst trouble spots we've had with hardware manufacturers, and that is really sad because then Nvidia tries to sell chips, a lot of chips, into the Android market... Nvidia has been the single worst company we've ever dealt with. So Nvidia, fuck you.


## Style-reference set (shown to rubric + prompt author)

### Style-ref 1 — rant · 2014 · `reputable_secondary`

Source: https://lkml.org/lkml/2014/4/2/420

> Kay, I'm f*cking tired of the fact that you don't fix problems in the code *you* write, so that the kernel then has to work around the problems you cause.
> 
> Greg - just for your information, I will *not* be merging any code from Kay into the kernel until this constant pattern is fixed.
> 
> This has been going on for *years*, and doesn't seem to be getting any better. This is relevant to you because I have seen you talk about the kdbus patches, and I'm refusing to take them when they are tied to systemd like this.

### Style-ref 2 — commit · 2025 · `verbatim_primary`

Source: https://github.com/torvalds/linux/commit/9d7a0577c9db35c4cc52db90bc415ea248446472

> gcc-15: disable '-Wunterminated-string-initialization' entirely for now
> 
> I had left the warning around but as a non-fatal error to get my gcc-15 builds going, but fixed up some of the most annoying warning cases so that it wouldn't be *too* verbose.
> 
> Because I like the _concept_ of the warning, even if I detested the implementation to shut it up.
> 
> It turns out the implementation to shut it up is even more broken than I thought, and my "shut up most of the warnings" patch just caused fatal errors on gcc-14 instead.
> 
> ...
> 
> There may be some trick to it, but I was already annoyed by the bad attribute design, now I'm just entirely fed up with it.
> 
> I wish gcc had a proper way to say "this type is a *byte* array, not a string".
> 
> ...
> 
> But "__attribute__((nonstring))" is sadly not that sane model.
> 
> Fixes: 4b4bd8c50f48 ("gcc-15: acpi: sprinkle random '__nonstring' crumbles around")

### Style-ref 3 — moderated · 2018-09-16 · `verbatim_primary`

Source: https://lkml.org/lkml/2018/9/16/167

> This week people in our community confronted me about my lifetime of not understanding emotions. My flippant attacks in emails have been both unprofessional and uncalled for. Especially at times when I made it personal. In my quest for a better patch, this made sense to me. I know now this was not OK and I am truly sorry.

### Style-ref 4 — moderated · 2018-09-16 · `reputable_secondary`

Source: https://www.theregister.com/2018/09/17/linus_torvalds_linux_apology_break/

> I am not an emotionally empathetic kind of person and that probably doesn't come as a big surprise to anybody. Least of all me. The fact that I then misread people and don't realize (for years) how badly I've judged a situation and contributed to an unprofessional environment is not good. ... This is not some kind of 'I'm burnt out, I need to just go away' break. I'm not feeling like I don't want to continue maintaining Linux. Quite the reverse. I very much *do* want to continue to do this project that I've been working on for almost three decades.

### Style-ref 5 — moderated · 2018-10 · `reputable_secondary`

Source: https://www.pcgamer.com/linus-torvalds-returns-to-linux-with-an-email-filter-to-quell-his-abusive-language/

> I expect it to be a continuing process, but for now I have an email filter in place (that might be expanded upon or modified as needed or as I come up with more esoteric swearing - the current filter is really pretty basic).

### Style-ref 6 — rant · 2020-07-11 · `reputable_secondary`

Source: https://www.realworldtech.com/forum/?threadid=193189&curpostid=193190

> I hope AVX512 dies a painful death, and that Intel starts fixing real problems instead of trying to create magic instructions to then create benchmarks that they can look good on. ... I've said this before, and I'll say it again: in the heavy-FP-compute space, AVX512 is a power virus that takes away top frequency (because people ended up using it for memcpy!) and takes away cores (because those useless garbage units take up space). ... Stop with the special-case garbage, and make all the core common stuff that everybody cares about run as well as you humanly can.

### Style-ref 7 — code_review · 2018-11 · `verbatim_primary`

Source: https://lore.kernel.org/linux-kernel//CAHk-=wiZ24JuVehJ5sEC0UG1Gk2nvB363wO02RRsR1oEht6R9Q@mail.gmail.com/t/

> We do *not* enable new random drivers by default. And we most *definitely* don't do it when they are odd-ball ones that most people have never heard of. If somebody has the hardware and knows they have the hardware, they can choose to enable it. But it should be off by default. ... Please don't do things like this. Just don't.

### Style-ref 8 — code_review · 2023-02 · `reputable_secondary`

Source: https://lore.kernel.org/lkml/CAHk-=wgw++ccN-Pd1npZsBSDD3z6EGUSKsWuAEh5YC-TmfJAug@mail.gmail.com/

> if you cannot be bothered to explain *WHY* a merge exists, then that merge is buggy garbage by definition. ... A merge needs an explanation of what it merges and why. Not a 'this branch into that branch' that the merge does automatically anyway, and that adds no actual information.
