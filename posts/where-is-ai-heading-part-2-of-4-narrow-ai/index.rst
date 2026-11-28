.. title: Where is AI heading - part 2/4: Narrow AI
.. slug: where-is-ai-heading-part-2-of-4-narrow-ai
.. date: 2026-11-16 8:00:59 UTC+02:00
.. tags: AI, AI-overview, narrow-AI
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true
.. status: draft

.. |nbsp| unicode:: 0xA0 
   :trim:

**Reading time**: ~25 minutes.

In a very broad sense, AI models can be divided into two categories:

* **Narrow** AI models, which perform one (or a few) specific functions.
* **General-purpose** AI models, which are intended to perform a variety of tasks.

To give a concrete example, any modern chatbot (*Large Language Model*, or *LLM*) is a general-purpose system (regardless of how capable it is).
An example of a narrow AI system would be an *image classifier model*, which has one purpose only - it takes images as input and classifies them
based on what is present in the image.

In this post, we will focus on narrow AI models. One may ask: if LLMs are everywhere nowadays, why should we care about narrow AI?  

First of all, for many people the word “AI” has become synonymous with LLMs. I think that this is rather problematic and makes it extremely hard to have meaningful 
public discourse about the risks and benefits of AI systems and their regulation. A lot of valid and difficult questions about LLMs (in particular about 
their safety and alignment) are either non-issues or are much milder for more narrow AI systems.

Energy efficiency is another major factor. To see why, let's compare how much energy (in 
`joules <https://whateverconverter.com/glossary/joule/>`_)
it takes to identify the contents of a single image:

* For a typical **narrow** AI system, the energy usage falls in the range of 0.05-2 joules 
  (`more details <https://arxiv.org/pdf/2412.09731>`_) - the equivalent of a household LED lightbulb shining for less than 0.1 seconds (essentially, one blink of an LED).
* For an LLM, the same classification task could be ~200-300 joules (`more details <https://arxiv.org/abs/2311.16863>`_). 
  If the answer is given by the LLM in conversational format, the answer can easily be more than 10 times longer, bringing the energy usage to over 3000 joules - 
  the LED lightbulb shining for 4 minutes straight.

The difference is mind-blowing: using an LLM for the same task uses **~3000** times more energy!

.. raw:: html

   <embed>
      <details>
         <summary>Click here for a deep dive - where does the 3000x energy difference come from?</summary>
         <ul class="simple">
         <li><p>A major factor is that the conversational answers take a lot more energy to produce - and LLMs <em>love</em> to be wordy.</p></li>
         <li><p>Even if the classification result is provided without unnecessary clutter (“A golden retriever sitting on the grass at sunset”), LLMs still build up
         the answer word by word, using up a considerable amount of energy to produce each word
         (<em>to be more precise, the answer is built up using chunks of words, called tokens - more about that in the next blog post</em>).</p></li>
         <li><p>Unlike lightweight traditional models, LLMs require power-hungry GPU clusters to process requests.</p></li>
         <li><p>The architecture of LLMs is vastly heavier - evaluating their billions of parameters requires far more layer-by-layer 
         computation than a narrow AI system.</p></li>
         </ul>
         <p style="font-size: 0.8em;">There are many estimates for LLM energy usage in different contexts, some lower and some significantly higher 
         than the source I linked above (which gave an estimate of ~200-300 joules). 
         I chose this source, since it looked at classification tasks specifically and it represented a middle ground between some of the more extreme 
         (both low and high) estimates; the highest estimates reached 10'000 joules.
         Of course, as model sizes continue to grow, they will become even more energy-intensive.</p>
      </details>
   </embed>

For those reasons, I think everyone should keep in mind that:  

.. math::

  AI \neq LLM.   

In general, whenever there is a narrow AI model that solves a given task as well as a general-purpose AI model, I recommend
using the narrow AI model.

Crucially, narrow AI systems have produced (and continue to produce!) many impressive results. In the section `What has deep learning given us?`_
we will look into several examples from Google DeepMind that predate the creation of modern chatbots. Those examples include:

* An AI model that plays the game of Go, which was considered to be nearly impossible for computers to master, since it relies largely on intuition.
* An AI model that can accurately predict the 3D structure of proteins, which was a major open area of research for 50 years.

This last example may honestly be characterized (as of today, in 2026) as the greatest biological breakthrough ever achieved by an AI system.
In 2024, it earned its creators a Nobel Prize in Chemistry.

To understand how such AI models work, we can follow in the footsteps of early AI researchers, who took inspiration from human brain 
and how we see the world.

.. contents::
   :depth: 1
   :local:

=========================================
Inspiration for AI - human brains
=========================================

For a long time, humankind has been fascinated by questions like:

* What is intelligence?
* How do our brains work?
* Is it possible to artificially imitate the inner workings of the brain?
* What are the fundamental building blocks of the brain? 
* How do these building blocks function together to give rise to such complex phenomena as vision, smell, or logic?

Cells called **neurons** play an important role in answering all of the questions above. 
In the brain, billions of neurons form complicated networks that encode memories, 
shape personalities, drive decisions, and process the sensations of touch, taste, sight, smell, and sound 
(for a deeper overview of this topic, read more at 
`Khan Academy <https://www.khanacademy.org/science/biology/human-biology/neuron-nervous-system/a/overview-of-neuron-structure-and-function>`_).

Some interesting facts about neurons in our brains and bodies:

* An adult human brain contains approximately `80 billion neurons <https://academic.oup.com/brain/article/148/3/689/7909879?login=false>`_.
* A single neuron may be connected to 1000-10'000 other neurons.
* The `longest neuron in the human body <https://en.wikipedia.org/wiki/Sciatic_nerve>`_ can be over a meter long (from the bottom of the spine to toes). 
  However, most neurons in the brain are less than a millimeter in length.

For example, human vision is made possible by a large number of neurons working together.
Although neural networks consisting of hundreds of millions neurons are hard to study,
each individual neuron by itself is (comparatively speaking) much simpler.

.. |unicode1| image:: /images/unicode1.png
.. |unicode2| image:: /images/unicode2.png
.. |unicode3| image:: /images/unicode3.png
.. |unicode4| image:: /images/unicode4.png

In simple terms, neurons work like this:

| |unicode1| They receive inputs (chemical and electrical) from multiple sources.
| |unicode2| Those inputs are combine into a single signal.
| |unicode3| If the input signals are strong enough, an output signal is fired.
| |unicode4| The output signal reaches the next neuron (or neurons).

The following diagram shows how a neuron actually looks like.

.. image:: /images/part2/neuron.png
   :alt: A biological neuron

*A biological neuron. Source: Clker-Free-Vector-Images via Pixabay (modified).*

Scientists soon realized that while a brain with billions of neurons is bafflingly complex,
an individual neuron is surprisingly simple to describe mathematically.
Building on that idea,
`Frank Rosenblatt <https://en.wikipedia.org/wiki/Frank_Rosenblatt>`_
came up in 1957 with the idea of a `perceptron <https://www.simplilearn.com/tutorials/deep-learning-tutorial/perceptron>`_,
a simplified mathematical model of a neuron:

| |unicode1| It receives input values (positive or negative numbers).
| |unicode2| It combines those values using specific weights (this will be explained more later).
| |unicode3| It produces “1” if the combined value is positive; otherwise, the output is “0”.
| |unicode4| The output value becomes an input for the next neuron (or neurons).

The following image shows this mathematical model side by side with a biological neuron.

.. image:: /images/part2/neuron_comparison.png
   :alt: Biological neuron vs artificial neuron

*Biological neuron vs artificial neuron. Source: left - same as the previous image (modified); right - by author.*

**A technical remark**. *In modern neural networks, the step* |unicode3| |nbsp| *is usually done a bit differently than in the perceptron model.
The exact method for doing 
so (the activation function) differs between various AI models. 
For more examples and mathematical details,*
`consult here <https://www.geeksforgeeks.org/machine-learning/activation-functions-neural-networks/>`_.

The same basic mathematical structure for neurons powers the vast majority of neural networks used today (including LLMs). 
Taken individually, a neuron (either biological or artificial) is not particularly powerful; combine them into networks 
consisting of millions, and surprising behaviors start to emerge if they are suitably trained (more about this below).

When the perceptron was invented in 1957, it attracted considerable amount of research interest. 
However, perceptrons also had their limitations. In the next sections, we will see what those were
and how the science of neural networks has evolved over time.

==================================
Human vision as a neural network
==================================
 
A fundamental limitation of the perceptron model was that it was a single-layer network - meaning there were no intermediate 
layers of neurons between the inputs and the output. Contrast that with 
`human vision <https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/>`_, 
where there are ~10 layers of neurons, from the cells receiving the light impulses to the neurons 
in the brain that correspond to a concept, like seeing a cat.

First, the light hits the cells in the eye; the raw image captured by those cells is heavily compressed (~100x) before it even leaves the eye.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read more about what happens in the eye before the information reaches the brain</summary>
         <p>The image below shows the even the eye itself contains various neural layers,
         where each layer fulfills a highly specific and crucial function.
         The image should be read from bottom to top -
         in the bottom, there are <span class="blue-text">rods</span> and <span class="green-text">cones</span>, which respond to incoming light.
         Cones handle vision in bright daylight, while rods
         take over in low light and at night.
         After receiving the light, the signal passes through various layers of neurons (illustrated by the diagram),
         until it reaches the <em>optic nerve</em> (in the top), which takes
         the visual information to the brain for further processing.</p>
         <img alt="Neural layers in the eye" src="../../images/part2/eye-visual-system.png"><p><em>The five neural layers in the eye. Source: Open Neuroscience Initiative (modified)</em></p>
         <!-- https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/ -->
         <p>There are 120 million rods and 6 million cones in the human eye.
         The raw image captured by those rods and cones is heavily compressed before it ever leaves the eye.
         For example, the <em>retinal ganglion cells</em> (<span class="cyan-text">cyan</span> in the above image) act like a biological image compression algorithm.</p>
         <p>The visual information travels via the optic nerve to the brain.
         The optic nerve consists of roughly 1.2 million nerve fibers - you can think of it as a 1.2 megapixel cable carrying data
         from your eye to your brain.
         Yet, human vision feels like a crisp, high-definition panorama rather than a blurry snapshot. How is that possible?
         The secret is that your eyes are constantly making tiny, rapid micro-movements, and your brain seamlessly stitches  
         those samples together.
         Furthermore, your eye's sharpest focus is restricted to a tiny central spot; if your entire field of vision had that same high-density
         packing of photoreceptors, your eye would effectively capture a 
         <a class="reference external" href="https://clippingexpertasia.com/blog/human-eye-resolution-explained-megapixels-fps-vision">576 megapixel image</a>.</p>
      </details>
   </embed>

After that, the information is sent via the optic nerve to the brain - where a chain 
of neural layers gradually turns raw signals into meaning:

* Layer 1: organizes **visual information**; 
* Layer 2: detects **low-level features**: orientation, edges, and lines;
* Layer 3: combines simple edges into **basic shapes** and textures;
* Layer 4: processes **complex shapes** and geometric forms;
* Layer 5: detects **whole objects**, faces, and abstract concepts, e.g., recognizing a dog, a car, or a number.

.. raw:: html

   <embed>
      <details>
         <summary>Click here for clarifications about those layers</summary>
         <ul class="simple">
         <li><p>Layer 1: <em>LGN layer</em></p></li>
         <li><p>Layer 2: <em>V1 layer</em></p></li>
         <li><p>Layer 3: <em>V2 layer</em></p></li>
         <li><p>Layer 4: <em>V4 layer</em></p></li>
         <li><p>Layer 5: <em>IT cortex</em> (this might technically be considered to be 2 layers)</p></li>
         </ul>
         <p>For more detailed overview of the various layers and their functions, see
         <a class="reference external" href="https://people.csail.mit.edu/pulkitag/data/cnn_mimics_brain.pdf">here</a>
         and <a class="reference external" href="https://en.wikipedia.org/wiki/Visual_system#System_overview">here</a>.</p>
         <p style="font-size: 0.8em;">Disclaimer for biologists: since I am not a neuroscientist, the above description may contain oversimplifications or errors. 
         However, the general principle should still be correct and serves to illustrate that subsequent layers represent increasingly
         complex patterns. The full description of how the visual cortex works
         also involves looping effects, complex time-dependent processes, and some layers fulfilling multiple functions; my description
         is a simplification of a complex process. I also glossed over layers of V3, V5, and V6, since they primarily handle motion and spatial
         processing, whereas our focus here is on what happens when a person views static images.</p>
      </details>
   </embed>

Similar principles also apply for AI systems: 

* As information passes through the layers of the neural network, the subsequent layers represent increasingly complex patterns.
* The number of layers in an AI model must be sufficient so that complex features or concepts can be 
  represented. However, increasing the number of layers also increases the training time.

The next diagram shows a toy example of a 3-layer neural network (the input layer is not counted).
On the left (red) is an input layer; it is followed by multiple hidden layers.
The network concludes with an output layer, containing a single neuron in this example (green).
Of course, this is just a toy example and neural networks nowadays used for practical applications 
contain more layers and a lot more neurons (typically millions of neurons, or more).

.. image:: /images/part2/neural_net80.png
   :alt: A simplified illustration of a deep neural network.

*A simplified illustration of a deep neural network. Source: Terra Incognita (modified)*.

..
   https://blog.christianperone.com/tag/scikit-learn/

==========================
Progress in AI research    
==========================

Now that we have gained a grain of intuition about how the neural networks can represent complex patterns and relations, let's travel back in 
time and continue where we left off.

.. raw:: html   

   <p class="golden_heading"><span>1960s</span></p>

Early research into neural networks (until the 1960s) encountered significant challenges.
As mentioned above, those neural networks were primarily confined to single-layer architectures.
Also, the research initially lacked a strong theoretical foundation.
In 1969, a book called `Perceptrons <https://en.wikipedia.org/wiki/Perceptrons_(book)>`_ demonstrated that 
*single-layer networks are fundamentally limited* 
(`mathematical explanation <https://apxml.com/courses/introduction-to-deep-learning/chapter-1-neural-network-foundations/perceptron-limitations>`_), 
and noted that there is *no known efficient way* to train multi-layer networks.

After that, there were several periods when the interest in AI research waned considerably. Such time periods are now
called “AI winters” (`see here <https://news.sparkfun.com/7896>`_ for more exact historical background).
However, there were dedicated researchers who kept pushing the boundaries.

.. raw:: html   

   <p class="golden_heading"><span>1980s</span></p>

A major breakthrough came in the 1980s when 
`Geoffrey Hinton <https://en.wikipedia.org/wiki/Geoffrey_Hinton>`_ 
helped demonstrate how a technique called **backpropagation** (a clever mathematical way of applying corrective feedback 
to the layers *in reverse order*)
could be used to efficiently train multi-layer networks. 
Nowadays, this approach to multi-layer training is known as **deep learning**.
`Yann LeCun <https://en.wikipedia.org/wiki/Yann_LeCun>`_
then took the backpropagation algorithm and applied it to the task of 
`recognizing handwritten digits <https://en.wikipedia.org/wiki/LeNet>`_.
For this, he used a type of neural net called a **convolutional neural network (CNN)**.

Remember those concepts (*backpropagation, deep learning, CNN*) - throughout this blog post, we will come back several times 
to models based on the *CNN architecture*,
since CNN models apply to visual data, which makes them great for providing intuitively understandable examples.

After some progress had been made in the 1980s and 1990s, progress stalled again. 
Looking back, it is clear that one of the reasons was that the computers used then just did not have sufficient computational 
capabilities to train practically useful models.
AI researchers tended to focus on other types of systems, for example 
carefully hand-crafted **expert systems** which require large amounts of hand-coded expert knowledge
(`read more here <https://en.wikipedia.org/wiki/Expert_system>`_).
However, there were three notable figures - 
`Yoshua Bengio <https://en.wikipedia.org/wiki/Yoshua_Bengio>`_,
Geoffrey Hinton and Yann LeCun, who kept the flame of curiosity regarding deep learning alive 
even when other researchers moved on. 
Over the decades, they collectively supervised 50+ PhD students on various topics.

.. raw:: html   

   <p class="golden_heading"><span>2010s</span></p>

By the late 2000s, deep learning was seen by the industry mostly as a curious historical relic.
A breakthrough came from an unexpected place. A researcher named `Fei-Fei Li <https://en.wikipedia.org/wiki/Fei-Fei_Li>`_
had been working on vision models for several years and had developed
`an intuition <https://arstechnica.com/ai/2024/11/how-a-stubborn-computer-scientist-accidentally-launched-the-deep-learning-boom/>`_
that making progress would require a much larger, high-quality training dataset.
She was also inspired by an 
`estimate <http://wexler.free.fr/library/files/biederman%20%281987%29%20recognition-by-components.%20a%20theory%20of%20human%20image%20understanding.pdf>`_ 
by vision scientist Irving Biederman - that the average person 
recognizes roughly 30'000 different kinds of objects.    
With just a few colleagues, limited funding, 2 years of hard work, and a lot of ingenuity, she managed to compile a dataset of *14 million images*, 
carefully annotated into 22'000 categories, which she named **ImageNet**. She released it in 2009. To help popularize it, she also launched the 
ImageNet competition, where AI systems could compete with each other in the image classification task.

In 2010 and 2011, winners of the ImageNet competition used techniques that were only slight improvements from the state of the art 
(mostly expert systems).
In 2012, `Alex Krizhevsky <https://en.wikipedia.org/wiki/Alex_Krizhevsky>`_, 
`Ilya Sutskever <https://en.wikipedia.org/wiki/Ilya_Sutskever>`_, 
and Geoffrey Hinton won the ImageNet competition using an AI system called **AlexNet**, which was an example of
a Convolutional Neural Network (CNN) - a model architecture that had waited for its time for several decades. 
It crushed the competition with an error rate of just 15%
(winners of 2010 and 2011 had demonstrated error rates almost twice as large).
At the same time, the training time for AlexNet was *mere days* (instead of months, which would have been expected at the time). 
This event was a huge catalyst for the following boom in deep learning (and AI in general).

So, why had the time to shine now arrived for CNNs, several decades later?
First of all, the computational capability of computers had improved enormously during those decades.
Secondly, the researchers behind AlexNet managed to use 
`GPU chips <https://www.ingameloop.com/graphics-cards/learn/what-does-a-gpu-do-for-gaming/>`_
to efficiently parallelize the training process. 

After the competition, many people wanted to know answers to questions such as:

* How did AlexNet manage to beat the hand-crafted expert systems by such a large margin?
* Furthermore, how can a model like CNN even succeed at such a complicated task as image classification?

The scientists showed that after successful training, a CNN model has a property that we already observed 
for human brains: 
as information moves through subsequent layers, 
`these layers start to represent increasingly complex concepts <https://arxiv.org/pdf/2108.00107>`_. 
Consider how a CNN model processes an image of a clownfish (below):

* earlier layers detect edges and colors (e.g., the edge of an orange stripe);
* following layers start to combine them into texture-like feature groups (e.g., an orange-white striped pattern);
* later layers assemble whole object parts (e.g., the fin of a clownfish);
* final layers combine the parts and their position & orientation to detect the object class (a clownfish).

Thus, the CNNs manage to utilize one of the central pillars of intelligence: representing complex relationships via a 
combination of simpler relationships.

**A remark**. *The AlexNet model has 8 layers and approximately 60 million parameters (weights).*

.. image:: /images/part2/clownfish30.jpg
   :alt: A clownfish.

| *A clownfish. CNNs like AlexNet proved to be efficient at classifying such complex images.*
| *Source: Mark Rosenstein / iNaturalist*

..
   https://fishesofaustralia.net.au/home/species/1275

======================================
What is a weight?
======================================

Before we can discuss AI models and their training processes, we need a solid understanding of 
the concept of a **weight** in an AI model. A weight is a number (positive, negative, or 0) that shows the strength of 
the connection between two neurons.

Image classifiers like CNNs are excellent for illustrating such abstract concepts. Consider a model that analyzes an 
image and identifies the animal species in it. To make things more interesting, we consider two animals 
that are very similar in some ways, but rather different in another way: a cheetah and a leopard.

Judging by the body outline alone, the cheetah and leopard are remarkably similar. Both of them are big cats
with a similar size and a feline silhouette. 
The distinguishing factor is their coat – cheetahs have black spots on their fur and leopards have multi-colored rosettes.

.. image:: /images/part2/cheetah_leopard.png
   :alt: Cheetah vs leopard 

*Cheetah (above) vs leopard (below). Source: Wikimedia Commons (cropped).*

The last layer of the image classification model usually contains one neuron for each of the possible image classes (in this case, the animals).
We concentrate on two neurons in that last layer that correspond to the classification results “cheetah” and “leopard”.
It is then reasonable to expect that the preceding layer of the model will contain neurons that represent:

* concepts that apply to both of those animals (e.g. “large feline”);
* concepts that distinguish those animals from each other (e.g. “black spots”, or “multi-colored rosettes”).

On the image below, weights (connections between neurons) are depicted as arrows. Bolder arrows correspond to strong associations
(e.g. “has black spots” :math:`\rightarrow` “cheetah”). Thinner arrows correspond to somewhat weaker associations 
(e.g. “large feline” :math:`\rightarrow` “cheetah”).
Dashed arrows represent negative weights – that is, factors that block (**inhibit**) the next neuron from activating 
(e.g. “multi-colored rosettes” :math:`\not\rightarrow` “cheetah”).
The numerical values of weights are written above the arrows.

.. image:: /images/part2/artificial_neuron.png
   :alt: Decision neurons

*Simplified diagram of neurons for detecting cheetahs and leopards (image by author).*

Of course, this is just a toy example - in actual neural networks, each individual classification decision 
receives input signals from hundreds 
or thousands of different neurons in the preceding layer, each of them playing a small part in the decision process.

Human brains also make use of inhibitory signals in various contexts, including vision. If you are interested, click on the following box to expand it
and learn more - it turns out that this inhibition mechanism is actually the cause for some common optical illusions!

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read how inhibitory signals are used in the human brain.</summary>
         <p>Imagine a dark tree next to a bright sky; focus on the edge where the two meet.
         When light from the sky hits the receptors in the eye, neurons fire strong active signals (“it is bright here”) 
         and <em>also send</em> inhibitory 
         (negative) signals to <em>their neighbor neurons</em>, causing the dark tree to appear even darker than it actually is.
         This causes the borders between dark and bright objects to have a lot of contrast and look crisp.</p>
         <p>Curiously, this exact same process that increases the contrast between dark and light areas (called
         <a class="reference external" href="https://en.wikipedia.org/wiki/Lateral_inhibition#Visual_inhibition">visual lateral inhibition</a>)
         is exactly the cause for 
         <a class="reference external" href="https://en.wikipedia.org/wiki/Grid_illusion">several optical illusions</a>
         where the viewer may see black dots appearing on a white background.</p>
         <img alt="Grid illusion" src="../../images/part2/grid_illusion.png"><p><em>A grid illusion. Source: Wikimedia commons</em></p>
         <!-- https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/ -->
      </details>
   </embed>

==========================
The process of learning
==========================

At the moment of birth, a baby already has almost 
`all of the neurons <https://scienceinsights.org/how-developed-is-a-babys-brain-at-birth/>`_ that an adult will have. 
Learning is not about *producing new neurons*; rather, it happens as new connections (**synapses**) *form* 
between existing neurons, unused ones are *pruned* away (removed), and the strengths of those connections *change*.

An analogous mechanism drives learning in AI.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read more about the development of a child's brain and the visual system.</summary>
         <p>At birth, newborns don't see the world in full color - their vision is mostly limited to stark contrasts of light and dark,
         and they can only
         <a class="reference external" href="https://www.healthline.com/health/baby/when-can-babies-see-color">differentiate between strong, contrasting colors</a>.
         At one month of age, they still do not see the world clearly - their vision is
         <a class="reference external" href="https://www.nationwidechildrens.org/family-resources-education/health-wellness-and-safety-resources/helping-hands/infant-vision-birth-to-one-year">blurry</a>
         and near-sighted.
         Research from 2024 <a class="reference external" href="https://neurosciencenews.com/infant-vision-development-ai-27078">has also shown</a> that babies prefer to
         look at simple, high-contrast patterns and edges found in everyday environments; furthermore, this is very important
         for the development of their visual skills. At later stages of child's development, they start to recognize and understand
         more complex visual aspects of their environment.</p>
         <p>What follows is that the development of the visual system and the learning process occur in parallel -
         as the baby's visual system develops to allow for
         seeing more complex input (from mostly black-and-white to color, from blurry and short-sighted to sharp and fully developed), the brain learns
         to recognize and interpret increasingly complex patterns. Every time a child learns something, it causes some neural connections to be strengthened
         or new connections to be formed.
         At various phases of growth, different layers in the brain are undergoing their most active periods of
         development. Finally, it is important to note that sleeping also
         <a class="reference external" href="https://www.quantamagazine.org/dueling-brain-waves-anchor-or-erase-learning-during-sleep-20191024/">plays a crucial role</a>
         in the learning process in the human brain.</p>
         <p style="font-size: 0.8em;">There is also an important process in brain development for making existing networks quicker -
         <a class="reference external" href="https://www.zerotothree.org/resource/what-are-the-most-important-changes-in-the-brain-after-birth/">myelination</a>.
         Since it has no analogue for artificial neural networks, we will not focus on it; however, feel free to read about it if you are
         interested in how the brain matures.
         </p>
      </details>
   </embed>

The word “learning” has a very specific meaning in machine learning:
it means that during the training process some weights are strengthened and some are weakened. 
The mathematical operations themselves connecting the previous layer with the next one do not change; only the weights do. 
This begs the question: how does the training process select the weights to change to gradually produce a useful AI model such as AlexNet?

**Remark**. *Keep in mind that computers do not “see” the image the same way as humans do. Instead, they see an image as a grid of pixels,
and each pixel is just 3 numbers for the AI model - corresponding to the amount of red, green, and blue in that pixel.
In that sense, for AI the whole image is just a grid of numbers.*

As an initial step, a model is chosen with all of the weights being *completely random* in a given range.
In the example of AlexNet, this means that the model will produce completely random outputs (e.g., classifying an image of random noise
as an elephant). Now, at each step, the following happens:

* A small batch of images (e.g., 128 images in the case of AlexNet) is chosen randomly.
* For each of the images in that batch, prediction error is calculated (based on whether the predictions agree with the labels assigned by human digitizers).
* Using clever mathematical techniques (such as `backpropagation and chain rule <https://www.3blue1brown.com/lessons/backpropagation/>`_), 
  it is calculated for *each weight* how much changing that specific weight in a 
  positive/negative direction would have affected the prediction error of the model.
* Each weight is changed by a tiny amount in the direction (calculated in the previous step) that most improves the predictions.

This process is then repeated millions of times; if everything goes as expected, the prediction errors should start to fall and the 
model should learn to recognize features and classify images correctly and reliably. 

**Remark**. *Mathematically, the hard part is calculating how changing each specific weight would have affected the resulting prediction error,
since each layer also affects each subsequent layer as well. Remember that a single image classification model will have tens or hundreds of 
millions of neurons, so the efficiency of this calculation is crucial. This is the problem that the*
`technique of backpropagation solved <https://techhistorylab.com/history-of-backpropagation-deep-learning/>`_.
*Recall from the historical overview above that backpropagation was invented only in the 1980s after several decades of research into this area.*

Let's walk through an example of how this training process could start. The training process considers the first image of the first batch,
which happens to depict a slightly cloudy sky. 
Since the network has been initialized randomly, there will be neurons in the earlier layers which respond to blue pixels; 
and there will be neurons in the later layers that eventually lead to the image class “sky” being activated. Since we have just started training,
the image is equally likely to be classified as “sky” or “strawberry”. Since the number of neurons is large, there will be (just by chance) 
some neurons that react to the color blue and push the classification toward “sky”. So if the given batch contains 
images of the sky, those weights that support this relationship (“blue pixels” :math:`\rightarrow` “image could depict the sky”) 
are slightly strengthened. At the same time,
weights representing alternative potential relationships (e.g., “blue pixels” :math:`\rightarrow` “image could depict a strawberry”) 
are slightly weakened.
Over thousands of iterations, such relationships take form and become functional.

Of course, this is just the easiest type of heuristic one can have. In order to become truly effective at classifying images 
(e.g., images of the sky), the model has to learn (i.e., find corresponding weights):

* to detect areas of same color, edges, lines, orientation of features;
* to understand how simple edges combine into basic edges and textures;
* to how complex shapes consist of simpler shapes and geometric forms.

Take the the example of detecting a clownfish. Let's assume that model has learned that clownfish have orange and white stripes on them.
The detection capability of the model will increase if it also starts making sure that those orange and white stripes are next to each other
and alternate in color. For this to happen, some neurons in the later layers have to specialize to respond to the positional information of 
those shapes (orange/white stripes) that were detected in the preceding layers.

I recommend to take a small pause here and think about some specific object in the world and reflect on how do you, as a human, recognize 
it in an image. Try to think of the features that define it and how the model *could learn* to gradually detect it via making millions of small 
improvement steps.

------------

The crucial question is whether there is a sufficient amount of positive and negative examples in the data set: 
the model may take “shortcuts” if the input data does not punish for it. There is a 
`famous study <https://arxiv.org/abs/1807.04975>`_ that showed that image detection models often rely extensively on the environmental context for 
detecting animals (concrete example: cows are usually photographed on grassy pastures). If there is an image of a cow in a new context
(e.g., cow on a paved road, or cow on a beach), the model will fail to classify it as a cow. 
What has happened is that instead of learning the complex anatomical features of a cow (ears, muzzle, body shape), the model has learned a 
simpler rule: “somewhat cow-like animal on a green pasture :math:`\rightarrow` cow”. This is an example of what is called **shortcut learning**.

.. raw:: html

   <embed>
      <p style="font-size: 0.8em;">To be completely honest, I think that humans would also do somewhat worse at detecting cows on beaches. To see what I mean, just look at
      the images on <a class="reference external" href="https://arxiv.org/pdf/1807.04975">page 2 of the PDF linked above</a>.</p>
   </embed>

The solution is to enrich the dataset of images to have variation of contexts, backgrounds lighting, viewpoints and shapes. It is also useful
to incorporate images taken by different photographers and camera types.

In this section, we looked at the process that AI researchers follow for producing useful AI models like AlexNet.
All of those steps can be shortly summarized in the following way: 

* Collect sufficient **input data**, classified with sufficiently high accuracy.
* Define the **goal function** (*the function that tells whether the AI model is doing a good or a bad job*).
* Choose a **model architecture** (e.g., CNN).
* Initialize the model with **random weights**.
* Run the **training process**.

===================================
A visual explainer of a CNN model
===================================

An excellent way to understand something is to observe and tinker with how it works.
In the case of AI systems, this is usually not something that is easy to do.
Luckily, 
`there is a webpage <https://poloclub.github.io/cnn-explainer/>`_
that contains a *visual explainer* of a CNN model.
This webpage runs a CNN model called “Tiny VGG” *directly in your browser*, allowing to upload your own image and 
see the classification model crunching through it before your own eyes.

Notice that this CNN model is quite limited: it only accepts tiny images (64x64 pixels) and sorts them to one of the 10 pre-defined classes.
This is intentional; first, it enables the model to run smoothly in a web browser. Secondly (and more importantly), 
this allows the model to be simple enough to visually illustrate what really happens at each step. Try clicking on different 
steps to get an intuitive understanding of what happens at various steps and how the model “sees” the image.

A word of warning, though - since my overview of the topic has been rather high-level, I have not given all of the necessary
definitions for understanding CNNs. I have not explained concepts like *convolutional layers*, *kernel layers*, *ReLU activations*,
and *max pooling* that are used in the visual explainer page. If you want to learn those definitions, open the collapsible accordion 
box below. If not, just head directly to the `visual explainer page <https://poloclub.github.io/cnn-explainer/>`_ and play with the model.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to learn the technical terms about CNNs used in the visual explainer page</summary>
         <ul>
            <li><em>Convolutional layer</em> - A layer in CNN model where each neuron is connected to all neurons in the previous layer.</li>
            <li><em>Kernel layer</em> - A layer in CNN model where each neuron is only connected to a small amount of the neurons from 
            the previous layer, e.g. those that correspond to the closest 3x3 pixels (the <em>kernel</em>).</li>
            <li><em>ReLU activation</em> - An activation function that maps negative values to 0, but keeps positive values intact. Basically,
            it blocks negative (inhibitory) signals from propagating further.</li>
            <li><em>Max pooling</em> - A layer which reduces the image size by replacing each 2x2 block with the maximum value from that block.</li>
            <li><em>Hyperparameter</em> - Any parameter of the model that is not trained; the machine learning researchers have to 
            manually choose those instead based on their experience / intuition.</li>
         </ul>
      </details>
   </embed>

================================================
How to see inside the model?
================================================

Let's consider a seemingly simple question - “do we fully understand how those models work?”

On the one hand, for a given local model, the model's architecture is fully known. 
Also, at any point of training, all of the weights are known and can be inspected.
But there are things which are harder to assess:

* What kind of patterns or capabilities has the model learned?
* Which neurons are relevant or necessary for a given pattern or capability?

It is entirely possible to follow the mathematical calculations - understanding the meaning behind the weights is harder to do.

Neuroscientists face the exact same challenge when studying biological brains. If they show someone an image of a cat, they can observe which 
areas of the brain light up. But what specific groups of neurons were responsible for noticing the color of the fur? Which ones detected
the patterns? Which ones separated the cat from the background, recognized its facial expression, or inferred its mood? 
Or even deeper - which neurons caused the viewer to feel an emotion based on how the cat seemed to be feeling? 

Of course, both neuroscientists and AI researchers have developed techniques to overcome those issues. However, since a large part of 
human cognition and model capabilities are complex and emergent properties, it is not often easy to give simple and intuitive answers to such 
questions. For example, in the early days of modern brain research, scientists tended to make absolute statements like “each specific brain 
region controls just one distinct mental task”. Modern neuroscience shows that high-level intelligence emerges from interconnected, dynamic 
networks rather than isolated single components. In the context of AI research, this is especially a problem for investigating general-purpose
models like LLMs.

In the context of image recognition models, researchers have found clever ways to visually represent the inner workings of the AI models.
One of those techniques is a **saliency map**. 
It is used to high-light the pixels in the input image that were most strongly used in the 
process of assigning the category label - e.g., “chair” or “cow” 
(`read more here <https://www.geeksforgeeks.org/machine-learning/what-is-saliency-map/>`_). 
Recall the earlier example where detection of cows relied on detection of 
grass by an extensive amount. In that case, the saliency map would strongly high-light the pixels containing grass, which would inform the 
researchers of the problem. Researchers could then fix it by enlarging the dataset by cows in other context (e.g., on
a paved road).

.. image:: /images/part2/dog-saliency-map.jpg
   :alt: Example: A saliency map.

*Example of a saliency map. Source: Jay Alammar.*

..
   https://jalammar.github.io/explaining-transformers/

There is also the technique of **feature visualization** for understanding what a given neuron (or a group of neurons) in the neural net reacts to.
For this, an image with random noise is taken. After that, it is gradually modified so that it becomes an image that makes the *previously chosen
neuron(s)* to be maximally active. This process is repeated for thousands of iterations. 
By the end of the process, the image is filled with objects that the neuron(s) react to.
The end result of this process is often quite psychedelic.
In the next image, we can see a *feature visualisation* for a group of neurons that activates *for dog eyes*.

.. image:: /images/part2/feature_visualisation_dog.png
   :alt: Example of a feature visualisation.

*Example of a feature visualisation (dog eyes). Source: Distill*

This page allows to `navigate through feature visualisations <https://distill.pub/2017/feature-visualization/appendix/>`_ of a CNN model
called GoogLeNet. Notice that initial layers (3a and 3b) correspond to simple textures, whereas later layers correspond to more 
complicated concepts. For each layer, there are visualisations that maximally excite a group of neurons (“positive channel”) and visualisations that 
least excite that same group of neurons (“negative channel”). More explanations can be found `here <https://distill.pub/2017/feature-visualization/>`_.

===================================================
The importance of a goal function
===================================================

Above, we considered the steps in the process of obtaining a useful AI model. 
I would like to now focus on the step of choosing an appropriate goal function, since this step is actually rather critical 
for success.

There are some fields where defining a good goal functions is easier, since the fields themselves are more precisely defined
and there are ways for rather directly verifying the correctness of a generated result - in mathematics, a machine-readable 
proof of a theorem can be verified; in programming, it is possible to verify whether the program compiles and produces the 
expected output for various inputs.

In some other fields it is harder to define a suitable goal function. Think of the task of writing a novel - there is no direct
way to grade the quality of a machine-generated novel on the scale of 0% to 100%.

As we will see in the next blog post, this is one of the reasons that LLMs have made enormous progress in some of the fields 
that where previously considered the hardest hills to conquer (e.g., mathematics), while the progress has been lagging a bit
more behind in some other areas. However, over time, clever techniques have been developed to address this shortcoming.

=========================================
What has deep learning given us?
=========================================

After AlexNet was released in 2012, the field of deep learning experienced an avalanche of renewed interest. 
Progress was made (using various deep learning techniques) in areas such as speech recognition, image generation, 
image classification, and machine translation. 

One of the major sources for innovation in that time period was a company called DeepMind 
(founded in 2010 by `Demis Hassabis <https://en.wikipedia.org/wiki/Demis_Hassabis>`_, 
`Shane Legg <https://en.wikipedia.org/wiki/Shane_Legg>`_, 
and `Mustafa Suleyman <https://en.wikipedia.org/wiki/Mustafa_Suleyman>`_;
acquired by Google in 2014). 
I would like to mention 3 areas where they successfully applied deep learning methods.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Playing 1980s computer games
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When DeepMind was founded, Demis Hassabis looked for ways of expanding the technique of deep learning to a wider array of contexts.
For this, computer games proved to be a useful medium.

In 2014, DeepMind 
`published research <https://deepmind.google/blog/deep-reinforcement-learning/>`_
about a model (**DQN** - “deep Q-learning”) that could learn to play a wide range of classical 1980s computer games 
(such as Pong, Breakout or Space Invaders) without having any prior description about how those games work.
Instead, they used deep learning methods, letting the model learn by trying to play the games -
providing the game's screen as an input (and the game's score) to the model at every frame.
Model could only interact with the game by choosing which keys to press.

Initially, the model starts out by “pressing” random keys at times. Throughout the training, models
accidentally stumble on tactics which increase the chances of achieving a high score and the corresponding weights in the network
get **reinforced**.
In machine learning, this is called **reinforcement learning** - the network takes actions and is scored based on the result
(the score, in this case). 

This is a crucial point that distinguishes it from learning that relies on pre-defined ground truth - which is called **supervised learning**.
The model AlexNet, which we considered above, is an example of supervised learning. 
Using supervised learning in the context of Atari games would be impossible - it would mean that humans would have to manually
judge a large portion of *all possible game states*. In that sense, reinforcement learning is much more flexible - it just requires
that there exists some well defined *goal function* (like the game's score).

This also means that in the case of reinforcement learning, the model might find solutions that humans did not anticipate or 
were not aware of. Here is a video of how this happened in the game of Breakout - model discovered a
`nice strategy <https://www.youtube.com/watch?v=TmPfTpjtdgg>`_
that the team in DeepMind had not been aware of.

~~~~~~~~~~~~~~~~~~~~~~~~
AlphaGo
~~~~~~~~~~~~~~~~~~~~~~~~

After the 
`dramatic chess matches <https://en.wikipedia.org/wiki/Deep_Blue_versus_Garry_Kasparov>`_
between 
`Garry Kasparov <https://en.wikipedia.org/wiki/Garry_Kasparov>`_
and a computer algorithm named Deep Blue (developed by IBM) in 1996 and 1997, 
chess engines continued to improve. Chess players slowly came to accept that machines are and will remain superior to human players.
The game of Go, however, was a different story - until 2015, the strongest computer programs played at intermediate level at best.
The board size is huge (19x19) and the number of possible games is staggering (that number has 173 digits). The difference with chess is 
that it is much harder to assess a position and say who is in the lead; the advantages become clear only in the end-game, where 
the score is solidified. Playing the game requires relying significantly more on one's intuition and experience.

DeepMind 
`developed AlphaGo <https://research.google/blog/alphago-mastering-the-ancient-game-of-go-with-machine-learning/>`_
using a combination of machine learning and tree search techniques, combined with extensive training, 
both from human and computer play. It is fascinating that the models that they trained for playing Go were CNNs -
the same architecture that AlexNet used. However, this time the inputs to the models were states of Go games, not images.

In order to not make this post any longer than strictly necessary, I leave the choice to you - 
feel free to read the technical details of how AlphaGo works at a technical level; or skip it.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read how Deepmind trained two CNN models for playing Go</summary>
         <p>DeepMind trained two CNN models for playing Go. 
         The first neural network, the <strong>policy network</strong>, predicts the next move, and is used to narrow the search 
         to consider only the moves most likely to lead to a win. The second neural network, the <strong>value network</strong>, is 
         then used to reduce the depth of the search tree - estimating
         the winner in each position instead of searching all the way to the end of the game.</p>
         <p>They started by training the policy network, which predicts the next move.
         It was initially trained by using <em>supervised learning</em> on 30 million moves from games played by human experts,
         until it could predict the human move ~57% of the time.
         After that, the policy network was improved by reinforcement learning - AlphaGo played thousands of games with itself
         and used the game's final result (win or loss) as the <em>goal function</em> to reinforce the weights behind the strategies that
         consistently lead to winning.</p>
         <p>This policy network was then used to train a <em>value network</em> via reinforcement learning and self-play.
         The obtained value networks were able to evaluate any Go position and estimate the eventual winner with high reliability -
         a problem so hard it was previously
         <a class="reference external" href="https://www.sciencedirect.com/science/article/pii/S0004370201001217">believed to be impossible to be solved by a computer</a>.
         For a more in-depth description, I recommend to read either their
         <a class="reference external" href="https://research.google/blog/alphago-mastering-the-ancient-game-of-go-with-machine-learning/">blog post</a> or
         <a class="reference external" href="http://www.nature.com/nature/journal/v529/n7587/full/nature16961.html">paper in Nature</a>.</p>
      </details>
   </embed>

In 2016, AlphaGo played a match against 
`Lee Sedol <https://en.wikipedia.org/wiki/Lee_Sedol>`_, 
one of the best Go players in the world - and won 4:1.
There is an `excellent movie <https://www.youtube.com/watch?v=WXuK6gekU1Y>`_ on YouTube which captures the dramatic events and the effect it
had on how Go is played. 
It also gives some nice visual explanations of the technology behind the breakthrough.

~~~~~~~~~~~~~~~~~~~~~~~~
AlphaFold
~~~~~~~~~~~~~~~~~~~~~~~~

In recent years, leaders of frontier labs have talked a lot about how LLMs could cure cancer in the future. In a longer time span, this may be true;
but in a shorter time span one has to keep in mind that while AI can help with suggesting new drug candidates or biological experiments,
some of the steps can not be so easily side-stepped, like clinical testing and obtaining regulatory approval for drugs.

At the same time, we already have one incredible biological breakthrough in an area that had seen only limited progress in 50 years - protein folding.
The problem's statement sounds innocent enough: given a protein, what 3D shape does this protein molecule take? 
Proteins consist of 22 different amino acids; those can be thought of as “universal LEGO bricks” that the body uses for various purposes.
The role of the proteins is largely determined by the 3D shape that they take (which in turn is determined by which amino acids repel and attract each
other). Here are some examples for illustrative purposes:

* keratin - *long rod-like shape* - important component of hair;
* collagen - *long triple helix shape* - gives strength to bones, tendons, and ligaments;
* hemoglobin (a protein that additionally contains iron) - *a basket-like shape* - transports oxygen into cells;
* antibodies (immunoglobulin) - *Y-shape* - each antibody attaches to a different target (e.g., a microbe or an infected cell) so that the 
  immune system knows to attack that target.

.. image:: /images/part2/4proteins70.png
   :alt: 4 proteins (keratin, collagen, hemoglobin, antibodies)

*3D structures of*
`keratin <https://www.rcsb.org/structure/6EC0>`_, 
`collagen <https://www.rcsb.org/structure/1CAG>`_, 
`hemoglobin <https://www.rcsb.org/structure/2HHB>`_, and 
`immunoglobulin <https://www.rcsb.org/structure/1IGT>`_.
*Source: RCSB Protein Data Bank* 

Protein folding was an active research area since 1971, and by end of 2022, 
`scientists had identified 3D shapes for 200 thousand proteins <https://www.rcsb.org/news/639b9e337f8444f313d20414>`_.
Previously, it could take a student their whole PhD study to determine the 3D structure of a *single protein*.
In 2018, DeepMind introduced a specialized deep learning model called 
`AlphaFold <https://deepmind.google/blog/alphafold-using-ai-for-scientific-discovery/>`_
for the protein folding problem, and it turned out to be hugely successful.
AlphaFold predicts the 3D structure that the protein takes, which can then be verified both mathematically and by physical 
observation. Throughout the years, the precision of their AI models continued to improve.
By 2022, they had achieved a milestone - they had mapped the 3D shape of *200 million* proteins, virtually 
`every protein known to exist in nature <https://deepmind.google/blog/alphafold-reveals-the-structure-of-the-protein-universe/>`_.
They had taken what took people years and tens of thousands of dollars via experimental methods, 
and turned it into something that the AI could do in seconds for a negligible cost.

For this achievement, Demis Hassabis and 
`John Jumper <https://en.wikipedia.org/wiki/John_M._Jumper>`_
were awarded the 
`Nobel Prize in Chemistry for AlphaFold <https://www.nobelprize.org/prizes/chemistry/2024/summary/>`_ in October 2024.

There is an excellent `video overview from Veritaserium channel <https://www.youtube.com/watch?v=P_fHJIYENdI>`_ about AlphaFold.
Alternatively, one can read technical details from 
`DeepMind blog <https://deepmind.google/blog/alphafold-using-ai-for-scientific-discovery/>`_.

==============
Conclusion
==============

The main takeaways I want to leave to you, the reader:

* Although AI systems have been originally been built on ideas borrowed from human brains, they are still very much different. And it is not 
  necessary for AI systems to blindly imitate human brains.
* Learning is possible where there is a clear goal function towards which to gradually optimize. Sometimes just defining a good goal 
  function is already a significant step towards success.
* There exists a large variety of different AI systems, both narrow and general-purpose. Being able to distinguish between them is a starting point for 
  any public discussion about both the benefits and risks.
* AI models are not magic - by learning the basic principles that they operate on, it is possible to have much more meaningful and deeper 
  conversations. This is also why it is crucial for politicians and lawmakers to educate themselves on the topic.

Although we covered a lot of ground in this post, this overview really just scratches the surface of all the research done over the decades
into various AI systems. In the next blog post, we will focus on generative AI (including LLMs), the transformer architecture,
and how it is different from the preceding AI architectures.

------------

.. raw:: html

   <p style="margin-bottom: 0.5rem;">To recognize their contribution to this field, Yoshua Bengio, Geoffrey Hinton and Yann LeCun were awarded the
   <a class="reference external" href="https://awards.acm.org/about/2018-turing">2018 Turing Award</a>
   for:</p>
   <blockquote cite="https://awards.acm.org/about/2018-turing" style="margin-top: 0px;">
      <p>&nbsp; conceptual and engineering breakthroughs that have made deep neural networks a critical component of computing.</p>      
   </blockquote>

------------

.. raw:: html

   <embed>
      <div class="ai-disclaimer">
      <b>Disclaimer of AI usage</b>: 
      <ul><li>AI (Google Gemini) was used to find additional sources for this post; 
      all sources were manually verified before citing.</li> 
      <li>AI was used to simplify some of the more complex & technical concepts (e.g. regarding human vision).</li>
      <li>AI was used in the final proof-reading process for pointing out improvement possibilities, but not for re-writing text.</li></ul>
      Total contribution of AI in terms of effort during the process: 5-10%
      </div>
   </embed>

