---
layout: post
title: "Deep Pipeline"
date: 2017-04-21
---
<b>Deep Pipeline</b>

I wrote my last post after reading through the 2015 paper on ADAM as a framework for democratizing big data in science. The authors argued that ADAM opens up genomic processing by allowing open-source processing tools to run on commodity hardware via Spark. They have so far implemented several important steps in the RNA-seq pipeline, and it seems like the project is gaining momentum. And just when I got on board with the ADAM approach, planning a thesis around sort of retooling other parts of the pipeline to plug into ADAM, another [2015 paper](https://people.cs.umass.edu/~aroy/genomic-cidr15.pdf) comes up and forces me to organize my thoughts here in another post.  

Diao, Roy, and Bloom present their progress on a full pipeline that takes advantage of a sort of customized Hadoop "substrate" that runs a full processing pipeline using existing tools. Some advantages of their deep pipeline include the ability of the user to decide which algorithms they want to use (e.g. BWA or another aligner) and I/O optimization afforded by a scheduler that moves piece of the pipeline around and logically partitions the data in order to reduce the amount of time spent reshuffling the data for different steps.  

There are a few points in here I want to think more about. One is the idea that several components of the pipeline are really hard to parallelize. The authors explain that while individual steps may be parallelized, it is difficult to parallelize the whole pipeline because individual components require different chunks of data to run, and that different chunking patterns will produce different results. I don't understand what this means! I understand, for example, that if you split up a large text file then you'll run into problems if a node needs part of the file that it doesn't have, but I don't see how this problem carries over to a Spark RDD. It seems to me that Spark's RDD's (and dataframes and datasets as well) are so successful because the scheduler ensures that each worker will have what it needs. These authors would say that then a large amount of shuffling would be necessary to reorganize between steps, but I wouldn't have thought that simply projecting different pieces of the dataset would be costly. I need to learn more about how RDD's are physically distributed to workers and how much work is required to figure out who needs what information. Until I understand how this works, I won't really understand the authors' claim that the whole pipeline can't be parallelized without super costly reshuffling.

 The other idea I want to understand is the claim that this deep pipeline approach is better than ADAM because unlike ADAM it doesn't require reimplementing existing tools. I didn't really think that ADAM required reimplementing existing tools...or perhaps it does and this is what the cannoli wrapper is intended to do. Understanding this is important, because we are trying to plug existing tools into the ADAM framework and are working under the assumption that it won't take an unreasonable amount of effort to do so. I think this point will be important for our group to discuss in the next few weeks.