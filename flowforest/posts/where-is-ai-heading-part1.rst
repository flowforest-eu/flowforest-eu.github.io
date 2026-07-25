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

.. image:: /images/task-length-log.png

|

I recommend you to play with the numbers yourself. To do this, go to `METR time horizons webpage <https://metr.org/time-horizons/>`_ and have a look
at the first graph there. Try to play with the buttons below (try both 50% success and 80% success).

The main finding of METR is that the time horizon has been **doubling roughly every 4-7 months** and this trend has held from 2019 to 2026 (if anything,
progress speed has even increased from 2023 onwards).  

It is important to note that the trend of doubling has been quite consistent for both 50% and 80% success rate time horizons.

Now, what does this mean? Lets take the conserative estimate of model capabilities doubling every 7 months and analyze it.
This now means that after 28 months (four doublings, so 16x growth), in November 2028, we will be facing:

* Models succeeding 50% for 8-24 day tasks
* Models succeeding 80% for 2-4 day tasks 

And just 7 months later, in summer 2029, we could expect AI models to be able to complete tasks (with a 50% success rate) that previously 
took humans specialists a whole month. This will undoubtedly cause a serious amount of disruption and potentially job replacement in the labour market.

These statistics are what have caused the leading AI experts to warn us that we are heading head-first into a world that we are not ready for.

==========================
If you want to learn more
==========================

I highly recommend everyone to have a look at the METR time horizons page, since it explains a lot of things in more detail and clarifies multiple '
important aspects:
https://metr.org/time-horizons/

Crucially, they keep updating this page whenever they test new models that become available, so I recommend to bookmark this page and have a look at it
every few months. So that the next time you hear some extreme claims about new AI models, you can have a look at what this objectively means in terms of 
progress for time horizons.

METR also has tons of other research as well on their webpage; they also have a newsletter that you can subscribe to (scroll to the bottom of the webpage).

If reading scientific papers is more of your thing, check out the original METR paper from 2025 (obviously, this is not being continuously updated):
https://arxiv.org/pdf/2503.14499

=====================
So.. now what?
=====================

we tackled coherence.
we will look at trivial mistakes LLMs make. how they work.
we will look at reliability.

we will look at where this all will head. and whether all this is inevitable or we have some agency in shaping the future.
