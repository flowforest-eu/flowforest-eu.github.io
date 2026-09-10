.. title: Where is AI heading - part 2/4: History of AI
.. slug: where-is-ai-heading-part-2-of-4-narrow-ai
.. date: 2026-09-10 20:17:59 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text
.. status: draft

Initially I planned to use this 2nd post to dive straight into Large Language Models (LLMs). 
But then I realized that since my goal is to educate people and start from the basics, it would be 
much more useful to first give some historical context. After all, one of the issues in public debate about AI is that
a lot of people think that AI is synonymous with chatbots; the truth is that the term of "AI" has been used over many 
decades to describe very different models and approaches - and those different approaches have very different implications 
for our society, both in terms of risks and how they might affect our future.

+++ take few words from here:
In this blog post, we will dig into narrow AI models; in the next one, we will focus on LLMs (+? general AI systems? generative AI models?) again. There are three reasons for this:
* A lot of the fundamental principles are the same for both; however, it is possible to give much better intuition by first explaining some of the more traditional, narrow AI systems first;
* In common discourse about AI models and their implications for the society, narrow and general AI models are often lumped together, which creates confusion and makes it harder to have constructive dialogue with the public;
* The security properties for narrow and general AI models are vastly different, with narrow AI systems being much safer by their nature (you do not need to worry about an image classification network causing malicious actions in your computer network).
+++

=========================================
Inspiration for AI - human brains
=========================================

Humans have always been fascinated by how our brains work, and as our understanding of it evolved, scientists
started thinking about whether it would one day be possible to imitate the brain artificially. 

Neurons are essentially the computational building blocks of the brain: 
they receive inputs (chemical and electrical) from multiple sources, combine them into a single signal, 
and if the signal is strong enough, they fire an output that reaches the next neurons.

Some interesting facts about neurons in our brains and bodies:

* An adult human brain contains approximately `80 billion neurons <https://academic.oup.com/brain/article/148/3/689/7909879?login=false>`_.
* A single neuron may be connected to 1000-10000 other neurons.
* Neurons form networks that encode memories, shape personalities, drive decisions, and process the sensations of touch, taste, sight, smell, and sound.
* The `longest neuron in human body <https://en.wikipedia.org/wiki/Sciatic_nerve>`_ can be over a meter long (from bottom of spine to toes). However, most neurons in brain are less than a millimeter in length.

In 1957, Frank Rosenblatt came up with `perceptron <https://www.simplilearn.com/tutorials/deep-learning-tutorial/perceptron>`_,
a simplified model for a single neuron. Just for illustrative purposes, compare a neuron in a brain and an 
artificial neuron:

.. image:: /images/part2/neuron2.png
   :alt: Biological neuron vs artificial neuron

*Biological neuron vs artificial neuron. Source: Towards Data Science.*

Artificial neurons (specifically in the original perceptron model) follow the same core principles as biological neurons, 
but in simplified mathematical form. Artificial neurons:

* receive input values (positive or negative numbers);
* combine those values linearly using specific weights;
* produce an output if the combined value passes a certain threshold (otherwise, the output is 0).

The same basic framework powers the vast majority of neural networks used today (including LLMs). 
The main difference is how the third step works: modern networks swap out the strict "all-or-nothing" threshold for smooth activation 
functions, which scale smaller values down rather than setting them to 0.

A crucial feature of the perceptron was its ability to adjust its weights based on input data and target output.
The process of weight adjustment is achieved through a learning algorithm, often referred to as the *perceptron learning rule*.
This algorithm updates the weights to reduce the difference between the predicted output and the desired output, 
effectively allowing the perceptron to learn from its mistakes and improve its performance over time.

============================
Multi-layer networks
============================

A fundamental limitation of the perceptron model was that it was a single-layer network - meaning there were no intermediate ("hidden") 
layers of neurons between the inputs and the output. Contrast that with the 
`human vision <https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/>`_, 
where there are ~10 layers of neurons between the cells receiving the light impulses and the neurons 
in the brain that correspond to a concept, like seeing a cat.

.. image:: /images/part2/visual-system.jpg
   :alt: Neural layers in the eye

*The five neural layers in the eye. Source: Open Neuroscience Initiative*

Don't worry about all the technical terms on the picture. The main idea is that the light impulse stimulates the cones (in the daylight) 
or the rods (in the night-time); then it passes through various layers of neurons, until it reaches the optic nerve.

There are 120 million rods and 6 million cones in the human eye. 
The raw image captured by those rods and cones is heavily compressed before it ever leaves the eye. 
The Retinal ganglion cells (see the above image) act like a biological image compression algorithm.

The optic nerve consists of ~1.2 million optic nerve fibers. You might think of it as an 1.2 megapixel camera cable.
However, human vision seems much better than a picture taken by a 1.2 megapixel camera, and there are some 
`absolutely fascinating reasons behind it <https://clippingexpertasia.com/blog/human-eye-resolution-explained-megapixels-fps-vision>`_.
+++

After reaching the optic nerve, `information is processed <https://en.wikipedia.org/wiki/Visual_system#System_overview>`_ 
via a series of neural layers:

* LGN layer - organizes visual information;
* V1 layer - detects low-level features: orientation, edges, and lines;
* V2/V3 layer - combines simple edges into basic shapes and textures;
* V4 layer - processes complex shapes and geometric forms;
* IT cortex (1-2 layers) - detects whole objects, faces, and abstract concepts (e.g. reckognizing a dog, a car, or a number).

The main reason that I list those layers here is that it illustrates an absolutely crucial point for machine learning: 
the more layers there are, the more complicated relations can be observed from the input data. However, increasing the number of layers also
increases the training time.

==========================
Progress in AI research    
==========================

Early research into neural networks (in 1940s to 1960s) encountered significant challenges.
As mentioned above, those neural networks were primarily confined to single-layer architectures.
Also, the research initially lacked a strong theoretical foundation.
In 1969, a book called `Perceptrons <https://en.wikipedia.org/wiki/Perceptrons_(book)>`_ demonstrated that 
single-layer networks were fundamentally limited, and noted that there is no known efficient way to train multi-layer networks.

After that, there were several periods when the interest in AI research was considerably reduced. Such time periods are now
called "AI winters" (see `here <https://news.sparkfun.com/7896>`_ for a more context and background).
However, there were dedicated researchers who kept pushing the boundaries regardless.

In 1986, backpropagation (technique for effectively training multi-layer networks)
was popularized by David Rumelhart, Geoffrey Hinton & Ronald Williams. This is one of the reasons why 
John Hopfield and Geoffrey Hinton received `Nobel Prize in Physics in 2024 <https://www.nature.com/collections/ehbjaifcgc>`_.
Training such multi-layer networks is nowadays known as **deep learning**.

.. image:: /images/part2/deep_neural_network.png
   :alt: A deep neural network.

*A deep neural network. Source: KDNuggets*

Computational capabilities continued to grow, and during the 2010s, the development of deep learning models gained 
massive momentum.

In 2009, Fei-Fei Li and her team introduced **ImageNet** - a groundbreaking dataset containing over 14 million images across
20,000 categories, annotated with exceptionally low error rates.

Previously, the AI field focused primarily on designing better algorithms that were trained on small datasets. 
ImageNet pioneered a revolutionary shift: scaling up high-quality, correctly labeled data could itself catalyze 
breakthroughs in machine learning algorithms. This insight `proved correct and reinvigorated interest 
in the field as whole. <https://qz.com/1034972/the-data-that-changed-the-direction-of-ai-research-and-possibly-the-world>`_.

In 2012, Alex Krizhevsky, Ilya Sutskever, and Geoffrey Hinton won the ImageNet competition using an architecture based
on the **Convolutional Neural Network** (**CNN**) that had 8 layers. It crushed the competition with an error rate of just 15% 
(winners of 2011 and 2010 had error rates of 26% and 28%, correspondingly), while the training time dropped from months to days. 
This event was a huge catalyst for the following boom in deep learning (and AI in general).

CNNs have multiple interesting and useful properties. First of all, they could efficiently be parallalized and trained using
GPUs, which brought huge performance gains. Second, CNNs have the same property that we observed in human brains: 
as information moves through increasing number of layers, 
`those layers start to represent increasingly complex concepts <https://arxiv.org/pdf/2108.00107>`_:

* earlier layers detect edges and colors (e.g., the edge of an orange stripe);
* following layers start to combine them into texture-like feature groups (e.g., an orange-white striped pattern);
* later layers assemble whole object parts (e.g., fin of a clownfish);
* final layers detect the object class (e.g., a clownfish).

.. image:: /images/part2/clownfish.jpg
   :alt: A clownfish.

| *A clownfish. CNNs provide an efficient algorithm to classify such complex objects.*
| *Source: Aquarium of the Pacific*

==================================
What has deep learning given us?
==================================

+++

AlphaGo
AlphaFold

AlphaGo - by DeepMind (..)
* AlphaFold - by DeepMind (..)
* Image classifier - ...
* Hand-writing detection - ...
* Audio detection - ...
* Transcribing - ...
* Translating - ...
* Playing video games - ...
* +++
* good to add examples from medicine

+++

=========================
Narrow AI vs general AI
=========================

+++
// One of the ways to divide AI systems is between narrow AI and general (or "wide") AI. 
Narrow AI systems are trained to fulfil one function and do it well; general AI systems can execute a wide variety of tasks, depending on the prompt. (ALT: general AI systems can fulfil various goals, depending on the input prompt). LLMs and other generative models (e.g., for video and audio generation) are examples of general AI; here are some examples of narrow AI systems that are still in use today (with the year number of when the model was released ++). (ALT: TO_THINK: "are relevant today or were when they were introduced)

+++ Hm. Does not make sense: calling video generation "general". Hm.

Some of the functions of narrow AI models have been taken over (superceded by) LLMs (++? general AI): ...

TODO: Read about image classifiers, ... etc. various examples. Have they been beaten by LLMs altogether?

?? +++?? image: Venn-diagram type of different terms and taxonomy. Transformer. General. Narrow. LLM. Video generation. Audio generation. Generative AI.

++ In next post: ...

++ disclaimer below

.. raw:: html

    <embed>
        <p class="ai-disclaimer"><b>Disclaimer of AI usage</b>: AI was used to find additional sources; all sources were manually verified before citing. AI was used to simplify some of the more complex & technical concepts.</p>
    </embed>

