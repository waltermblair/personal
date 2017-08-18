---
layout: post
title: "CSIS 604 - NoSQL Review"
date: 2017-07-21
---
<b>NoSQL Review</b>  

In CSIS 601, the database project I chose to build was an automatic homebrew clone recipe builder. The database was automatic in the sense that a user would click ‘update ingredients’ buttons that would scrape hops, yeasts, and malts from pre-defined websites and update all the ingredients tables. The user would then type in the name of the beer, and the system would scrape beeradvocate.com for that beer. The user would finally click on the returned beer name, and the system would run through some logic and insert a new recipe into the database...easy interface and no opportunity for users to make CRUD operations on the database. 

In retrospect, this whole design was poorly suited for the assignment, because the project was to build a MySQL relational database with well-defined normalization, isolation, and ACID properties. I didn’t care about any of that, though. This was the first lesson I had in the importance of choosing the right system for a particular use case, and I had no idea how many options there actually were until reading Cattell 2010 [1]⁠. In 601, we had consistency drilled into our heads, because critical systems often depend on consistency. I’m not so optimistic as the author that users “tolerate” errors in purchase orders and overbooking of flights, but I nevertheless agree with the author that relational database management systems will always fill an important need. On the other hand, my website was generating beer recipes, and almost no one thinks homebrewing is mission-critical…

 The current paper does a great job of 1) overwhelming the reader with the available options for data store systems and thereby increasing the perceived need for a knowledgeable consultant and 2) summarizing what sorts of systems work with a variety of use cases. As for point number one, I respect that consultants gonna consult, but aside from being overwhelmed by so many data store solutions, one of the important points I gathered was that the market is extremely competitive and the selective pressures are fierce. Some of the systems mentioned here in 2010 I have heard of in 2017, and others I have not. If I were tasked with choosing one system over another, a strong consideration would be whether the product had a long track record of success. It seems that there are two likely fates for some of the smaller companies – either get bought out or go extinct, and I would hesitate to choose a newer solution for fear of the latter option. I would certainly be willing to sacrifice certain system properties for an assurance that I won’t have to migrate my system in a year’s time. Regarding point number two, I appreciate the author’s more general and stable information on which sorts of systems work well for various uses. Were I to put my 601 project into production, I might choose a NoSQL system like Cassandra that would allow extensible records and that prefers availability and partition-tolerance over consistency. More to the point for this class, it seems clear that if scalability and performance are the highest priorities, then a relational system that prioritizes consistency probably will never be the best solution. On the other hand, if it’s possible to throttle down the system a touch, then I don’t see why the ubiquitous and easy-to-use SQL solution wouldn’t be the most pragmatic choice. SQL isn’t sexy, and as the author points out, it is very easy to do very expensive queries with it, but SQL is so widely understood and supported, that the convenience and stability would spill over to benefits in staffing, system maintenance, etc.

References
[1]	R. Cattell, “Scalable SQL and NoSQL data stores,” ACM SIGMOD Rec., vol. 39, no. 4, p. 12, 2011.