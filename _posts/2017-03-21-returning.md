---
layout: post
title: "Returning"
date: 2017-03-21
---
<b>Returning</b>

I finished CSCI 362, Dr. Bowring's software engineering course that had me blogging regularly, and have since started work toward my M.S. Computer & Information Sciences. I've learned a lot these past few months but have had a difficult time getting a grasp on what I know and what I don't know, so it seems that it's high time to return to the blog as a way to think through my progress and obstacles more clearly.

I just borrowed a book from Dr. Bowring - <i>Software Development: An Open Source Approach</i> by Tucker, Morelli, and de Silva. I asked him for some advice on how to wrap my head around the largest codebase I've so far tried to tackle, and he recommended Chapter 6 which details a solid strategy on approaching new software in a systematic way with the aim of eventually making a successful contribution.

The most basic advice is really important for me - take a top-down approach to reading the code. I've waded into parallel programming by way of Apache Spark and bdgenomics/adam, and I'm trying to tackle the adam software without having a ton of familiarity with Scala or Spark. When I've wanted to understand specific functions like how adam reads in a fastq file and converts it to an RDD, or how a JavaRDD is piped to a Scala RDD, I've tried to dig really deep into very specific classes and functions without taking the time to look from a high level at the overall structure of the software and the big domain classes that set the stage for these specific functions I'm interested in. I'm going to try this week to start from the top and understand the general structure and workflow of the software and slowly wade further in as I get more comfortable with it.

The other important advice is a reminder from what I learned in software engineering - any successful contribution I want to make will depend on me being really organized, and one of the most important ways to stay organized is to keep careful stock of functional/non-functional requirements and unit tests. I'm excited to try to develop some automated testing for the Scala read-trimmer I'm working on, because it will help me make a better product and also give me a better understanding of how to contribute in a professional setting as part of a development team.

So my major short-term goals this week are to start my top-down look at how adam works and also to get my Scala trimmer organized so that I can write specifications and start automating tests.
