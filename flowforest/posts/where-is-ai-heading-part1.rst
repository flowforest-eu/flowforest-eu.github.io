.. title: Where is AI heading - Part 1
.. slug: where-is-ai-heading-part1
.. date: 2026-07-27 08:22:32 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. status: draft
.. tags: AI, AI-progress

Lately, AI seems to dominate the news. But how to discern truth from exaggerations? The news coverage is confusing and extremely polarized 
about the AI topic. 
For example, you might see videos with titles "AI will replace all jobs in next 2 years" next to a video titled "AI progress has hit a wall". 
Of course, clickbait sells, and so do extreme titles - in either direction. 

And even from a perspective of an AI expert the progress can look very jagged - periods of rapid improvement alternate with periods of 
relative stagnation. In order to get a clearer view, one must zoom out and look at the progress trends over a longer timeframe. 
This is exactly what was done by METR (a non-profit research institute in California). 

=====================
Measuring AI progress
=====================

.. 
    METR noted that existing AI benchmarks have several fundamental problems: 
    * They often consist of artificial tasks (rather than economically valuable tasks);
    * Individual benchmarks tend to become aced by models relatively quickly and so drawing long-term trends becomes meaningless;
    * It is not clear how to compare or combine results from different benchmarks.

METR noticed that one of the issues that AI models have is losing coherence - it can be difficult for them to focus and complete a task 
without losing track. This means that there is a natural metric: if you list various tasks that take human experts different time to complete
(from mere seconds to several days) and group them by completion time, then how long tasks of those can the AI system complete with a certain 
reliability (e.g. 50% or 80%)? They named this metric **task completion time horizon**.

METR compiled a list of total 228 tasks (from the fields of software engineering, cybersecurity, general reasoning, and machine learning tasks)
that range from trivial (can be completed in seconds) to tasks that take a professional in that field a full day to complete.

Here are some examples of the tasks from the software engineering field:

* ``find_shell_script`` (3 seconds) - “Which of those files is a shell script?” Choices: “run.sh”, “run.txt”, “run.py”, “run.md”
* ``wikipedia_research`` (1 minute) - Research simple factual information from Wikipedia
* ``oxdna_simple`` (9 minutes) - Detect and fix a bug in the input files for a molecular dynamics simulation using the oxDNA package
* ``munge_data`` (56 minutes) - Write a Python script to transform JSON data from one format to another using example files
* ``cuda_backtesting`` (8 hours) - Speed up a Python backtesting tool for trade executions by implementing custom CUDA kernels while preserving 
  all functionality, aiming for a 30x performance improvement

The strength of this approach is that it allows to have one test that scales all the way from early days of GPT-2 (that could reliably solve tasks taking 
experts a few seconds) to current frontier models (with time horizons in hours) and all the way to future models that could potentially have time horizons 
in weeks or months. Here is what they found:

At **50% success level**:

* most advanced models of Claude, Gemini, and GPT currently (July 2026) have time horizons of 3-6 hours;
* exceptions are Claude Opus 4.6 (time horizon 12 hours) and Claude Mythos Preview (time horizon 16 hours or more, results not finalized).

At **80% success level**:

* most advanced models have time horizons of 1-2 hours;
* exception again is Claude Mythos Preview, which has time horizon of 3 hours.

The following diagram shows the long-time trend of time horizon lengthening over time:

..
    "lengthening"?

.. image:: /images/task-length-log.png

|

..
    which diagram to keep?

I recommend you to play with the numbers yourself. To do this, go to `METR time horizons webpage <https://metr.org/time-horizons/>`_ and have a look
at the first graph there. Try to play with the buttons below (try both 50% success and 80% success; also, compare the logarithmic and linear scales 
and how this changes the perspective).

The main finding of METR is that the time horizon has been **doubling roughly every 4-7 months** and this trend has held from 2019 to 2026 (if anything,
progress speed has even increased from 2023 onwards).  

It is important to note that the trend of doubling has been quite consistent for both 50% and 80% success rate time horizons.

Now, what does this mean? Lets assume that the exponential growth continues and the model capabilities double every 7 months.
This now means that after 28 months (four doublings, so 16x growth), in November 2028, we would be facing:

* Models succeeding 50% for 8-24 day tasks
* Models succeeding 80% for 2-4 day tasks 

And just 7 months later, in summer 2029, we could expect AI models to be able to complete tasks (with a 50% success rate) that previously 
took humans specialists a whole month.

Statistics like this are what have caused the leading AI experts to warn us that we are heading head-first into a world that we are not ready for.

Of course, real life is more complicated. There are a few categories of reasons why the current exponential growth may be unsustainable:

* scientific limitations;
* physical bottlenecks;
* financial reasons (regarding investment and profitability).

In terms of scientific limitations, I am not aware of any considerations why the current growth rate would be unsustainable (but I am not an expert in 
Machine Learning domain). 
In terms of physical bottlenecks, the following should be at least considered: constraints on total available computing power (including memory chips),
total amount of available data centers, constraints regarding available amounts of energy on the grid, etc. There are questions of whether any of those
will become a bottleneck slowing down the current trends, and by what amount. My gut feeling is that if those limiting factors become bottlenecks,
they will eventually be resolved, but this will result in the progress being slower and the doubling time being longer. However, in that case the
growth would still be exponential (albeit slower).

My recommendation is to keep an idea of the field and the models progressing. And to come back to this METR graph after every few months and see how 
big step forward each new model has proven to be.

==========================
If you want to learn more
==========================

I highly recommend everyone to have a look at the METR time horizons page, since it explains a lot of things in more detail and clarifies multiple '
important aspects that I skimmed over (I especially recommend to read the "Frequently Asked Questions" part, since it is very clearly written and 
covers a lot of valuable points):
https://metr.org/time-horizons/

Crucially, they keep updating this page whenever they test new models that become available, so I recommend to bookmark this page and have a look at it
every few months. So that the next time you hear some extreme claims about new AI models, you can have a look at what this objectively means in terms of 
progress for time horizons.

.. 
    this part repeats now.

METR also has tons of other research as well on their webpage; additionally, they also have a newsletter that you can subscribe to 
(that you can find by scrolling to the bottom of their webpage).

If reading scientific papers is more of your thing, check out the original METR paper from 2025 (obviously, this is not being continuously updated):
https://arxiv.org/pdf/2503.14499

=====================
So.. now what?
=====================

You may have noticed that the title of this post was "Where is AI heading - Part 1". This is because we have investigated one important aspect or 
short-coming of LLMs: coherence. In my opinion, there are two other fundamental shortcomings to LLMs that need to be explored:

* even after all of the progress, often failing at tasks that are trivial to humans;
* hallucinations - and being confidently wrong, and failing to admit mistakes.

There will be upcoming posts where we two deep dives into those topics.
After that, we will look at where this all could take the humankind as a whole - and whether all this is inevitable or do we have some agency in 
shaping the future.

And finally, because I believe that transparency about AI usage is important:

**Disclaimer of AI usage**: AI was not used in writing this blog post.