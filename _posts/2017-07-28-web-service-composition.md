---
layout: post
title: "CSIS 604 - Web Service Composition"
date: 2017-07-28
---
<b>Web Service Composition</b>  

Sheng et al. (2014) begin their review of web service composition with the clearest definition of web services and service oriented computing that I’ve ever read [1]⁠. Web services are standardized interfaces with an identifier, a set of attributes, and a set of operations (they sound like objects that you can call up). They are standardized so that they can sort of plug-and-play with other services, and the two most well-developed standards are SOAP and REST. Calling a single web service might be simple, but the industry is moving toward large networks and pipelines of composed web services. Entire platforms built by Google, Amazon, etc. are built around web service composition. This is difficult to do well. In software engineering, we learned about the exponentially increasing complexity of systems as the number of component parts increases. A web service that functions well in a vacuum or even composed with one set of existing services might fail in some novel system, and it’s quite difficult to perform system tests for systems that don’t yet exist!

Sheng et al. (2014) review the current techniques for composing web services. They begin by reviewing several leading definitions of web services, but all of them center around the notion of an openly accessible and standardized application. The openly accessible part comes from an internet connection but also requires that the interface be predictable and consistent, and the authors go on to summarize the two major standards SOAP and REST. I have previously thought of SOAP as a more cumbersome and stringent older brother to the more relaxed and fun-loving REST younger brother, but maybe that’s just me. Like probably many people, I am familiar with RESTful GET, PUT, DELETE, and POST verbs, but I don’t know much about SOAP calls. 

I have heard of BPEL, but I wasn’t aware of the distinction between orchestration (BPEL) and choreography (CDL). It sounds like orchestration centralizes control or functionality in a single unit whereas choreography let’s each component service sort of understand and have some say in what’s going on with the larger picture. The distinction between static and dynamic composition makes sense – I imagine that a SOAP composition within an enterprise system might be statically composed, whereas a dynamic cloud cluster for example would be dynamically composed as containers and such come and go. These dynamic services are likely more and more being automatically composed, whereas the static enterprises are probably manually composed.

The life cycle diagram is a useful framework for thinking about the composition process and would probably do me some good on our composition assignment (Fig 1)! It reminds me a lot of the requirements elicitation processes used in software engineering, though this diagram goes all the way to deployment and execution without the word test being used anywhere. It’s interesting that some failure correction is discussed as playing an important role in the Definition phase of the life cycle, and the success of this process must come out of the thoroughness and correctness of the modeling language and documentation produced during this phase.

I’m most interested in the standardization efforts discussed in section four, because standardization is incredibly difficult in an area that evolves and shifts as rapidly as web services. I mentioned earlier that I thought I had heard of BPEL, but what I think I actually had seen before was BPML. BPEL, the execution language isn’t familiar to me, but I get the impression that it is well suited for large compositions and for organizations that are fans of formalization. I’m assuming that it is naturally quite hierarchical given the authors earlier statement that it is used for orchestration. CDL and BPML are both used for choreography and are very popular, but I’m not sure what to think about ebXML and OWL-S except that they sound more niche-specific. Of course Europeans have their own standard with WSMF which is tailored for e-commerce. Judging by Table 1, the authors really don’t appreciate OWL-S or WSMF.

The major contribution of this review is the comparison of thirty-some-odd composition research prototypes, but I certainly won’t dive into all of the results. I’m most interested in eFlow, WISE, and Self-Serv which the authors highlight as older systems that have made important contributions to the field. It sounds like eFlow made major progress in dynamic composition using a process called dynamic conversation selection [2]⁠. WISE developed a really nice separation of concerns for business to business commerce [3]⁠. Self-Serv sounds like it pioneered some really nice control strategies by clearly defining roles and scopes for services and also happens to be authored by the authors of this review [4]⁠.

The review of platforms makes me feel like I have no clue what the authors are talking about, because my experience with web service composition so far doesn’t use any of these. I thought that what I was doing with the Salesforce API in CSIS 659 was something related to web service composition, and I could have sworn that Google Cloud has a whole suite of web service composition tools. It looks like BPEL is king here, so that would be a good skill for me to practice.

It looks like the authors are pushing for more support around RESTful web service composition, but it seems like this would be at tension with the other open issues like dependability and security. There must be some engineering tradeoffs here, but it seems like the authors want it all.

References
[1]	Q. Z. Sheng, X. Qiao, A. V. Vasilakos, C. Szabo, S. Bourne, and X. Xu, “Web services composition: A decade’s overview,” Inf. Sci. (Ny)., vol. 280, pp. 218–238, 2014.
[2]	F. Casati and M.-C. Shan, “Dynamic and adaptive composition of e-services,” Inf. Syst., vol. 26, no. 3, pp. 143–163, May 2001.
[3]	A. Lazcano, G. Alonso, H. Schuldt, and C. Schuler, “The WISE Approach to Electronic Commerce,” Int. J. Comput. Syst. Sci. Eng., vol. 15, pp. 345–357, 2001.
[4]	Q. Z. Sheng, B. Benatallah, M. Dumas, and E. O. Y. Mak, “SELF-SERV: A platform for rapid composition of web services in a peer-to-peer environment,” Search, no. 2002, p. 1054, 2002.