.. title: Where is AI heading - part 2/4: History of AI
.. slug: where-is-ai-heading-part-2-of-4-narrow-ai
.. date: 2026-09-10 20:17:59 UTC+03:00
.. tags: AI, AI-overview, narrow-AI
.. category: 
.. link: 
.. description: 
.. type: text
.. has_math: true
.. status: draft

Initially I planned to use this second post to dive straight into Large Language Models (LLMs). 
But when I thought about explaining the basic principles of LLMs, I realized that it makes much more sense to
start by explaining the basic concepts of preceding AI systems; and only then do a deep dive into LLMs and transformer
architecture in general.

In particular, we will focus in this post on image classification models. They are relatively easy to intuitively grasp 
and they are also very illustrative for concepts that we will need later on. On the way, we will touch a bit on the history
of the AI as a field. 

.. contents::
   :depth: 1
   :local:

The following timeline high-lights some of the key events in the history of AI: TODO

..
   https://timeline.knightlab.com/

..
   ++ AlphaStar master StarCraft II.

**Important note**: *if you scroll through this post, you will see some complex-looking images. Don't be put off by those!
Those are mostly provided for illustrative purposes - I will do my best to explain everything in simple and understandable terms.*

=========================================
Inspiration for AI - human brains
=========================================

For a long time, humankind has been fascinated by questions as:

* What is intelligence?
* How do our brains work?
* Is it possible to artifically imitate the inner workings of the brain?
* What are the fundamental building blocks of the brain? 
* How do these building blocks function together to give rise to such complex phenomena as vision, smell, or logic?

Cells called **neurons** play an important role in answering all of the questions above. 
In the brain, millions of neurons form complicated networks that encode memories, 
shape personalities, drive decisions, and process the sensations of touch, taste, sight, smell, and sound 
(for deeper overview of this topic, read more at 
`Khan Academy <https://www.khanacademy.org/science/biology/human-biology/neuron-nervous-system/a/overview-of-neuron-structure-and-function>`_).

Some interesting facts about neurons in our brains and bodies:

* An adult human brain contains approximately `80 billion neurons <https://academic.oup.com/brain/article/148/3/689/7909879?login=false>`_.
* A single neuron may be connected to 1000-10000 other neurons.
* The `longest neuron in human body <https://en.wikipedia.org/wiki/Sciatic_nerve>`_ can be over a meter long (from bottom of spine to toes). However, most neurons in brain are less than a millimeter in length.

Human vision is made possible by a large number of neurons working in unison.
Although neural networks consisting of hundreds of millions neurons are hard to research,
each individual neuron by itself is (comparatively speaking) much simpler.

Neurons carry out the following functions:

* they receive inputs (chemical and electrical) from multiple sources;
* they combine those inputs into a single signal;
* if the signal is strong enough, they fire an output that reaches the next neuron (or neurons).

Scientists working in this field realized that an individual neuron is not that difficult to describe mathematically.
Building on that idea,
`Frank Rosenblatt <https://en.wikipedia.org/wiki/Frank_Rosenblatt>`_
came up in 1957 with the idea of a `perceptron <https://www.simplilearn.com/tutorials/deep-learning-tutorial/perceptron>`_,
a simplified mathematical model of a neuron. Just for illustrative purposes, compare a neuron in a brain and an 
artificial "neuron":

.. image:: /images/part2/neuron2.png
   :alt: Biological neuron vs artificial neuron

*Biological neuron vs artificial neuron. Source: Towards Data Science (modified).*

Artificial neurons (specifically in the original perceptron model) follow the same core principles as biological neurons, 
but in simplified mathematical form. Artificial neurons:

* receive input values (positive or negative numbers);
* combine those values linearly using specific weights (this will be explained more later);
* produce an output if the combined value passes a certain threshold (otherwise, the output is 0).

The same basic structure for neurons powers the vast majority of neural networks used today (including LLMs). 
The main difference is how the third step works: modern networks swap out the strict "all-or-nothing" threshold for 
a bit more complicated threshold functions.

A crucial feature of the perceptron was its ability to use a learning algorithm to adjust its weights based 
on input data and target output, thus learning from its mistakes and improving its performance over time. 

However, perceptrons also had their limitations. In the next sections, we will see what those were
and how the science of neural networks has evolved over time.

============================
Multi-layer networks 
============================
 
A fundamental limitation of the perceptron model was that it was a single-layer network - meaning there were no intermediate 
layers of neurons between the inputs and the output. Contrast that with the 
`human vision <https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/>`_, 
where there are ~10 layers of neurons, from the cells receiving the light impulses to the neurons 
in the brain that correspond to a concept, like seeing a cat.

The next image is provided mostly for illustration purposes - there is *no need to memorize* it!
It just demonstrates some of the neural layers present in the eye. The image should be read from bottom to top - 
in the bottom, there are rods and cones, which respond to incoming light. *Cones* handle vision in bright daylight, while *rods*
take over in low light and at night. 
After that, the signal passes through various layers of neurons (illustrated by the diagram), until it reaches the optic nerve, which takes 
the visual information to your brain for further processing.

.. image:: /images/part2/eye-visual-system.png
   :alt: Neural layers in the eye

*The five neural layers in the eye. Source:*
`Open Neuroscience Initiative <https://pressbooks.atlanticoer-relatlantique.ca/openneuroscience/chapter/chapter-9-sensation-and-perception-the-visual-system/>`_
*(with my modifications)*

..
   License for previous image: Creative Commons Attribution-NonCommercial 4.0 International License.

There are 120 million rods and 6 million cones in the human eye. 
The raw image captured by those rods and cones is heavily compressed before it ever leaves the eye (via the optic nerve). 
For example, the retinal ganglion cells (drawn in blue color in the above image) act like a biological image compression algorithm.

The optic nerve consists of ~1.2 million optic nerve fibers. You might think of it as an 1.2 megapixel camera cable.
However, human vision feels much better than a picture taken by a 1.2 megapixel camera, and there are some 
`absolutely fascinating reasons for this <https://clippingexpertasia.com/blog/human-eye-resolution-explained-megapixels-fps-vision>`_.

After reaching the optic nerve, information is processed 
via a series of neural layers.
Each layer builds on the previous layer and represents increasingly complex features:

1. layer: organizes **visual information** (*technically: "LGN layer"*);
2. layer: detects **low-level features**: orientation, edges, and lines (*technically: "V1 layer"*);
3. layer: combines simple edges into **basic shapes** and textures (*technically: "V2 layer"*);
4. layer: processes **complex shapes** and geometric forms (*technically: "V4 layer"*);
5. layer: detects **whole objects**, faces, and abstract concepts, e.g., reckognizing a dog, a car, or a number (*technically, 1 or 2 layers: "IT cortex"*).

For more detailed overview, see `here <https://people.csail.mit.edu/pulkitag/data/cnn_mimics_brain.pdf>`_
and `here <https://en.wikipedia.org/wiki/Visual_system#System_overview>`_.

.. raw:: html

    <embed>
        <p style="font-size: 0.8em;">Since I am not a neuroscientist, the above description may contain oversimplifications or errors. 
        However, the general principle should still be correct and serves to illustrate the subsequent layers represent increasingly
        complex patterns. The full description of how the visual cortex works
        also involves looping effects, complex time-dependent processes, and some layers fulfilling multiple functions; my description
        is a simplification of a complex process. I also glossed over layers of V3, V5, and V6, since they primarily handle motion and spatial
        processing, whereas our focus here is on what happens when a person views static images.</p>
    </embed>

The same principles applies for machine learning: the number of layers must be sufficient so that complex features or concepts can be 
represented. However, increasing the number of layers also increases the training time.

==========================
Progress in AI research    
==========================

Early research into neural networks (in 1940s to 1960s) encountered significant challenges.
As mentioned above, those neural networks were primarily confined to single-layer architectures.
Also, the research initially lacked a strong theoretical foundation.
In 1969, a book called `Perceptrons <https://en.wikipedia.org/wiki/Perceptrons_(book)>`_ demonstrated that 
*single-layer networks are fundamentally limited* 
(`mathematical explanation <https://apxml.com/courses/introduction-to-deep-learning/chapter-1-neural-network-foundations/perceptron-limitations>`_), 
and noted that there is no known *efficient* way to train multi-layer networks.

After that, there were several periods when the interest in AI research was considerably reduced. Such time periods are now
called "AI winters" (`see here <https://news.sparkfun.com/7896>`_ for more exact historical background).
However, there were dedicated researchers who regardless kept pushing the boundaries.

A major breakthrough came in the 1980s when 
`Geoffrey Hinton <https://en.wikipedia.org/wiki/Geoffrey_Hinton>`_ 
helped demonstrate how a technique called **backpropagation**
could be used to efficiently train multi-layer networks. 
`Yann LeCun <https://en.wikipedia.org/wiki/Yann_LeCun>`_
then took this algorithm and applied it to the problem of 
`recognizing handwritten digits <https://en.wikipedia.org/wiki/LeNet>`_.
For this, he used a type of neural net called **convolutional neural network (CNN)**.
This practical application of multi-layer training established the paradigm that is nowadays known as **deep learning**.
Remember those concepts - throughout this blog post, we will come back several times to models based on the *CNN architecture*,
since CNN models work on visual data, which makes them great for providing intuitively understandable examples.

The next diagram shows a toy example of a 4-layer neural network (the input layer is not counted).
On the left (orange) is an input layer; it is followed by multiple layers of neurons (green columns);
the network concludes with an output layer, containing a single neuron in this example (red).
Of course, this is just a toy example and neural networks nowadays used for practical applications 
contain millions of neurons or more.

.. image:: /images/part2/deep_neural_network.png
   :alt: A simplified illustration of a deep neural network.

*A simplified illustration of a deep neural network. Source: KDNuggets*

After some progress had been made in 1980s and 1990s, progress stalled again. 
Looking back, it is clear that one of the reasons was that the computers used then just did not have sufficient computational 
capabilities to train practically useful models.
AI researchers tended to focus on other types of systems, for example 
carefully hand-crafted **expert systems** which require large amounts of hand-coded expert knowledge
(`read more here <https://en.wikipedia.org/wiki/Expert_system>`_).
However, there were three notable figures - 
`Yoshua Bengio <https://en.wikipedia.org/wiki/Yoshua_Bengio>`_,
Geoffrey Hinton and Yann LeCun, who kept the flame of curiousity regarding deep learning alive 
even when other researchers moved on. 
Over the decades, they collectively supervised 50+ PhD students on various topics.

Lets fast forward to 2008. Deep learning was seen by the industry mostly as a curious historical relic.
A breakthrough came from an unexpected place. A researcher named `Fei-Fei Li <https://en.wikipedia.org/wiki/Fei-Fei_Li>`_
had been working on vision models for several years and had developed
`an intuition <https://arstechnica.com/ai/2024/11/how-a-stubborn-computer-scientist-accidentally-launched-the-deep-learning-boom/>`_
that for making progress,
more comprehensive high-quality training dataset would be necessary.
She was also inspired by an 
`estimate <http://wexler.free.fr/library/files/biederman%20%281987%29%20recognition-by-components.%20a%20theory%20of%20human%20image%20understanding.pdf>`_ 
by vision scientist Irving Biederman that the average person 
recognizes roughly 30,000 different kinds of objects.    
With just a few colleagues, limited funding, 2 years of hard work, and a lot of ingenuity, she managed to compile a dataset of *14 million images*, 
carefully annotated into 22 000 categories, which she named **ImageNet**. She released it in 2009. To help to popularize it, she also launched an
image classification competition for AI systems.

In 2010 and 2011, winners of the ImageNet competition used techniques that were only slight improvements from the state of the art 
(mostly expert systems).
In 2012, `Alex Krizhevsky <https://en.wikipedia.org/wiki/Alex_Krizhevsky>`_, 
`Ilya Sutskever <https://en.wikipedia.org/wiki/Ilya_Sutskever>`_, 
and Geoffrey Hinton won the ImageNet competition using an AI system **AlexNet**, which was an example of
a Convolutional Neural Network (CNN) - a model architecture that had waited for its time for several decades. 
It crushed the competition with an error rate of just 15%
(winners of 2010 and 2011 had error rates of 28% and 26%, correspondingly), while the training time dropped from months to days. 
This event was a huge catalyst for the following boom in deep learning (and AI in general).

So, why had the time to shine now arrived for CNNs, several decades later?
First of all, the computational capability of computers had improved enormously in that time.
Secondly, the researchers behind AlexNet managed to use 
`GPU chips <https://www.ingameloop.com/graphics-cards/learn/what-does-a-gpu-do-for-gaming/>`_
to efficiently parallelize the training process. 

After the computation, many people wanted to know answers to questions such as:

* How did AlexNet manage to beat the hand-crafted expert systems by such a large margin?
* Furthermore, how can a model like CNN even succeed at such a complicated task like image classification?

After successful training, a CNN model has a property that we already observed 
for human brains: 
as information moves through subsequent layers, 
`these layers start to represent increasingly complex concepts <https://arxiv.org/pdf/2108.00107>`_. 
Consider how a CNN model processes an image of a clownfish:

* earlier layers detect edges and colors (e.g., the edge of an orange stripe);
* following layers start to combine them into texture-like feature groups (e.g., an orange-white striped pattern);
* later layers assemble whole object parts (e.g., fin of a clownfish);
* final layers combine the parts and their position & orientation to detect the object class (a clownfish).

Thus, the CNNs manage to utilize one of the central pillars of intelligence: representing complex relationships via a 
combination of 
simpler relationships. In the next section we will have a look at how the learning process actually works.

**Note**. *The AlexNet model has 8 layers and approximately 60 million parameters.*

.. image:: /images/part2/clownfish.jpg
   :alt: A clownfish.

| *A clownfish. CNNs like AlexNet proved to be efficient at classifying such complex images.*
| *Source: Aquarium of the Pacific*

======================================
But how does this learning happen?
======================================

There are some similarities between learning in humans (especially babies) and how AI models are trained, and there are many 
crucial differences. Before we dive into those similarities and differences, it is useful to think a bit about how babies learn.

At birth, newborns don't see the world in full color - their vision is mostly limited to stark contrasts of light and dark,
and they can only 
`differentiate between strong, contrasting colors <https://www.healthline.com/health/baby/when-can-babies-see-color>`_.
At one month of age, they still do not see the world clearly - their vision is 
`blurry <https://www.nationwidechildrens.org/family-resources-education/health-wellness-and-safety-resources/helping-hands/infant-vision-birth-to-one-year>`_
and near-sighted.
Research from 2024 `has also shown <https://neurosciencenews.com/infant-vision-development-ai-27078>`_ that babies prefer to 
look at simple, high-contrast patterns and edges found in everyday environments; furthermore, this is very important
for the development of their visual skills. At later stages of child's development, they start to recognize and understand
more complex visual aspects of their environment.

What follows is that the development of the visual system and the learning process occur in parallel - 
as the baby's visual system develops to allow for 
seeing more complex input (from mostly black-and-white to color, from blurry and short-sighted to sharp and fully developed), the brain learns
to recognize and interpret increasingly complex patterns. Every time a child learns something, it causes some neural connections to be strengthened 
or new connections to be formed.
At various phases of growth, different layers in the brain are undergoing their most active periods of 
development. Finally, it is important to note that sleeping also 
`plays a crucial role <https://www.quantamagazine.org/dueling-brain-waves-anchor-or-erase-learning-during-sleep-20191024/>`_
in the learning process in the human brain.

Curiously, at the moment of birth a baby already has almost 
`all of the neurons <https://scienceinsights.org/how-developed-is-a-babys-brain-at-birth/>`_ that the adult will have. 
The learning process is not about *producing new neurons*, it is about the process of new connections (**synapses**) *forming* 
between the existing neurons, unused connections being *pruned* (removed), and the strengths of connections *changing*.

.. raw:: html

   <embed>
      <p style="font-size: 0.8em;">There is also an important process in brain development for making existing networks quicker - 
      <a class="reference external" href="https://www.zerotothree.org/resource/what-are-the-most-important-changes-in-the-brain-after-birth/">myelination</a>. 
      Since it has no analogue for artificial neural networks, we will not focus on it; however, feel free to read about it if you are 
      interested in how the brain matures.
      </p>
   </embed>

Lets now think about AI models, their training, and the similarities and differences compared to human learning.
First, the analogue of a biological synapse (connection between neurons) is a **weight** in an AI model. 
Below, we repeat the image from above about the structure of an artificial neuron; this time we have added some values to it 
for explanatory purposes (TODO).
Bigger arrows correspond to larger weights (TODO). 

.. image:: /images/part2/neuron_only.png
   :alt: Artificial neuron

*Artificial neuron. Source:* 
`Towards Data Science <https://towardsdatascience.com/the-concept-of-artificial-neurons-perceptrons-in-neural-networks-fab22249cbfc/>`_ 
*(with my modifications FIXME).*

In neural nets, weights can also have a negative value (depicted with a dashed arrow - TODO). This has the effect of that neuron acting as a brake
for the neuron in the next layer (the technical term is "**inhibition**"). 
Consider a network trying to distinguish a cheetah from a leopard - both are big cats with four legs, a tail, 
and spotted fur.
The distinguish feature is the shape of the spots - cheetahs have solid, single black spots; leopards have complex, multi-colored rosettes.
Lets assume that the blue neuron in the image stands for a network detecting cheetahs. x1 and x2 (TODO) would represent factors that are common
for both cheetahs and leopards; xn (TODO) would represent the detection of rosettes. Since cheetahs do not have such rosettes, the weight wn (TODO)
would be strongly negative, *inhibiting* the detection of the class "cheetah".

TODO: add image of cheetah vs leopard.

Human brains also make use of inhibitory signals in various contexts, including vision; if you are interested, click on the following box to expand it
and learn more.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read how inhibitory signals are used in the human brain
         and how this is related to some optical illusions</summary>
         <p>Imagine a dark tree next to a bright sky; focus on the edge where the two meet.
         When light from the sky hits the receptors in the eye, neurons fire strong active signals ("it is bright here") 
         and <em>also send</em> inhibitory 
         (negative) signals to <em>their neighbor neurons</em>, causing the dark tree appear even darker than it actually is.
         This causes the borders between dark and bright objects to have a lot of contrast and look crisp.</p>
         <p>Curiously, this exact same process that increases the contrast between dark and light areas (called
         <a class="reference external" href="https://en.wikipedia.org/wiki/Lateral_inhibition#Visual_inhibition">visual lateral inhibition</a>
         is exactly the cause for 
         <a class="reference external" href="https://en.wikipedia.org/wiki/Grid_illusion">several optical illusions</a>
         where the viewer sees dots appearing on white background.</p>
      </details>
   </embed>

The word "learning" has a very specific meaning in machine learning:
it means that during the training process, some weights are strengthened and some are weakened. 
The mathematical operations themselves connecting the previous layer with the next one do not change; only the weights do. 
This begs the question: how does the training process select the weights to change to gradually produce a useful AI model such as the AlexNet?

**Remark**. *Keep in mind that computers does not "see" the image as humans do. Instead, they see an image as a grid of pixels,
and each pixel is just 3 numbers for the AI model - corresponding to the amount of red, green, and blue in that pixel.
In that sense, for AI an image is just a grid of numbers.*

As an initial step, a model is chosen with all of the weights being completely random in a given range.
In the example of AlexNet, this means that the model will produce completely random outputs (e.g., classifying a image of random noise
as an elephant). Now, at each step, the following happens:

* A small batch of images (e.g., 128 images in case of AlexNet) is chosen randomly.
* For each of the images in that batch, the error rate is calculated (how good or bad the prediction was).
* Using clever mathematical techniques (such as `backpropagation and chain rule <https://www.3blue1brown.com/lessons/backpropagation/>`_), 
  it is calculated for *each weight* how much changing that specific weight in a 
  positive/negative direction would have affected the error rates of the model.
* Each weight is changed by a tiny amount in the direction (calculated in the previous step) that most improves the error rates.

This process is then repeated millions of times; if everything goes as expected, the error rates should start to fall and the 
model should learn to recognize features and classify images correctly and reliably. 

**Remark**. *Mathematically, the hard part is calculating how changing of each specific weight would have affected the resulting error rate,
since each layer also affects each subsequent layer as well. Remember that a single image classification model will have tens or hundreds of 
millions of parameters, so the efficiency of this calculation is crucial. This is the problem that the*
`technique of backpropagation solved <https://techhistorylab.com/history-of-backpropagation-deep-learning/>`_.
*Recall from the historical overview above that backpropagation was invented only in 1980s after several decades of research into this area.*

Lets walk through an example of how this training process could start. We are at the first step, where the model has been initialized randomly. 
The image that we are given depicts a slightly cloudy sky and the image has been classified (by a human, before training) as "sky".
In the network that has been initialized randomly, there will be neurons in the earlier layers which respond to the blue color; 
and there will be neurons in the layer laters that eventually lead to the image class "sky" being activated. Since we have just started training,
the image is as likely to be classified as the "sky" as a "strawberry". Since the number of neurons is large, there will be (just by chance) 
some neurons that react to the color blue and eventually affect the result being classified as the sky. So if the given batch contains 
images of sky, those weights that support this relationship ("lot of blue => image could depict the sky") are strengthened. At the same time,
alternative relationships (e.g., "lot of blue => image could depict a strawberry") are weakened.

Of course, this is just the easiest type of heuristic one can have. In order to become truly effective at classifying images 
(e.g., images of the sky), the model has to learn (i.e., find corresponding weights):

* to detect areas of same color, edges, lines, orientation of features;
* to understand how simple edges combine into basic edges and textures;
* to how complex shapes consist of simpler shapes and geometric forms.

Take the the example of detecting a clownfish. Lets assume that model has learned that clownfishes have orange and white stripes on them.
The detection capability of the model will increase if it also starts making sure that those orange and white stripes are next to each other
and alternate in color. For this to happen, some neurons in the later layers have to specialize to respond to the positional information of 
those shapes (orange/white stripes) that were detected in the preceding layers.

I recommend to take a small pause and think about some specific object in the world and reflect on how do you recognize 
it in an image. Try to think of the features that define it and how the model could learn to detect it.

The crucial question is whether there is a sufficient amount of positive and negative examples in the data set: 
the model may take "shortcuts" if the input data does not punish for it. There is a 
`famous study <https://arxiv.org/abs/1807.04975>`_ that showed that image detection models often rely extensively on the environmental context for 
detecting animals (specific example: cows are usually photographed on grassy pastures). If there is an image of a cow in a new context
(e.g., cow on a paved road, or cow on a beach), the model will fail to classify it as a cow. 
What has happened is that instead of learning the complex anatomical features of a cow (ears, muzzle, body shape), the model has learned a 
simpler rule: "somewhat cow-like animal on a green pasture => cow". This is an example of what is called **shortcut learning**.

.. raw:: html

   <embed>
      <p style="font-size: 0.8em;">To be completely honest, I think that humans would also do somewhat worse at detecting cows on beaches. To see what I mean, just look at
      the images on <a class="reference external" href="https://arxiv.org/pdf/1807.04975">page 2 of the PDF linked above</a>.</p>
   </embed>

The solution is to enrich the dataset of images to have variation of contexts, backgrounds lighting, viewpoints and shapes. It is also useful
to incorporate images taken by different photographers and camera types.

Finally, for something completely different - I would like to present a *visual explainer* of a CNN model.
It is a webpage that runs a CNN model called "Tiny VGG" *directly in your browser*, allowing to upload your own image and 
see the classification model crunching through it before your own eyes.
However, this model only accepts tiny images (64x64 pixels) and sorts the images to one of 10 pre-defined classes.
This is intentional; first, it enables the model to run smoothly in a web browser. Secondly (and more importantly), 
this allows the model to be simple enough to visually illustrate what really happens at each step. Try clicking on different 
steps to get an intuitive understanding of what happens at various steps and how the model "sees" the image.

A word of warning, though - since my overview of the topic has been rather high-level, I have not given all of the necessary
definitions for understanding CNNs. I have not explained concepts like *convolutional layers*, *kernel layers*, *ReLu activation*,
and *max pooling* that are used in the visual explainer page. If you want to learn those definitions, open the collapsible accordion 
box below. If not, just head directly to the `visual explainer page <https://poloclub.github.io/cnn-explainer/>`_.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to learn the technical terms about CNNs used in the visual explainer page</summary>
         <ul>
            <li><em>Convolutional layer</em> - A layer in CNN model where each neuron is connected to all neurons in the previous layer.</li>
            <li><em>Kernel layer</em> - A layer in CNN model where each neuron is only connected to a small amount of the neurons from 
            the previous layer, e.g. those that correspond to the closest 3x3 pixels (the <em>kernel</em>).</li>
            <li><em>ReLu activation</em> - An activation function that maps negative values to 0, but keeps positive values intact. Basically,
            it blocks negative (inhibitory) signals from propagating further.</li>
            <li><em>Max pooling</em> - A layer that applies the <em>softmax</em> operation, normalizing the sum of all signals in the preceding 
            layer to be 1.</li>
            <li><em>Hyperparameter</em> - Any parameter of the model that is not trained; the machine learning researchers have to 
            manually choose those instead based on their experience / intuition.</li>
         </ul>
      </details>
   </embed>

In this section, we looked at the process that AI researchers follow for producing useful AI models like AlexNet.
All of those steps can be shortly summarized in the following way: 

* Collect sufficient **input data**, classified with sufficiently high accuracy.
* Define the **goal function**.
* Choose a **model architecture** (e.g., CNN).
* Initialize the model with **random weights**.
* Run the **training process**.

================================================
How to see inside the model?
================================================

Lets consider a seemingly simple question - "do we fully understand how those models work?"

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
questions. For example, in the early days of modern brain research, scientists tended to make absolute statements like "each specific brain 
region controls just one distinct mental task". Modern neuroscience shows that high-level intelligence emerges from interconnected, dynamic 
networks rather than isolated single components. In the context of AI research, this is especially a problem for investigating general-purpose
models like LLMs.

In the context of image recognition models, researchers have found clever ways to visually represent the inner workings of the AI models.
One of those techniques is a **saliency map**. 
It is used to high-light the pixels in the input image that were most strongly used in the 
process of assigning the category label - e.g., "chair" or "cow" 
(`read more here <https://www.geeksforgeeks.org/machine-learning/what-is-saliency-map/>`_). 
Recall the earlier example where detection of cows relied on detection of 
grass by an extensive amount. In that case, the saliency map would strongly high-light the pixels containing grass, which would inform the 
researchers of the problem. Researchers could then fix it by enlarging the dataset by cows in other context (e.g., on
a paved road).

.. image:: /images/part2/dog-saliency-map.jpg
   :alt: Example: A saliency map.

*Example of a saliency map. Source:* `Jay Alammar <https://jalammar.github.io/explaining-transformers/>`_

There is also the technique of **feature visualization** for understanding what a given neuron (or a group of neurons) in the neural net reacts to.
For this, an image with random noise is taken. After that, it is gradually modified so that it becomes an image that makes the *previously chosen
neuron(s)* to be maximally active. This process is repeated for thousands of iterations. 
By the end of the process, the image is filled with objects that the neuron(s) react to.
The end result of this process is often quite psychedelic.
In the next image, we can see a feature visualisation for a group of neurons that activates *for dog eyes*.

.. image:: /images/part2/feature_visualisation_dog.png
   :alt: Example of a feature visualisation.

*Example of a feature visualisation (dog eyes). Source: Distill*

This page allows to `navigate through feature visualisations <https://distill.pub/2017/feature-visualization/appendix/>`_ of a CNN model
called GoogLeNet. Notice that initial layers (3a and 3b) correspond to simple textures, whereas later layers correspond to more 
complicated concepts. For each layer, there are visualisations that maximally excite a group of neurons ("positive channel") and visualisations that 
least excite that same group of neurons ("negative channel"). More explanations can be found `here <https://distill.pub/2017/feature-visualization/>`_.

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
more behind in some other areas.

==================================================
Narrow AI vs general-purpose AI
==================================================

In a very broad sense, AI systems can be divided into two:

* **narrow** AI systems, which can perform one (or a few) specific functions (e.g., AlexNet);
* **general-purpose** AI systems, which can perform a variety of tasks (e.g., any LLM).

**NB!** *The last definition should not be confused with "AGI" ("Artificial General Intelligence"), which is defined as "an AI system that 
that matches or surpasses human capabilities across virtually all cognitive tasks"*.

Note that while AGI is a vague term and everyone interprets it differently, the distinction between *narrow* and *general-purpose* AI systems 
is much more clear-cut - the distinction focuses on the *applicability* of the model, not its capabilities. Even the earliest version of Chat-GPT
were *general-purpose* (even though they were not very capable).

For many people, the word "AI" has become synonymous to LLMs. I think that this is rather problematic and makes it extremely hard to have 
meaningful public discourse about risks and benefits of AI systems and their regulation. A lot of valid and difficult questions 
about LLMs (in particular about their safety and alignment) are either non-issues or much milder for more narrow AI systems.
Of course, there are also issues that are relevant in both cases (e.g., bias).

Consider also energy efficiency. For example, lets compare the energy usage (in 
`joules <https://whateverconverter.com/glossary/joule/>`_)
of taking a single image and detecting the content of the image (i.e., an image classification task):

* For a typical **narrow** AI system, the energy usage falls in the range of 0.05-2 joules 
  (`more details <https://arxiv.org/pdf/2412.09731>`_) - the equivalent of a household LED lightbulb shining for less than 0.1 seconds (essentially, one blink of a LED).
* For a LLM, the energy usage for the same classification task could take ~200-300 joules (`more details <https://arxiv.org/abs/2311.16863>`_). 
  If the answer is given by the LLM in the conversational format, the answer can easily be more than 10 times longer, bringing the energy usage to over 3000 joules - 
  the LED lightbulb shining for 4 minutes straight.

For me, the difference is mind-blowing: using an LLM for the same task uses **~3000** times more energy!

.. raw:: html

   <embed>
      <details>
         <summary>Click here for an explanation - where does the 3000x energy difference come from?</summary>
         <ul class="simple">
         <li><p>As already mentioned, large part of it is that conversational answers take a lot more energy to produce - and LLMs <em>love</em> to be wordy.</p></li>
         <li><p>Even if the classification result is provided without unnecessary clutter ("A golden retriever sitting on a grass field at sunset"), LLMs still build up
         the answer word by word (<em>token by token, to be more precise - more about that in the next blog post</em>), using up a considerable amount of energy for 
         producing each word.</p></li>
         <li><p>Unlike lightweight traditional models, LLMs require power-hungry GPU clusters to process requests.</p></li>
         <li><p>The architecture of LLMs is vastly heavier - evaluating its billions of parameters requires far more layer-by-layer computation than a narrow AI system.</p></li>
         </ul>
         <p style="font-size: 0.8em;">There are many estimates for LLM energy usage in different contexts, some lower and some significantly higher 
         than the paper I cited above (which gave an estimate of ~200-300 joules). 
         I chose this paper, since it looked at classification tasks specifically and it represented a middle ground between some of the more extreme 
         estimates; the highest estimates reached 10000 joules.
         Of course, as model sizes continue to grow, they will become even more energy-intensive.</p>
      </details>
   </embed>

For all of those reasons, I think that everyone should keep in mind that:  

.. math::

  AI \neq LLM.   

Crucially, narrow AI systems have produced (and continue to produce!) many impressive results. In the following section,
we will have a look at three examples from Google DeepMind that predate the creation of modern chatbots. Looking back today in 2026,
the last one of them may honestly be characterized as the greatest biological breakthrough ever achieved by an AI system.

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
about a model (**DQN** - "deep Q-learning") that could learn to play a wide range of classical 1980s computer games 
(such as Pong, Breakout or Space Invaders) without having any prior description about how those games work.
Instead, they used deep learning methods, letting the model learn by trying to play the games -
providing the game's screen as an input (and the game's score) to the model at every frame.
Model could only interact with the game by choosing which keys to press.

Initially, the model starts out by "pressing" random keys at times. Throughout the training, models
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
There is an `excellent movie <https://www.youtube.com/watch?v=WXuK6gekU1Y>`_ on YouTube which captures the dramatic events and how the world 
of Go was ever changed through it. It also gives some nice visual explanations of the technology behind the breakthrough.

~~~~~~~~~~~~~~~~~~~~~~~~
AlphaFold
~~~~~~~~~~~~~~~~~~~~~~~~

In recent years, leader of fronteir labs have talked a lot about how LLMs could cure cancer in the future. In a longer time span, this may be true;
but in a shorter time span one has to keep in mind that while AI can help with suggesting new drug candidates or biological experiments,
some of the steps can not be so easily side-stepped, like clinical testing and obtaining regulatory approval for drugs.

At the same time, we already have one incredible biological breakthrough in an area that had seen only limited progress in 50 years - protein folding.
The problem's statement sounds innocent enough: given a protein, what 3D shape does this protein molecule take? 
Proteins consist of 22 different amino acids; those can be thought of as "universal LEGO bricks" that the body uses for various purposes.
The role of the proteins is largely determined by the 3D shape that they take (which in turn is determined by which amino acids repel and attract each
other). Here are some examples for illustrative purposes:

* keratin - *long rod-like shape* - important component of hair;
* collagen - *long triple helix shape* - gives strength to bones, tendons, and ligaments;
* hemoglobin (a protein that additionally contains iron) - *a basket-like shape* - transports oxygen into cells;
* antibodies (immunoglobulin) - *Y-shape* - each antibody attaches to a different target (e.g., a microbe or an infected cell) so that the 
  immune system knows to attack that target.

.. image:: /images/part2/4proteins.png
   :alt: 4 proteins (keratin, collagen, hemoglobin, antibodies)

*Illustration: 3D structures of*
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
  conversations.

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

.. raw:: html

   <embed>
      <div class="ai-disclaimer">
      <b>Disclaimer of AI usage</b>: 
      <ul><li>AI (Google Gemini) was used to find additional sources; 
      all sources were manually verified before citing.</li> 
      <li>AI was used to simplify some of the more complex & technical concepts.</li>
      <li>AI was used in the final proof-reading process for pointing out improvement possibilities, but not for re-writing text.</li></ul>
      Total contribution of AI in terms of contribution effort in the process: 5-10%
      </div>
   </embed>

