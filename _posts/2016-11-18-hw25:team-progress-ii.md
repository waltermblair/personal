---
layout: post
title: "HW25: Team Progress II"
date: 2016-11-18
--- 
We had a fair amount of work to do following our last Deliverable #3, so I'll recap that a bit. Our automated testing framework with the Simple-Java-Calculator was put together super fast, and we took an unfortunate turn at a fork in the road in its design. We weren't exactly sure how much work the Java method driver was allowed to do. The choice was to either pass the testCase.txt file to the driver and let the driver unpack the contents or to have the script unpack the contents and then simply pass the input value for the method. We unfortunately chose the former option. The framework executed and printed a report for that deadline, but we had to go back and restructure the framework so that the script would do all of the work.  

To be completely honest, I planned to do as little work as possible on this Deliverable #4. I was sort of burned out from putting #3 together so fast, so Matthew and Nicholas did the great majority of the work for this last deliverable. Matthew totally redid the html report creation and format so that it is readable in rows and compatible with current web standards. We made a lot of progress in class on transferring the work from the Java driver to the script. Nicholas and I got the first test case working, but he reworked the existing 12 test cases we had and wrote remaining cases to bring us to 25 total.  

I think we're in the clear now in terms of having a solid structure for our framework, so the work ahead with fault injection seems super manageable. I'm hoping the frustration is mostly behind us, and putting together pdfs and .ppt files will be a cakewalk compared to this.   
