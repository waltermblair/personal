---
layout: post
title: "Apache Ignite - Follow Up"
date: 2018-01-10
---
<b>Apache Ignite - Part II</b>  

I had a really happy (and tiring) few months with the little one, and now it's time to get back into gear on research. This post follows up on my previous introduction to Ignite, summarizes a the take aways from a few papers I had finally waded through, and hopefully answers some of the questions I had at the end of that discussion.

<h3>The Big Question</h3>
The major question I tried to answer in the past few days is what we gain and what we lose by shifting focus from Spark to Ignite. Specifically, the whole point of Spark waas to solve consistency and efficiency problems with shared memory systems that had come before. So do we lose Spark's consistency and efficiency when we instead use Ignite's shared memory?

In the release paper describing Spark's underlying Resilient Distributed Datasets, the authors emphasize the consistency and efficiency of the RDD abstraction over previous attempts to use shared memory in distributed systems. RDDs are resilient, because a dataset's lineage can be used to recompute missing data at anytime over the lifetime of the RDD. RDDs are efficient, because a dataset is immutable and therefore excludes the fine-grained updates that are the bread and butter of relational databases in favor of the coarse-grained read-only operations used in a wide variety of analytical applications.

So in shifting to Ignite, which brings its own implementation of Spark's RDD as described in my previous post, we stand to lose the two major achievements of resiliency and efficiency. 

<h3>IgniteRDD Resiliency</h3>
The ability of a Spark application to recompute missing RDD data deterministically is critical to its resiliency. Conventional distributed systems rely on data backups that must be moved around the network to facilitate fault recovery. During an update operation, the backups must also be updated, and the system will fall somewhere in the speed v. consistency tradeoff. Either the system is extremely fast and the backups are often inconsistent with the primary data, as in a typical NoSQL system, or the speed is sacrificed in order to enforce strict consistency, as in an ACID-compliant relational database. Spark on the other hand is built in such a way that datasets can be recomputed in case of failure by following the dataset's lineage of deterministic operations. Not having to deal with lots of data shuffling and updates contributes significantly to Spark's speed, but the authors note that conventional dataset checkpoints nevertheless become important as the size of the dataset grows and the cost to recompute pieces of it increases past a certain point (Zaharia 2012).

The cost then of using checkpoints with Ignite between application contexts isn't necessarily a tradeoff between speed and performance but rather a question of the size of the dataset. Are typical use cases for our Ignite pipelines going to use datasets large enough to benefit from Spark checkpoints? If yes, then our strategy for resiliency won't actually diverge from Spark's strategy where recomputing datasets is unwieldy. If no, then we should expect performance decreases and should weigh this cost with the benefits of maintaining the dataset in Ignite's distributed cache.

I need to be sure I understand Ignite's coherance strategy. I think that it uses owner-based distribution of data, where an owner receives a direct request for data, and I need to understand the pros/cons of this approach compared to an RDBMS's broadcast strategy that is more ACID-compliant.

For a broad comparison of Spark with distributed shared memory systems, compare Table 1 of Nitzberg and Lo (1991) with Table 1 of Zaharia et al. (2012). It seems like the two tables summarize DSM systems differently and this seems important.

<h3>IgniteRDD Efficiency</h3>
Spark is extremely efficient, because RDBMS-style fine-grained updates are excluded by the immutability of Spark's RDDs. IgniteRDDs, on the other hand, are mutable and do allow updates. Opening up the ability to perform updates on our dataset will drop the important assumptions Spark uses to maintain really break-neck speed on immutable RDD transformations. Is it worth it? The question is whether we need OLTP functionality or whether we are satisfied with OLAP. It seems to me that the the development of a HTAP system that does both moderately well is a worthy goal, but we need to decide whether our use cases demand the extra functionality at the expense of perforamce. One interesting option is a time-traveling insert-only hybrid system like the one proposed by Plattner (2009). Plattner summarizes a lot of his group's work by recommending columnar storage which allows really efficient compression (seconded to be sure by ADAM) and an insert-only dataset with timestamps that allow the dataset to be checkpointed easily. Our group has previously discussed the possibility of adding additional columns to represent subsequent steps in an RNA-seq processing pipeline, for example, and Plattner's approach works well for adding columns to a dataset. Each step in the pipeline could simply insert new records to reflect the "updated" sequence reads.

A question here is whether Ignite is better suited for row-based or column-based data. I also should take a glance at VoltDB and MemSQL here.

Regarding OLTP capability, take a look at SAP HANA and MonetDB.

<h3>References</h3>  
Nitzberg B, Lo V. 1991. Distributed Shared Memory: A Survev of Issues and Algorithms. Computer 24(8):42-50.

Plattner H. 2009. A Common Database Approach for OLTP and OLAP Using an In-Memory Column Database. Proceedings of the 35th SIGMOD international conference on Management of data - SIGMOD '09.

Zaharia M, Chowdhury M, Das T, Dave A, Ma J, McCauley M, Franklin MJ, Shenker S, Stoica I. 2012. Resilient distributed datasets: A fault-tolerant abstraction for in-memory cluster computing. Proceedings of the 9th USENIX conference on Networked Systems Design and Implementation. USENIX Association, 2012.
