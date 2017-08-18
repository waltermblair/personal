---
layout: post
title: "Weekly Update"
date: 2017-08-18
---
<b>Weekly Update</b>  

After taking a break from Scala and Spark all summer, it's fun getting back into the swing of things. I work well with some well-defined external motivation, so I decided mid-week to shoot for the Sep 5 deadline for submitting a paper to BIOSTEC 2018 in January in Portugal. After catching up with Leo Friday morning, it seems clear that we have enough to go around for two parallel but independent papers. Leo will work more with the REU project on using named pipes that can be used to link together existing software tools with some scripting and no modification to the source code, and I'm going to try to flesh out my work on reimplementing tools in Scala to pass datasets from one step to another in memory.   

The data I collected back in the spring shows that my Scalatrim application scales better than Trimmomatic due to the use of the wholeTextFiles function that reads N many input files at once, which works more efficiently than dealing with one at a time as Trimmomatic must do. I realized just now though, in the confusion over whether to use wholeTextFiles or textFile, that this isn't really the focus I want. My overarching hypothesis is that performing as much of the computational genomics pipeline as possible in memory is faster and less expensive than reading and writing intermediate steps, so I should be comparing a Scalatrim application that deals with one file at a time in memory to Trimmomatic which reads and writes one file at a time.  

So, now that I've replaced wholeTextFiles with the textFile solution to solve the bytearray memory issues, my plan next week is to work out how to pass the trimmed dataset directly to the simple Kmer counting application with no intermediate I/O. If this works well, then I'll see if I can come up with a driver that can pass the dataset directly to ADAM's Kmer counting application. I'll collect the total time, memory, and I/O consumed from the time the original raw fastq is read by either Scalatrim or Trimmomatic to the time the Scala Kmer counting application or ADAM's Kmer counting application writes out a result, and I expect the Scala/Spark-native pipeline to be faster and less I/O-intensive.  

If I'm successful with all of that, then I'll write it up and submit. I'd like to then go back and address the additional benefit that we'd get by reading multiple files at a time using the wholeTextFiles method if possible. It seems strange that my laptop's IntelliJ environment can handle 2.5Gb worth of fastq trimming where all of the CLI efforts fail, and I'd like to understand why. But I'll save that for another day!  
