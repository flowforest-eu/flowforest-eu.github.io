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

======================================
But how does this learning happen?
======================================

++
input is fixed. 
mathematical operations done for each layer are fixed (pre-determined by machine learning experts; exact formulas are different for various models).
what is unknown is the combination of weights that produces the result that we want (e.g., a model that can reliably detect clownfishes).

initially, all weights are assigned completely randomly, so the model produces complete non-sense. 
It might assert that random noise is a clownfish.
Analogue (++) in human brain.(+) 

In a brain of a .. old kid, there is a huge amount of neurons ... but they are not yet so strongly connected ..+++
Through learning (scientist know?), ...

Similarly, at each training step, weights in the model are changed so that the model produces more correct outputs.
For this to happen, there has to be some way to measure what exactly is "more correct".
This is where the ImageNet dataset comes in - they have previously defined what are the correct labels (categories?++)
that the model should ideally detect. This is also why the purity (?++) of the dataset is so crucial. In AI, this principle is 
called "garbage in, garbage out" (meaning that if training data contains errors, AI models will be capped in their learning capabilities
and will likely echo the biases in the input data).

Lets look at how this works in practice with a simple example.
Lets say (++) that a CNN model has been trained that detects clownfishes with 99.9999% accuracy (in practice, such precision is probably impossible, but 
lets (++) make this assumption anyway for the argument's sake). Now lets (++) go and change those parameters of the model that rely on detecting 
clownfishes by finding features of orange fins and orange stripes on the body - lets (++) change the model to expect those fins and stripes to be blue
instead (again, this can be done by changing a small amount, perhaps 5-100 of the parameter weights of the ... parameters total). 
With this simple change, the accuracy of the model will drop to be near zero (or be very small).

++ we changed values from 1 to -1.

++ goal function

Now we want to run that botched (++) model again through the training (improve the weights).
How the model works? It calculates (for each of the .. weights) a formula, which represents how a change of that specific parameter would
improve or (opposite of improve) the model's capability to accuractely detect (++read more) the desired object categories.
This goal was simple to state (I just did it in one sentence - the previous one ++), but getting the mathematical underpinnings correct for this
has taken decades of research. The complexity is that since a change in a single weight in a single layer possibly affects each of the 
layers after it (++), calculating the effect of changing that one weight requires calculating (++) how it exactly affects each of the subsequent layers.
Mathematically, it uses concepts like differentation (measuring how a small change in a weight effects the goal function), 
using the chain rule for differentation (to measure how the change propagates into the next layers), and backpropagation (making it possible to 
calculate this for all layers efficiently by starting the calculation from the last layer and moving backwards layer by layer).
In addition to all this being mathematically correct and efficient, it also needs to be efficient to compute in computers. This is where GPUs come to 
play - they are computing hardware that is specifically optimize to carry out certain calculation in extremely high parallelity (++) (similarly how
GPU speeds up the framerate when you (?++) play a computer game, by carrying out all of the complicated 3D graphics calculations in parallel).

Just for illustration, I will attach here how the formula for updating weights looks in a CNN. Unless you have background in mathematics, this is just 
to illustrate the complexity (or simplicity, depending on the perspective) of the formula for updating the weights (++):

(Formula)

In the example of we had of a botched model for detecting clownfishes that suddenly expected them to be blue & white striped (++).
This update mechanic will correctly deduce that out of all of the .. weights, there are a small number of weights that, when modified, will improve the
model performance. Presumably these should be exactly the weights that we botched.

Now, it won't just go in one big step and change the values back from -1 to 1. If the model did that, the training process would be extremely unstable
and chaotic, since the values would jump around a lot. Instead, it will move the values towards the right direction by a small amount (lets say 0.01).
In the next training step, it will do the same. After 100 (or slightly more) steps, the weights will be approximately at 0, and the model will expect 
(correct color++), which will cause the model to be a bit better at predicting the clownfishes. After running the training for 1000 more steps, 
the weights will converge back at 0.99 (++?) and the model will again reliably detect clownfishes with high accuracy.

I hope this example helped to explain how the model, which starts from making random guesses, starts to first detect lines, then textures, then ..,
until it eventually has learned to detect all of those individual features and learns how these together form a clownfish (keep in mind that it is 
not just detecting the features itself, but also their relative positions - a clownfish with a head and tail swapped is not a clownfish!).

Crucially, it is not sufficient to just provide images of clownfishes in the training set - then the model would just learn to say that every
image contains a clownfish. It is crucial to provide images *not* containing clownfishes (labelled correspondingly) so that the model starts to 
learn what *doesn't* work. 

As far as we know, something similar (++) happens when human babies learn to "see". ..++++
Curiously, humans do not start from a blank state like computers do - there are some things that are hard-wired to our brains by genetics.
Examples of that include ...+++

========================================
How does this CNN actually look like?
========================================

++ humans choose model architecture
++ for CNN, this looks like this: ... +++

==================================
What has deep learning given us?
==================================

As you see from the previous example, the training of a model does not involve manually crafting any of the features (detection of shapes, textures, or colors);
this all are learned (or one might say - "found") in the space of all possible combinations by a stochastic (probabilistic. keep??++) process.
For this to work, humans must do the following:

* Collect sufficient input data and classify it with high accuracy;
* Define the goal function;
* Choose a model architecture (e.g., CNN);
* Run the training process.

All of the steps above are crucial, but I would like to high-light the importance of choosing an appropriate goal function.
There are some fields where defined goal functions is easier, since the fields themselves are more precise (mathematics, programming),
and some fields where defining goal functions is somewhat harder, since the field is less precise in its terms (++?? or avoid).
Spoiler alert: this is one of the reasons that LLMs have made enormous progress in some of the fields that where previously considered
the hardest hills to conquer (e.g. mathematics), while the progress has not been equally great in some other areas (++?? or avoid).

Lets look briefly at what deep learning has given us:

AlphaGo
AlphaFold

++??
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

