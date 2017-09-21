---
layout: post
title: "Weekly Update"
date: 2017-09-21
---
<b>Weekly Update</b>  

The plan last month changed a bit, but it seems to have worked out! My goal was to string together some Scala Spark applications to show that the in-memory strategy scales better, but I got stuck at the problem of transferring a dataset from one Spark context to another context. I noticed that Apache Ignite provided a solution for persistent IgniteRDDs that could be passed in this way, so we combined Ignite and named pipes to build a demonstration that a pipeline of non-Spark applications can be executed entirely in memory and skip all the intermediate I/O. We got a conference paper together, and I look forward to getting some feedback on it, so far so good!

I wanted to take a step back and get a bit more context on what other folks are doing to make processing pipelines more efficient, and it seems like Toil got a reboot that deserves a closer look. Toil is funded by the same BD2K Genomics project that produced ADAM and the rest of the standards-based big data stack, and they've just published some example workflows driven by Toil [https://github.com/bigdatagenomics/workflows]. These workflows are meant to execute processing pipelines within the ADAM universe using various components that have either been wrapped for Spark with cannoli or reimplemented in Spark via ADAM.

It looks like Toil has a lot going for it, especially the Dockerization, WDL-based standardization, and generally-accessible Python implementation that suggest to me that it is built to be around for awhile. Designing a workflow seems to take a bit of work, but what I was really interested in was how the workflow components are linked together - are intermediates in memory or on disk? On disk, it turns out!

I appreciate the realization that even the newest and most Spark-enthusiastic pipelines are still stuck with intermediate files, and I also am excited that Toil might be a really high-impact project to target with our named pipe and persistent IgniteRDD tweaks. I'm going to spend a bit of time trying to see if I can trick Toil into using named pipes. Toil's FileStore is a really robust class designed to manage intermediate file I/O, so this will be my focus for a little while. Even if it turns out that Toil is incompatible with our approach, I'll end up with a better understanding of one of the most promising projects directly related to my thesis work.

I'll alternate my Toil study with my attempts to get better acquainted with Ignite and named pipes so that I have a clearer idea of what exactly we did with our paper. Hopefully I'll arrive at the conference with a pretty solid understanding of what we did as well as what others are doing.
