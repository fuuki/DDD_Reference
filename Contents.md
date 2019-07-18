## Contents

略

\* New term introduced since the 2004 book.

### Acknowledgements

It has now been over ten year since the publication of my book, Domain-Driven Design, Tackling Complexity in the Heart of Software (or “The Big Blue Book”, as some people have taken to calling it). In that decade, the fundamentals discussed in the book haven’t changed much, but a lot has changed about how we build software. DDD has stayed relevant because smart and innovative people have shaken things up repeatedly. I want to thank those people.

Let me start with Greg Young, Udi Dahan and the people inspired by them, for CQRS and Event Sourcing. These are now quite mainstream options for the architecture of a DDD system. This was the first successful big departure from the narrow view of architecture inherited from the turn of the century.

Since then, there have been several interesting technologies and frameworks that had a goal of making DDD more concrete in implementation (among other goals of their designers), with varying degrees of success. These include Qi4J, Naked Objects, Roo, and others. Such experiments have great value, even when they don’t gain wide adoption.

I also want to thank the people and communities that have revolutionized our technical ecosystem in recent years in ways that make DDD much more fun and practical. Most of these people have minimal interest in DDD, but their work has benefited us tremendously. I’m particularly thinking of the freedom NoSQL is bringing us, the reduced syntactical-noise of new programming languages (some functional), and the relentless drive toward lighter technical frameworks and unintrusive, decoupled libraries. The technology of a decade ago was complicated and heavy, and made DDD even more difficult. There is bad new technology too, of course, but the trend is good. So I extend a special thanks to all those who have contributed to this trend, though you may never have heard of DDD.

Next, I want to thank those who have written books about DDD. The first book about DDD after mine was by Jimmy Nilsson. With one book, you have a book. With two, you have a topic. Next, InfoQ published DDD Quickly, which, because of its brevity, its availability as a free download and the reach of InfoQ, gave a lot of people their first taste of the topic. The years went by, and there were many valuable blog articles and other short-form writings. There were also specialty books such as DDD with Naked Objects. And I particularly want to thank the indispensable Martin Fowler, who has helped to clearly communicate the concepts of DDD as well as often providing the definitive documentation of emerging patterns. Just last year, Vaughn Vernon published the most ambitious book since my own, Implementing Domain-Driven Design (which some seem to be calling “The Big Red Book”).

I feel a kind of despair over the inevitability that I will leave out many people who made significant contributions, and I am genuinely sorry about that. Let me at least give a blanket thank you to the people who have pushed DDD out into the public view and to those who have pushed DDD into quiet corners of organizations. It takes thousands of champions for a software philosophy to have any impact.

Although this is the first print edition of the DDD reference, the earliest form actually predates the publication of my 2004 book. On the advice of Ralph Johnson, I extracted the brief summaries of each pattern and used them in workshops, with each pattern being read aloud by attendees followed by discussion. I used those documents in training classes for several years.

Then, a few years after my book was published, Ward Cunningham, as part of his work on a patterns repository, proposed to a few authors that we put short summaries of our patterns into the Creative Commons. Martin Fowler and I, with the agreement of Pearson Education, our publisher, did just that, which opened up possibilities for derivative works, such as this one.

Thank you all.

Eric Evans, June 2014

### Definitions

#### domain

A sphere of knowledge, influence, or activity. The subject area to which the user applies a program is the domain of the software.

#### model

A system of abstractions that describes selected aspects of a domain and can be used to solve problems related to that domain.

#### ubiquitous language

A language structured around the domain model and used by all team members within a bounded context to connect all the activities of the team with the software.

#### context

The setting in which a word or statement appears that determines its meaning. Statements about a model can only be understood in a context.

#### bounded context

A description of a boundary (typically a subsystem, or the work of a particular team) within which a particular model is defined and applicable.

### Pattern Language Overview

---

!!!Image here!!!

---
