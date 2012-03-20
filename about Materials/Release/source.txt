"About Inform 7" by "Bart Massey"

[Released under the Creative Commons Attribution 3.0 United States (CC BY 3.0) license. See http://creativecommons.org/licenses/by/3.0/us/ for license details.]

Volume - Setup

Release along with an interpreter, cover art, the source text and the library card.

After reading a command when the player's command matches the regular expression "^\p|^\*" (this is the ignore beta-comments rule): say "(noted)"; reject the player's command.

To say debug: (- #ifdef DEBUG; -). To say end debug: (- #endif; -).

Use American dialect.

Rule for deciding whether all includes scenery: it does not.

The story headline is "A Metareflective Talk Environment".

Book - Out Of World

Helping is an action out of world. Carry out helping: say "For this help, say 'help'. For basic information, say 'version'. For acknowledgments, say 'acks'. For other help, I'm afraid you're out of luck." Understand "help" as helping.

Acknowledging is an action out of world. Carry out acknowledging: say "Sources for this work include the Inform 7 documentation, [italic type]Inform 7 for Programmers,[roman type] the [italic type]Inform 7 Handbook,[roman type] Aaron Reed's book [italic type]Creating Interactive Fiction with Inform 7[roman type] and a whole bunch of other stuff scattered around the web.[paragraph break]My brother, Byron Massey (20 September 1967 – 11 October 2010), was the great player of games in our family, and I wish I could show him what I'm doing. I think he might think it was cool." Understand "acknowledgements" or "acknowledgments" or "acks" as acknowledging.

When play begins, say "Copyright (c) 2012 Bart Massey[paragraph break]This text 'adventure' is both the 'slides' for my talk and a couple of demo apps. One demo app, a Nim player, is based on a graphical Nim player I wrote for the 128K Macintosh around 1982. It plays perfectly, but only plays as second player, so it is beatable. The other demo app is a more traditional text adventure puzzle.[paragraph break]The briefing itself uses a not-yet-complete 'books' extension I'm working on that provides fairly elaborate book behavior. To see the talk slides, say 'read book' and keep saying it until you're done. Say 'help' for further meta-information."

The maximum score is 2.

Book - The Briefing Room

There is a room called The Briefing Room. "This wood-paneled study is adequately if indirectly lit by wall-mounted lamps along the walls. In the center of the room is a table, and on the table are several books. Open doorframes lead west and south. A restroom door lies to the east."

The briefing table is fixed in place scenery in The Briefing Room. "This sturdy polished table of light mahogany has plenty of space to spread out."

Volume - Books

Book - Reading

[XXX: This book is deliberately not book-specific. It is arguable that this should be split out into a separate extension and eventually rolled into the Standard Rules in some form. Having "read" be a synonym for "examine" is bizarre IMHO.]

Reading is an action applying to one visible thing and requiring light.

Every thing has a text called the read text. The read text is usually "".

Understand "read [thing]" as reading.

To say error (the thing read - a thing) has no read text (this is the say no read text error rule): say "[The thing read] has no text to read."

Check an actor reading a thing (called the thing read) (this is the check reading a thing rule): if the read text of the thing read is empty, instead say error the thing read has no read text.

To say the read text of (the thing read - a thing) (this is the say the read text rule): Say "[command clarification break][the read text of the thing read][command clarification break][paragraph break]".

Carry out an actor reading a thing (called the thing read) (this is the read a thing rule): say the read text of the thing read.

Book - Books and Book Parts

A book is a kind of container. It is openable. It is usually closed. It has some text called the title. The description is usually "[the default book description of the item described][run paragraph on]".

To say the default book description of (the book described - a book) (this is the say the default book description rule): if the book described is open, say "[The book described] is open."; if the book described is closed and the book described is titled, say "[The book described] is titled '[the title of the book described]'."; if the book described is closed and the book described is untitled, say "[The book described] is closed."

Part - Book Titles

The title of a book is usually "[the printed name in title case]".

A bound volume is a kind of book. The title of a bound volume is usually "".

Definition: a book is titled if the title of it is not empty. Definition: a book is untitled if the title of it is empty.

Part - Implicit Opening / Closing

To implicitly open (the book opened - a book) (this is the implicitly open a book rule): silently try opening the book opened; say first opening the book opened clarification.

To say first opening (the book opened - a book) clarification (this is the say first opening clarification rule): say "(first opening [the book opened]) [command clarification break]".

To implicitly close (the book closed - a book) (this is the implicitly close a book rule): silently try closing the book closed; say finally closing the book closed clarification.

To say finally closing (the book closed - a book) clarification (this is the say finally closing clarification rule): say "(finally closing [the book closed])[paragraph break]".

Before an actor searching a closed book (called the book searched) (this is the open closed book for searching rule): implicitly open the book searched.

Part - Pages

Some pages are a kind of thing. The description is usually "[if the page count of the book abstracted by the item described is greater than 1][The book abstracted by the item described] has [the page count of the book abstracted by item described] pages. [end if]The pages are uninteresting in themselves; you may want to try reading them." Pages are part of every book.

To decide what book is the book abstracted by (the concrete pages - some pages) (this is the find the book abstracting some pages rule): decide on the object that the concrete pages relates to by the incorporation relation.

A book has a table name called the manuscript. It has a number called the current page.

Before an actor opening a closed book (this is the open a book to the first page rule): now the current page is 1.

After an actor closing a book (this is the close a book and lose the place rule): now the current page is 0.

Chapter - Page Functions

To decide what text is the current page text of (the book read - a book) (this is the decide the current page text rule): let M be the manuscript of the book read; let N be the current page of the book read; decide on the Page Text in row N of M.

To decide which number is the page count of (the book in question - a book) (this is the decide the page count of a book rule): Let M be the manuscript of the book in question; if M is not empty, decide on the number of rows in M; otherwise decide on 0.

To say a page of (the book read - a book) (this is the say a page of a book rule): Let N be the page count of the book read; if N is greater than 1, say the current page number clarification of the book read; say the current page text of the book read; increment the current page of the book read.

To say the current page number clarification of (the book read - a book) (this is the say the current page number clarification rule): say "(page [current page of the book read])[line break]".

To say the current page text of (the book read - a book) (this is the say the current page text rule): say "[line break][current page text of the book read][paragraph break]".

Chapter - Turning To

Turning it to is an action applying to one thing and one value and requiring light. Understand "page [number]" or "[number]" as "[page number]". Understand "turn [book] to [page number]" or "open [book] to [page number]"  as turning it to. Understand "turn to [page number] in [book]" or "open to [page number] in [book]" as turning it to (with nouns reversed).

Before an actor turning a closed book (called the book turned) to a number (this is the implicitly open a closed book for turning to rule): implicitly open the book turned.

Check an actor turning a book (called the book turned) to a number (called the target page) (this is the check turning to a valid page rule): If the target page is less than 1 or the target page is greater than the page count of the book turned, instead say error the target page does not exist in the book turned.

To say error (the target page - a number) does not exist in (the book turned - a book) (this is the say nonexistent target page error rule): say "Page [the target page] does not exist in [the book turned]."

Carry out an actor turning a book (called the book turned) to a number (called the page number) (this is the turn a book to a page rule): now the current page of the book turned is the page number.

Chapter - Turning To First Or Last

Turning to first is an action applying to one thing and requiring light. Understand "first/front" or "the first/front" or "first/front page" or "the first/front page" as "[first]". Understand "turn [book] to [first]" or "turn to [first] of/in [book]" as turning to first. Instead of an actor turning to first a book (called the book turned) (this is the turn to first page rule): try turning the book turned to 1.

Turning to last is an action applying to one thing and requiring light. Understand "last/end/ending/final" or "the last/end/ending/final" or "last/end/ending/final page" or "the last/end/ending/final page" as "[last]". Understand "turn [book] to [last]" or "turn to [last] of/in [book]" as turning to last. Instead of an actor turning to last a book (called the book turned) (this is the turn to last page rule): try turning the book turned to the page count of the book turned.

Part - Summarizing

Summarizing is an action applying to one visible thing and requiring light. Understand "summarize [book]" as summarizing.

Before an actor summarizing a closed book (called the book to be summarized) (this is the implicitly open a book before summarizing rule): implicitly open the book to be summarized.

Check an actor summarizing a book (called the book to be summarized) (this is the check summarizing a book rule): If the read text of book to be summarized is empty, instead say error the book to be summarized has no summary.

To say error (the book to be summarized - a book) has no summary (this is the say summarizing an unsummarizable book error rule): say "[The book to be summarized] is not easily summarized---another possibility is to try READing it."

Carry out an actor summarizing a book (called the book summarized) (this is the summarize a book rule): say the read text of the book summarized.

Section - Book Reading

Before an actor reading a closed book (called the book read) (this is the open closed book for reading rule): implicitly open the book read.

[XXX: This next bit awkwardly overrides checking reading things in general to handle the special case of books. There must be a better way.]

The check reading a thing including books rule is listed instead of the check reading a thing rule in the check reading rulebook.

Check an actor reading a book (called the book read) (this is the check reading a book rule): if the book read is closed, instead say error the book read is stuck closed; if the page count of the book read is 0 and the read text of the book read is empty, instead say error the book read has no content.

Check an actor reading a thing (called the thing read) (this is the check reading a thing including books rule): if the thing read is not a book, abide by the check reading a thing rule.

To say error (the book read - a book) has no content (this is the say reading an no-content book error rule): say "The contents of [the book read] are uninteresting."

To say error (the book read - a book) is stuck closed (this is the say book stuck closed error rule): say "[The book read] seems to be stuck closed, and cannot be read." [XXX: It would take some finagling for this rule to be reached. It's just defensive programming.]

Carry out an actor reading a book (called the book read) (this is the read a book rule): if the page count of the book read is greater than 0, say a page of the book read; otherwise say the read text of the book read; rule succeeds.

After an actor reading an open book (called the book read) (this is the reading the last page of a book rule): let P be the current page of the book read; let N be the page count of the book read; if N is greater than 1 and P is greater than N, implicitly close the book read; if P is greater than N, now P is 1.

Part - Bookcovers

A bookcover is a kind of thing. The description is usually "[The item described] is uninterestingly blank."

To decide what book is the book bound by (the binding bookcover - a bookcover) (this is the find the book bound by a bookcover rule): decide on the object that the binding bookcover relates to by the incorporation relation. [XXX: "decide on the book that the binding bookcover relates to by the incorporation relation" hits Inform 7 bug 729 in version 6G60, as do several similar constructions; see bug 829.]

A title-bearing bookcover is a kind of bookcover. The description is usually "[The default bookcover description of the item described][run paragraph on]".

To say the default bookcover description of (the bookcover described - a bookcover) (this is the say the default bookcover description rule): if the book bound by the bookcover described is titled, say the titled description of the bookcover described; otherwise say the untitled description of the bookcover described.

To say the titled description of (the bookcover described - a bookcover) (this is the say the titled description of a bookcover rule): say "[The bookcover described] is nondescript, merely indicating the title '[the title of the book bound by the bookcover described]'."

To say the untitled description of (the bookcover described - a bookcover) (this is the say the untitled description of a bookcover rule): say "[The bookcover described] bears no title."

Section - Standard Bookcovers

A front cover is a kind of title-bearing bookcover. A front cover is part of every book.

A back cover is a kind of bookcover. A back cover is part of every book.

A spine is a kind of title-bearing bookcover. A spine is part of every book.

Part - The Relevant Book

The nonexistent book is a privately-named book. The last book touched is a book variable. The last book touched is the nonexistent book.

Before an actor doing something to a book (called the book touched) (this is the remember the last book touched rule): now the last book touched is the book touched.

To say error cannot find a relevant book (this is the say cannot find a relevant book error rule): say "There is no obvious choice of book."

To decide which book is the relevant book: If the last book touched is not the nonexistent book and the last book touched is visible, decide on the last book touched; if exactly one book is visible, decide on a random visible book; say error cannot find a relevant book; decide on the nonexistent book.

Understand "read" as reading. Rule for supplying a missing noun when reading (this is the find a book to read rule): Let B be the relevant book; if B is the nonexistent book, rule fails; now the noun is B; say "(reading [the noun])[command clarification break]".

Turning to page is an action applying to one value and requiring light. Understand "turn to page [number]" or "open to page [number]" as turning to page.

Carry out turning to page number (called the page number turned to) (this is the turn to page rule): Let B be the relevant book; if B is the nonexistent book, rule fails; try turning B to the page number turned to.

[Page turning is an action requiring light. Understand "turn page" or "turn the page" as page turning. 

Carry out page turning: Let B be the relevant book; if B is the nonexistent book, rule fails; let P be the current page of B; let Q be P + 1; try turning B to Q; say the current page number clarification of B.]

Book - Bookmarks

[XXX: We put bookmarks in their own "Book" (doh) preparatory to moving them to a separate extension altogether.]

A bookmark is a kind of thing. A bookmark has a number called the bookmarked page.

[XXX: By default, it's nice to be able to see the bookmark hanging out of a book. Of course, if you allow putting other things in books you may want to do something more sophisticated. Or you may just want to force people to open books to see the bookmarks...]

A book is usually transparent.

Part - Bookmarking Actions

Before an actor inserting a bookmark into a closed book (called the book inserted into) (this is the open closed books for bookmarking rule): implicitly open the book inserted into.

Check an actor inserting a thing (called the thing inserted) into a book (called the book inserted into) (this is the check inserting a thing into a book rule): If the thing inserted is not a bookmark, instead say error inserting the thing inserted that is not a bookmark into the book inserted into; if the page count of the book inserted into is 0, instead say error inserting the thing inserted into the book inserted into that has no pages. 

To say error inserting (the thing inserted - a thing) into (the book inserted into - a book) that has no pages (this is the say inserting into a book with no pages error rule): say "[The thing inserted] has no useful place in [the book inserted into]."

To say error inserting (the thing inserted - a thing) that is not a bookmark into (the book inserted into - a book) (this is the say inserting a non-bookmark into a book error rule): say "Putting [the thing inserted] into [the book inserted into] seems pointless."

After an actor inserting a bookmark (called the bookmark inserted) into a book (called the book inserted into) (this is the bookmark a book rule): now the bookmarked page of the bookmark inserted is the current page of the book inserted into; say report that the bookmark inserted is in the book inserted into.

To say report that (the bookmark inserted - a bookmark) is in (the book inserted into - a book) (this is the say inserted a bookmark into a book report rule): say "[The bookmark inserted] falls gently into [the book inserted into]."

Understand "put [bookmark] at/in [page number]" as a mistake ("To bookmark a particular page of some book, you need to open the book to that page, then insert the bookmark. Try OPEN (book) TO PAGE (page), INSERT (bookmark) INTO IT.").

Part - Opening To

Opening to is an action applying to one thing. Understand "turn to [bookmark]"  or "open to [bookmark]" as opening to.

Check an actor opening to a bookmark (called the target bookmark) (this is the check opening to a bookmark rule): If the target bookmark is not contained in a book, instead say error opening to the target bookmark that is not in a book.

To say error opening to (the target bookmark - a bookmark) that is not in a book (this is the opening to a bookmark not in a book error rule): say "[The target bookmark] is not in a book."

To decide which book is the bookmarked book of (the target bookmark - a bookmark) (this is the decide the bookmarked book of a bookmark rule): if a book (called B) contains the target bookmark, decide on B; otherwise decide on nothing.

Carry out an actor opening to a bookmark (called the target bookmark) (this is the open to a bookmark rule):  Let B be the bookmarked book of the target bookmark; let P be the bookmarked page of the target bookmark; try turning B to P; say clarification turning to page P of B.

To say clarification turning to page (the target page - a number) of (the book turned - a book) (this is the say turning to page clarification rule): say "(turning to page [the target page] of [the book turned])[command clarification break]".

Volume - The Talk

Chapter - The Briefing Books

Section - The Useless Manual

The useless manual is a book on the briefing table. "A patently useless manual lies here." The indefinite article is "a". The title is "Useless Manaul" [sic]. The manuscript is the Table of Useless Manual Pages.

Table of Useless Manual Pages
Page Text
"[italic type]The Useless Manual[roman type][line break]by Bart Massey"
"This manual is entirely useless. If you are reading it, you are making a mistake."
"Regardless of its uselessness this manual has several pages. [bracket]The word 'uselessness' is a cool word. Five 's'[']s including two double-'s'[']s---also three 'e'[']s.[close bracket]"

Section - The Briefing Book

The briefing book is a book on the briefing table. The title is "Inform 7 Briefing Book" [sic]. The manuscript is the Table of Briefing Book Pages.

To say p: say paragraph break.
To say l: say line break.

Table of Briefing Book Pages
Page Text
"[italic type]Inform 7 Briefing Book[roman type][l]by Bart Massey[p]Contents[l]* History (p. 2)[l]* Goals (p. 3)[l]* Example (p. 4)[l]* Learning (p. 5)[l]* Caveats (p. 6)[l]* Conclusions (p. 7)"
"Inform 7 is a language for writing text adventures.[p]I7 builds on Inform 6, a standard-looking (mostly) procedural language.[p]I6 is built on the Infocom [italic type]z-code[roman type] infrastructure.[p]I7 compiles to I6, which compiles to z-code.[p]Anything with a keyboard and display probably runs z-code."
"The goal of I7 is to allow game authors to write in lightly-stylized English.[p]It turns out to be doable (even nice?) to write fairly intricate behaviors in this style.[p]Specifying machines, non-player characters (NPCs), complex environments, time, scenes, data structures, reasonable user I/O, and the like in I7 is routine for game writers.[p]In support of this, I7 offers powerful first-class features including a relation-base, constraint solvers, full functional programming, etc---all in reasonablish English."
"The behavior of the book you are reading now was specified in maybe 30 paragraphs of I7.[p]The behavior and environment of the NPC next door, which includes playing perfect Nim, was specified in about 10 paragraphs.[p]Rather than give examples here, I would suggest that you go out-of-world (a cool power) and look at the I7 source to the tinyverse you live in."
"Learning I7 takes a while and is challenging.[p]The community is great, and mostly lives on a MUD.[p]The IDE is pretty nice. Sadly, it works best on Windows, then Mac, then X, but even on X it is quite usable.[p]There's a ton of documentation, but it is quite scattered; I need to work on a metapage.[p]The manual isn't my style: sort of random examples that wind in a not-too-structured way through this vast language."
"There are several downsides to I7.[p]The not-quite-English can be hard to remember and write (although the tools really try to help).[p]The language is huge and changes fairly regularly.[p]The open source situation is...complicated.[p]The limitations of zcode show through.[p]The learning curve is longggg."
"People write non-game-ish demos and stuff in I7 all the time. This is just one example. You can find more on the web.[p]I7 is also a good model for how to do user interaction via DSL. I think it generalizes to GUI UX etc.[p]Inform 7 is cool. You should learn it."



Volume - Nimrod

To decide what number is the xor of (a - a number) and (b - a number):
	(- ({a} + {b} - 2 * ({a} & {b})) -).

Chapter - The Game

There is a room called The Game Room. The Game Room is west of The Briefing Room. "An ancient, pitted Nim Table dominates the center of the room. Behind the table, seated in a high-backed chair, is the legendary Nim champion Nimrod. You, it appears, may stand.[p]An open doorframe leads east."

Section - The XORer - Not for release

A register is a kind of thing. Every register has a number called the rvalue. The rvalue is usually 0. The description of a register is "This register is currently set to [rvalue of the item described]."

To decide what number is the xor of (a - a register) and (b - a register): let ra be the rvalue of a; let rb be the rvalue of b; decide on the xor of ra and rb.

The xorer is a thing in The Game Room. "A high-quality xorer sits in a corner of the room, each input register ready for assignment." A register called the alpha register is part of the xorer. A register called the beta register is part of the xorer. The description of the xorer is "The xorer indicates that the xor of alpha = [the rvalue of alpha] and beta = [the rvalue of beta] is [the xor of alpha and beta]."

Assigning it to is an action applying to one value and one visible thing and requiring light. Understand "assign [number] to [register]" as assigning it to. Check assigning a number (called v) to a register: if v < 0, say "The registers are unsigned." instead. Carry out assigning a number (called v) to a register (called r): now the rvalue of r is v.

Section - The Setting

A nim table is a scenery supporter in The Game Room.  The description is "This table is waist-high, and has three pits for stones. [The description of pit one] [The description of pit two] [The description of pit three]". A high-backed chair is a scenery supporter in The Game Room. The description is "The high back of this chair is ornately carved." The carvings are part of the high-backed chair. The description is "Intricately-carved abstract patterns somehow express the nim-ness of the situation."

Nimrod is on the high-backed chair. He is scenery. The description is "Nimrod's long black hair, pulled back and fastened, contrasts with his pale skin, as does the black stubble on his cheek and jaw. His white gi is fastened with a white belt." Nimrod wears a white gi. The description of the white gi is "The garment appears sound, but its long use is apparent. In short, this gi is the epitome of comfortable clothing." Nimrod wears a white belt. The description of the white belt is "Why does Nimrod wear a white belt? To keep his gi shut."

To say (n - a number) stones: if n is 0, say "nothing"; if n is 1, say "one stone"; if n is greater than 1, say "[n] stones".

A pit is a kind of thing. Every pit has a number called the stone count. The description of a pit is "[The item described] contains [the stone count of the item described stones]."

A pit called pit one is part of the nim table. The stone count of it is 3. Understand "pit 1" as pit one.

A pit called pit two is part of the nim table. The stone count of it is 5. Understand "pit 2" as pit two.

A pit called pit three is part of the nim table. The stone count of it is 7. Understand "pit 3" as pit three.

Section - Playing Nim

Taking it stones from is an action applying to one value and one visible thing and requiring light. Understand "take [number] stone/stones/-- from [pit]" as taking it stones from.

Check taking a number (called n) stones from a pit (called p): let np be the stone count of p; if n > np, say "Your reach exceeds your grasp. Too many stones? The wrong pit? Just confused? Who can say?" instead; if n < 1, say "Clever...but also illegal. Nimrod glares mercilessly at you as you pull your hand back." instead. 

Carry out taking a number (called n) stones from a pit (called p): now the stone count of p is the stone count of p - n; say "You feel [n stones] magically fade away at your touch. [The p] now contains [the stone count of p stones]."; try Nimrod moving.

Carry out Nimrod taking a number (called n) stones from a pit (called p): now the stone count of p is the stone count of p - n; say "Nimrod deftly erases [n stones] from [the p], leaving [the stone count of p stones]."

Moving is an action applying to nothing.

Definition: A pit is nonempty if the stone count of it is greater than 0.

To decide whether the table is empty: let l be the list of nonempty pits; if the number of entries of l is 0, yes; otherwise no.

Check Nimrod moving when the table is empty: say "Nimrod stares sadly at the empty pits. He hangs his head in shame. He has been defeated.[paragraph break]Congratulations, you bastard. You've ruined everything."; now the score is 1; end the story.

Report Nimrod moving when the table is empty: say "Nimrod's eyes flash in triumph as he completes his victory. You have lost, as he knew you would.[paragraph break]You slink away in shame."; now the score is -1; end the story.

Section - Computer Play

Carry out Nimrod moving:
	say "Nimrod ponders the situation ponderously...[line break]";
	let q be 0;
	repeat with p running through the list of nonempty pits:
		let n be the stone count of p;
		now q is the xor of q and n;
	repeat with p running through the list of nonempty pits:
		let n be the stone count of p;
		let r be the xor of n and q;
		if n > r:
			let t be n - r;
			try Nimrod taking t stones from p instead;
	let m be pit one;
	repeat with p running through the list of nonempty pits:
		let nm be the stone count of m;
		let np be the stone count of p;
		if np > nm:
			now m is p;
	try Nimrod taking 1 stones from m.
		
Chapter - Testing - Not for release

Test winning with "take 1 stone from pit 1 / take 1 stone from pit 2 / take 1 stone from pit 1 / take 1 stone from pit 1 / take 1 stone from pit 3 / take 1 stone from pit 3 / take 1 stone from pit 3 / take 1 stone from pit 3".

Test losing with "take 3 stones from pit 1 / take 4 stones from pit 3 / take 1 stone from pit 2"

Volume - Demo Lab

Chapter 1 - The Game

The Demo Lab is a region. The Demo Room and the Airlock are in the Demo Lab.

Some walls are a backdrop which is in the Demo Lab. Some metal sheets are a backdrop which is in the Demo Lab.

The metal ladder is a backdrop which is in the Demo Lab. The description is "It looks worn but sturdy." Instead of climbing: try going up. Understand "climb [ladder]" as climbing.  Understand "climb up [ladder]" as climbing. [still needs work]

A room has a room called the xyzzy-room. The xyzzy-room of a room is usually nowhere.

Xyzzying is an action applying to nothing. Carry out xyzzying when the xyzzy-room of the location of the player is not nothing: say "*Poof*!"; now the player is in the xyzzy-room of the location of the player; rule succeeds. Carry out xyzzying:  say "Wha?"; rule fails. Understand "xyzzy" as xyzzying.

Section 1 - The Demo Room

The Demo Room is south of The Briefing Room. "Around you stretch the riveted sheets of bare metal that form the walls of the Demo Room. At the center of the room, a narrow metal ladder leads upward through a hatch in the ceiling, currently [lower hatch position]. An open doorframe leads north." The xyzzy-room of the Demo Room is the Airlock.

The sign is an object in the Demo Room. "A flimsy plastic sign is affixed to one wall." The description is "The sign reads 'Up and Out!'" It is fixed in place.

The cardboard box is an unopenable open container in the Demo Room. "A nondescript cardboard box sits in the corner. The sides sag out." Before taking the box: try apprehending the zorkmid. Carry out looking under the box: say "You see what looks like the underside of a cardboard box."; try apprehending the zorkmid. Instead of pushing the box when the box is not carried: say "You give the box a shove."; try apprehending the zorkmid. 

The zorkmid coin is an object. The description is "This zorkmid coin is made of the usual lead-gold alloy (heavy on the lead)." After examining the zorkmid for the first time: say "You muse on the distant land from which this coin must have originated." Apprehending the zorkmid is an action applying to nothing. Carry out apprehending the zorkmid for the first time: now the zorkmid is in the Demo Room; try silently taking the zorkmid; say "You find a zorkmid coin under the box (taken)."

Section 2 - The Airlock

The Airlock is a room. It is below the upper hatch and above the lower hatch. "You hang from a metal ladder in a circular metal shaft. The room is bathed in the reddish light of emergency lamps. There are vents in the wall of the shaft near the top and the bottom. A lower hatch,  [lower hatch position] below you, leads to the Demo Room; an upper hatch, [upper hatch position] above, leads...who knows?" Some reddish lamps are scenery in the Airlock. The description is "These incandescent lamps, obscured by metal gratings, emit an orange-red glow."  Understand "lights", "light" and "lamp" as the lamps.  Some vents are scenery in the Airlock. The description is "The vents are covered with dinged and pitted metal grating. Behind them is an ominous darkness." Understand "vent" as the vents. The xyzzy-room of the Airlock is the Demo Room.

A hatchway is a kind of door which is openable and lockable. It is usually closed. It is scenery. To say (H - a hatchway) position: if H is open, say "open"; otherwise say "closed".

The upper hatch is a locked hatchway. It is above the Airlock. The description is "This [upper hatch position] hatch leads from the Airlock into the mysterious unknown."

The lower hatch is an unlocked hatchway. It is below the Airlock and above the Demo Room. The description is "This [lower hatch position] hatch connects the Airlock and the Demo Room."

Section 3 - The Hatch Wheel System

The hatch wheel is in the Airlock. "A small metal wheel protrudes from a shaft halfway up the wall opposite you." It is fixed in place. The wheel can be either pointing upward or pointing downward. It is pointing downward. The description is "This is a rough metal wheel with four spokes affixed to the wall. It looks like some kind of control. There is a red mark painted on the wheel, currently at [mark placement]."  To say mark placement: if the wheel is pointing upward, say "the top of the wheel"; otherwise say "the bottom of the wheel".

To decide whether the wheel is active: if the lower hatch is closed and the upper hatch is closed and the slot is loaded, decide yes; otherwise decide no. To decide whether the wheel is inactive: if the wheel is active, decide no; otherwise decide yes. Before turning the wheel, ignore the can't turn what's fixed in place rule. Instead of turning the wheel when the wheel is inactive: say "The wheel wiggles, but refuses to move.". After turning the wheel, say "The wheel turns creakily through a half revolution. Dry, sterile-smelling air pours from the upper vents and flows out the lower vents for a moment, then stops. Eerie quiet resumes." Carry out turning the wheel when the wheel is active and the wheel is pointing downward: now the lower hatch is locked; now the upper hatch is unlocked; now the wheel is pointing upward; rule succeeds. Carry out turning the wheel when the wheel is active and the wheel is pointing upward: now the lower hatch is unlocked; now the upper hatch is locked; now the wheel is pointing downward; rule succeeds.

The slot is in the Airlock. "Next to the wheel is a small slot." The description is "The slot is entirely nondescript. It is vertical: about the height and width of a silver dollar." It is fixed in place. The slot can be either loaded or unloaded. It is unloaded. Loading it into is an action applying to two touchable objects. Carry out loading the zorkmid into the slot: say "The zorkmid vanishes into the slot with a metallic clink."; remove the zorkmid from play; now the slot is loaded; rule succeeds. Carry out loading an object into the slot: say "You look more closely at the [noun] and at the slot and change your mind." Understand "put [thing] in/into [slot]" as loading it into. Understand "drop [thing] in/into [slot]",  "insert [thing] in/into [slot]" and "load [thing] in/into [slot]" as loading it into.

Section 4 - Ending the Game

After going through the upper hatch: say "You climb out of the Demo Lab and into the Briefing Room. All that work for nothing!"; increment the score; now the player is in The Briefing Room.

Chapter 2 - Testing and Debugging - Not for release

Going unto is an action applying to one thing. Carry out going unto a room (called R) (this is the going unto a room rule): move the player to R. Before going unto a thing: ignore the basic accessibility rule. Carry out going unto a thing (called T) (this is the going unto a thing rule): move the player to the location of T. Understand "go unto [any room]" as going unto. Understand "go unto [any thing]" as going unto. Test go-unto with "go unto wheel / go unto nonexistent / go unto Demo Room".

Test me with "test sign / test zorkmid / up / test airlock / test wheel".

Test sign with "take sign / read sign".

Test zorkmid with "look in box / look under box / i".

Test airlock with "up / close lower / down / close hatch / up".

Test wheel with "close lower / turn wheel / put zorkmid in / turn wheel / down / up".


Chapter - The Restroom

The restroom door is a scenery door. The restroom door is east of The Briefing Room and west of the Genderless Restroom. The description is "The restroom door bears the universal indication of both genders."

The Genderless Restroom is a room. "It's a restroom. You've seen them before. Do you really need a detailed model of all the fixtures? If you [italic type]must[roman type] flush the imaginary toilet, imagine doing so now, and supply your own vision of the result. Go ahead, I'll wait.[paragraph break]The door is to the west."