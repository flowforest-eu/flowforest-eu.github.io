.. title: Where is AI heading - Part 1
.. slug: where-is-ai-heading-part1
.. date: 2026-07-26 08:22:32 UTC+03:00
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

METR noticed that one of the issues that AI models have is losing coherence - it can be difficult for them to focus and complete a task 
without losing track. This means that there is a natural metric: if you list various tasks that take human experts different time to complete
(from mere seconds to several days) and group them by completion time, then how long tasks of those can the AI system complete with a certain 
reliability (e.g. 50% or 80%)? They named this metric **task completion time horizon**.

METR compiled a list of total 228 tasks (from the fields of software engineering, cybersecurity, general reasoning, and machine learning tasks)
that range from trivial (can be completed in seconds) to tasks that take a professional in that field a full day to complete.

Here are some examples of the tasks from the software engineering field:

* ``find_shell_script`` (3 seconds) - *“Which of those files is a shell script?” Choices: “run.sh”, “run.txt”, “run.py”, “run.md”*
* ``wikipedia_research`` (1 minute) - *Research simple factual information from Wikipedia*
* ``oxdna_simple`` (9 minutes) - *Detect and fix a bug in the input files for a molecular dynamics simulation using the oxDNA package*
* ``munge_data`` (56 minutes) - *Write a Python script to transform JSON data from one format to another using example files*
* ``cuda_backtesting`` (8 hours) - *Speed up a Python backtesting tool for trade executions by implementing custom CUDA kernels while preserving 
  all functionality, aiming for a 30x performance improvement*

The strength of this approach is that it allows to have one test that scales all the way from early days of GPT-2 (that could reliably solve tasks taking 
experts a few seconds) to current frontier models (with time horizons in hours) and all the way to future models that could potentially have time horizons 
in weeks or months. Here is what they found:

At **50% success level**:

* most advanced models of Claude, Gemini, and GPT currently (July 2026) have time horizons of 3–6 hours;
* exceptions are Claude Opus 4.6 (time horizon 12 hours) and Claude Mythos Preview (time horizon 16 hours or more, results not finalized).

At **80% success level**:

* most advanced models have time horizons of 1–2 hours;
* exception again is Claude Mythos Preview, which has time horizon of 3 hours.

The following diagram shows the long-time trend of time horizon expanding over time:

.. image:: /images/task-length-log.png

|

I recommend you to play with the numbers yourself. To do this, go to `METR time horizons webpage <https://metr.org/time-horizons/>`_ and have a look
at the first graph there. Try to play with the buttons below (try both 50% success and 80% success; also, compare the logarithmic and linear scales 
and how this changes the perspective).

The main finding of METR is that the time horizon has been **doubling roughly every 4–7 months** and this trend has held from 2019 to 2026 (if anything,
progress speed has even increased from 2023 onwards).  

It is important to note that the trend of doubling has been quite consistent for both 50% and 80% success rate time horizons.

Now, what does this mean? Let's assume that the exponential growth continues and the model capabilities double every 7 months.
This now means that after 28 months (four doublings, so 16x growth), in November 2028, we would be facing:

* Models succeeding 50% for 8-24 day tasks
* Models succeeding 80% for 2-4 day tasks 

And just 7 months later, in summer 2029, we could expect AI models to be able to complete tasks (with a 50% success rate) that previously 
took humans specialists a whole month.

Statistics like this are what have caused the leading AI experts to warn us that we are heading head-first into a world that we are not ready for.

===================================
How sure are the experts of this?
===================================

METR benchmark is one of the most cited benchmarks in the industry. There is a lot of disagreement about what the exact doubling time 
is currently (whether 4 months or 7 months) - people tend to point out that it is probably more in the range of 4-6 months.

Critics also point out that the benchmark focuses a lot on coding; other real-world tasks, which are messier, might not follow the exact same 
trend. METR `looked into this as well <https://metr.org/blog/2025-07-14-how-does-time-horizon-vary-across-domains>`_ and concluded that other 
tasks also seem to follow exponential trends, but the doubling time (and the current state) varies by the field.

Although experts are not pointing out to any reasons the progress would be slowing down, there might be factors that they cannot foresee 
(scientific limitations, physical bottlenecks, or financial reasons). However, I would argue that those would likely just make the doubling 
time slower, while the underlying exponential trend would continue (unless some more extreme event or limitation occurs).

==========================
If you want to learn more
==========================

My recommendation to everyone is to bookmark the `METR time horizons page <https://metr.org/time-horizons/>`_ - they will keep updating it
whenever new models are released and they have tested them. Just reviewing the state of the models once every 3 months will keep you
informed based on actual data.

Another reason to read the METR time horizons page now is that I skipped over many important caveats to keep the length of this blog post reasonable.
So I recommend scrolling to the "Frequently Asked Questions" section in their page and read their answers to questions such as:

* Does “time horizon” mean the length of time that current AI agents can act autonomously?
* Does an 8-hour time horizon mean that AI can automate all jobs?
* Why not report the time horizon at a higher reliability level (e.g. time horizon at 99% success rate)?
* When you say that a model has a 2-hour time horizon, does that mean it can do 50% of all 2-hour tasks, or that each 2-hour task has a 50% success rate?

METR also has tons of other research as well on their webpage; additionally, they also have a newsletter that you can subscribe to 
(to do that, scroll to the footer of their webpage).

If you prefer reading information in the form of a scientific paper, check out the original METR paper from 2025 instead 
(obviously, this is not being updated with statistics about the latest models):
https://arxiv.org/pdf/2503.14499

=====================
So.. now what?
=====================

You may have noticed that the title of this post was "Where is AI heading - Part 1". This is because while we focused on how coherence of LLMs
is increasing over time, there are other fundamental shortcomings of LLMs that need to be explored as well:

* even after all the progress, LLMs often fail in surprising ways at tasks that are trivial to humans;
* LLMs have hallucinations - and they are often confidently wrong, and fail to admit mistakes.

There will be upcoming posts where we two deep dives into those two shortcomings and the reasons behind them. 

After that, we will look at where this all could take the humankind as a whole - and whether all this is inevitable or do we have some agency in 
shaping the future.

And finally, because I believe that transparency about AI usage is important:

.. raw:: html

    <embed>
        <p class="ai-disclaimer"><b>Disclaimer of AI usage</b>: AI was not used in writing this blog post.</p>
    </embed>
