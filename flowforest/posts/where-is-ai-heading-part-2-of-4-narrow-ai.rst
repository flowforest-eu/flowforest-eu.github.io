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
But the more I thought about how to best explain LLMs, the more I realized that it is much easier to 
explain the basic concepts on the basis of previous AI systems (++). In particular, models related
to image classification are easy to intuitively grasp and they are very illustrative for concepts that
we will need later on. On the way, we will touch a bit on historical progress and how we have gotten to 
the point that we are in today.

The following timeline high-lights some of the key events in the history of AI:

..
   https://timeline.knightlab.com/

..
   ++ AlphaStar master StarCraft II.

**Important note**: if you scroll through this post, you will see some complex-looking images. Don't be put away (++) by them!
Those are here for illustrative purposes - I will do my best to explain everything in simple and understandable terms.

=========================================
Inspiration for AI - human brains
=========================================

Humans have always been fascinated by how our brains work, and as our understanding of the brain evolved, scientists
started thinking about whether it would one day be possible to imitate the brain artificially. 
Scientist (++ word repeat) have tried to understand, what are the fundamental building pieces of the brain and how do they 
function together to give rise to such complex phenomena (++simplify) like vision, smell, or thinking?

One of the critical parts of the answer are cells called neurons. Together, neurons form networks (++ consisting of millions) that encode memories, 
shape personalities, drive decisions, and process the sensations of touch, taste, sight, smell, and sound (++link).

Some interesting facts about neurons in our brains and bodies:

* An adult human brain contains approximately `80 billion neurons <https://academic.oup.com/brain/article/148/3/689/7909879?login=false>`_.
* A single neuron may be connected to 1000-10000 other neurons.
* The `longest neuron in human body <https://en.wikipedia.org/wiki/Sciatic_nerve>`_ can be over a meter long (from bottom of spine to toes). However, most neurons in brain are less than a millimeter in length.

Hundreds of millions such neurons together enable us to see. (++ make smoother)
However, each individual neuron by itself is not that complicated.
They carry out the following functions:

* they receive inputs (chemical and electrical) from multiple sources;
* they combine those inputs into a single signal;
* if the signal is strong enough, they fire an output that reaches the next neuron (or neurons).

Scientists working in this area thought about the fact (++) that an individual neuron is not that hard to describe mathematically.
Building on that ide, in 1957, Frank Rosenblatt came up with `perceptron <https://www.simplilearn.com/tutorials/deep-learning-tutorial/perceptron>`_,
a simplified mathematical model of a neuron. Just for illustrative purposes, compare a neuron in a brain and an 
artificial neuron:

.. image:: /images/part2/neuron2.png
   :alt: Biological neuron vs artificial neuron

*Biological neuron vs artificial neuron. Source: Towards Data Science (modified).*

Artificial neurons (specifically in the original perceptron model) follow the same core principles as biological neurons, 
but in simplified mathematical form. Artificial neurons:

* receive input values (positive or negative numbers);
* combine those values linearly using specific weights;
* produce an output if the combined value passes a certain threshold (otherwise, the output is 0).

The same basic framework powers the vast majority of neural networks used today (including LLMs). 
The main difference is how the third step works: modern networks swap out the strict "all-or-nothing" threshold for smooth activation 
functions, which scale smaller values down rather than setting them to 0.

..
   last part is too complicated. best to just say "... which have better mathematical properties."

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

.. image:: /images/part2/eye-visual-system.png
   :alt: Neural layers in the eye

*The five neural layers in the eye. Source: Open Neuroscience Initiative (with my modifications)*

Although the image looks complicated, the main idea is fairly simple. Light enters the eye and excites either the cones (in the daylight) 
or the rods (in the night-time). After that, it passes through various layers of neurons, until it reaches the optic nerve.

There are 120 million rods and 6 million cones in the human eye. 
The raw image captured by those rods and cones is heavily compressed before it ever leaves the eye. 
For example, the retinal ganglion cells (marked on the above image) act like a biological image compression algorithm.

The optic nerve consists of ~1.2 million optic nerve fibers. You might think of it as an 1.2 megapixel camera cable.
However, human vision seems much better than a picture taken by a 1.2 megapixel camera, and there are some 
`absolutely fascinating reasons behind it <https://clippingexpertasia.com/blog/human-eye-resolution-explained-megapixels-fps-vision>`_.
+++

After reaching the optic nerve, information is processed 
via a series of neural layers. Here is a rather simplified description of how the visual information is processed in the brain
(`see here <https://en.wikipedia.org/wiki/Visual_system#System_overview>`_ for a more detailed overview):

1. layer: organizes visual information (technically: "LGN layer");
2. layer: detects low-level features: orientation, edges, and lines (technically: "V1 layer");
3. layer: combines simple edges into basic shapes and textures (technically: "V2/V3 layer");
4. layer: processes complex shapes and geometric forms (technically: "V4 layer");
5. layer: detects whole objects, faces, and abstract concepts, e.g., reckognizing a dog, a car, or a number (technically, 1 or 2 layers: "IT cortex").

..
   ++ fact-check me

.. raw:: html

    <embed>
        <p style="font-size: 0.8em;">Since I am not a neuroscientist, the above text may contain oversimplifications or errors. 
        However, the general principle should still be still correct. The full description of how the visual cortex in the brain
        also involving looping effects, complicated time-dependent processes, and some layers serving multiple functions. My description
        is a simplification of a complex process.
    </embed>

This list of layers and information through them illustrates an absolutely crucial point for machine learning: 
the more layers there are, the more complicated relations can be observed from the input data. However, increasing the number of layers also
increases the training time.

==========================
Progress in AI research    
==========================

Early research into neural networks (in 1940s to 1960s) encountered significant challenges.
As mentioned above, those neural networks were primarily confined to single-layer architectures.
Also, the research initially lacked a strong theoretical foundation.
In 1969, a book called `Perceptrons <https://en.wikipedia.org/wiki/Perceptrons_(book)>`_ demonstrated that 
*single-layer networks are fundamentally limited* 
(`mathematical explanation <https://apxml.com/courses/introduction-to-deep-learning/chapter-1-neural-network-foundations/perceptron-limitations>`_ ++), 
and noted that there is no known efficient way to train multi-layer networks.

After that, there were several periods when the interest in AI research was considerably reduced. Such time periods are now
called "AI winters" (`see here <https://news.sparkfun.com/7896>`_ for more exact historical background).
However, there were dedicated researchers who regardless kept pushing the boundaries.

In 1980s, process was made regarding how to train such multi-layer networks - a technique called **backpropagation** was invented.
Training such multi-layer networks is nowadays known as **deep learning**.

.. image:: /images/part2/deep_neural_network.png
   :alt: A simplified illustration of a deep neural network.

*A simplified illustration of a deep neural network. Source: KDNuggets*

After some progress had been made in 1980s and 1990s, progress stalled again. 
Lets fast forward to 2008. In terms of AI, most researchers had moved on to approaches that seemed mathematically more elegant.

A breakthrough came from an unexpected place. A researcher named Fei-Fei Li 
`had an intuition <https://arstechnica.com/ai/2024/11/how-a-stubborn-computer-scientist-accidentally-launched-the-deep-learning-boom/>`_ 
that progress could be made if a more comprehensive training dataset was built (++). This was based on her own prior experience with
machine learning. She was also inspired by an 
`estimate <http://wexler.free.fr/library/files/biederman%20%281987%29%20recognition-by-components.%20a%20theory%20of%20human%20image%20understanding.pdf>`_ 
by vision scientist Irving Biederman that the average person 
recognizes roughly 30,000 different kinds of objects.    
With just a few colleagues, limited funding, 2 years of hard work, and a lot of ingenuity, she managed to compile a dataset of 14 million images, 
annotated into 22 000 categories, which she named **ImageNet**. She released it in 2009. To help to popularize it, she also launched an
image classification competition for AI systems.

In 2010 and 2011, winners of the ImageNet competition used techniques that were only slight improvements from the state of the art. (++ Moreso, they .. 
hand-crafted ..).  
In 2012, Alex Krizhevsky, Ilya Sutskever, and Geoffrey Hinton won the ImageNet competition using an AI system **AlexNet**, which was based
on an architecture called 
**Convolutional Neural Network** (**CNN**). It crushed the competition with an error rate of just 15% 
(winners of 2011 and 2010 had error rates of 26% and 28%, correspondingly), while the training time dropped from months to days. 
This event was a huge catalyst for the following boom in deep learning (and AI in general).

CNNs have multiple interesting and useful properties. First of all, their training process could efficiently be parallalized using
`GPU chips <https://www.ingameloop.com/graphics-cards/learn/what-does-a-gpu-do-for-gaming/>`_, 
which brought huge performance gains. Second, CNNs have a property that we already observed in human brains: 
as information moves through subsequent layers, 
`these layers start to represent increasingly complex concepts <https://arxiv.org/pdf/2108.00107>`_:

* earlier layers detect edges and colors (e.g., the edge of an orange stripe);
* following layers start to combine them into texture-like feature groups (e.g., an orange-white striped pattern);
* later layers assemble whole object parts (e.g., fin of a clownfish);
* final layers detect the object class (e.g., a clownfish).

**Note**. The AI model AlexNet mentioned above had 8 layers and approximately 60 million parameters.

.. image:: /images/part2/clownfish.jpg
   :alt: A clownfish.

| *A clownfish. CNNs like AlexNet proved to be efficient at classifying such complex images.*
| *Source: Aquarium of the Pacific*

======================================
But how does this learning happen?
======================================

There are some similarities between learning in humans (especially babies) and how AI models are trained, and there are many 
crucial differences. Before we dive into those, it is useful to think a bit about how babies learn.

At birth, babies do not see colors - their vision is black and white. 
Babies at about 1 month of age do not yet see the world clearly - their vision is 
`blurry <https://www.nationwidechildrens.org/family-resources-education/health-wellness-and-safety-resources/helping-hands/infant-vision-birth-to-one-year>`_
and they cannot see very far. (++)
Research from 2024 `has also shown <https://neurosciencenews.com/infant-vision-development-ai-27078>`_ that babies prefer to 
look at simple, high-contrast patterns and edges found in everyday environments; furthermore, this is very important
for the development of their visual skills. At later stages of child's development, they start to reckognize and understand
more complex visual aspects.

What follows is that learning and development of visual system happen in parallel - as babies' eyes develops to allow for 
seeing more complex input (from black-and-white to color, from blurry and short-sighted to sharp and long-sighted ++), brain learns
to reckognize and interpret increasingly complex patterns from it (++). Above, we discussed what the different neural layers 
in the brain's visual cortex are - at different stages of the brain's development, different layers are going through the most active 
process of learning and adaption. (+++)

To give a concrete example, imagine kids of different ages who are seeing a wooden Jenga block for the first time in their life.
Each of them will be curious about this new object, and this curiosity will cause them to make observations, but depending on their 
age and development stage, they might focus on different aspects of that Jenga block:

* the youngest (a baby) might focus just on its color (and put it to his mouth, which is also a way of learning about the world);
* a slightly older kid will focus on it having straight edges;
* next kid might concentrate on the texture of the wooden block;
* and the oldest of them could notice all of the previous, associate it with the words "Jenga block" that he heard from his parents, and memorize
  this new concept. (++ concrete ages?)

Every time a kid learns something, it causes some neural connections to be strengthened or new connections to be formed. Sleeping also plays a 
crucial role in this process. (+++ learn more)

What is interesting is that a baby at the moment of birth has already almost 
`all of the neurons <https://scienceinsights.org/how-developed-is-a-babys-brain-at-birth/>`_ that the adult will have. 
The learning process is not about *producing new neurons*, it is about the process of new connections (**synapses**) *forming* 
between the existing neurons, unused connections being pruned (removed), and the strengths of connections changing.

..
   There is also a process in brain development for making existing networks quicker (*myelination*). 
   https://www.zerotothree.org/resource/what-are-the-most-important-changes-in-the-brain-after-birth/
 
Lets now think about AI models, their training, and the similarities and differences compared to human learning.
First, the analogue of a biological synapse (connection between neurons) is a **weight** in an AI model. Here is again the image from above. 
Bigger arrows correspond to larger weights. 

.. image:: /images/part2/neuron_only.png
   :alt: Artificial neuron

*Artificial neuron. Source: Towards Data Science (modified).*

In neural nets, weights can also have a negative value (not depicted on the image above). This has the effect of that neuron acting as a brake
for the next layer (the technical term is "**inhibition**"). This also happens in the human brain in various contexts. In the context of vision,
this happens at the edge where a darker object and a lighter object meet (for example a dark tree next to a bright sky). When light hits the
receptors in the eye, neurons fire strong active signals ("it is bright here") and *also send* inhibitory (negative) signals to *their neighbor neurons*.
This causes the borders between dark and bright objects to have a lot of contrast and look crisp. At the same time, this process (called
`visual lateral inhibition <https://en.wikipedia.org/wiki/Lateral_inhibition#Visual_inhibition>`_) is exactly the cause for 
`several optical illusions <https://en.wikipedia.org/wiki/Grid_illusion>`_ where we see dots appearing on white background.

The word "learning" in the context of AI models means that during the training process some weights are strengthened and some are weakened. 
The mathematical operations themselves connecting the previous layer with the next one do not change; only the weights do. 
This begs the question: how does the training process know which weights to change to produce a useful AI model such as the AlexNet?

**Remark**. *Keep in mind that computers does not see "see" the image as we do. Instead, they see an image as a 2-dimensional grid of pixels,
and each pixel is just 3 numbers for the AI model - corresponding to the amount of red, green, and blue in that pixel.
In that sense, for AI an image is just a grid of numbers.*

As an initial step, a model is chosen with all of the weights being completely random in a given range.
In the example of AlexNet, this means that the model will produce completely random outputs (e.g., classifying a image of random noise
as an elephant). Now, at each step, the following happens:

* A small batch of images (e.g., 128 images in case of AlexNet) is chosen randomly.
* For each of the images in that batch, the error rate is calculated (how good or bad the prediction was).
* Using clever mathematical techniques (++link), it is calculated for *each weight* how much changing that specific weight in a 
  positive/negative direction would have affected the error rates of the model for the given batch of images.
* Each weight is changed by a tiny amount in the direction (calculated in the previous step) that most improves the error rates.

This process is then repeated millions of times; if everything goes as expected, the error rates should start to fall and the 
model should learn to recognize features and classify images correctly and reliably. 

**Remark**. *Mathematically, the hard part is calculating how changing of each specific weight would have affected the resulting error rate,
since each layer also affects each subsequent layer as well. Remember that a single image classification model will have tens or hundreds of 
millions of parameters, so the efficiency of this calculation is crucial. This is the problem that the*
`mathematical technique of backpropagation solved <https://www.geeksforgeeks.org/machine-learning/backpropagation-in-neural-network/>`_.
*Recall from the historical overview above that backpropagation was invented only in 1980s after several decades of research into this area.*

Lets walk through an example of how this training process starts. We are at the first step, where the model has been initialized randomly. 
The image that we are given depicts a slightly cloudy sky and the image has been classified (by a human, before training) as the "sky".
In the network that has been initialized randomly, there will be neurons in the earlier layers which respond to the blue color; 
and there will be neurons in the layer laters that eventually lead to the image class "sky" being activated. Since we have just started training,
the image is as likely to be classified as the "sky" as an "orange". Since the number of neurons is large, there will be (just by chance) 
some neurons that react to the color blue and eventually affect the result being classified as the sky. So if the given batch contains 
images of sky, those weights that support this relationship ("lot of blue => image could depict the sky") are strengthened. At the same time,
alternative relationships (e.g., "lot of blue => image could depict an orange") are weakened.

Of course, this is just the easiest type of heuristic one can have. In order to become truly effective at classifying images 
(e.g., images of the sky), the model has to learn to (i.e., find weights that enable to):

* detect areas of same color, edges, lines, orientation of features;
* understand how simple edges combine into basic edges and textures;
* how complex shapes consist of simpler shapes and geometric forms.

Take the the example of detecting a clownfish. Lets say that model has learned that clownfishes have orange and white stripes on them.
The detection capability of the model will increase if it also starts making sure that those orange and white stripes are next to each other
and alternate in color. For this to happen, some neurons in the later layers have to specialize to respond to the positional information of 
those shapes (orange/white stripes) that were detected in the preceding layers.

I recommend to make a small pause here. Think about some specific object in the world and think about how do you recognize 
it from an image. Try to imagine the features that define it; think how the model might learn to detect it (given that there are images 
in the input data where recognizing this feature is beneficial).

The last part is crucial: the model may take "shortcuts" if the input data does not punish for it. There is a 
`famous study <https://arxiv.org/abs/1807.04975>`_ that showed that image detection models often rely extensively on the context for 
detecting animals (specific example: cows are usually photographed on grassy pastures). If ones moves the cow to a new context
(e.g., cow on a paved road, or cow on a beach), the model will fail to classify it as a cow. 
What happened was that instead of learning the complex anatomical features of a cow (ears, muzzle, body shape), it learned a 
simpler rule: "somewhat cow-like animal on green grass => cow". This is an example of what is called **shortcut learning**.

To be completely honest, I think that humans would also do somewhat worse at detecting cows on beaches. To see what I mean, just look at
the images on `page 2 of the PDF linked above <https://arxiv.org/pdf/1807.04975>`_. 

The solution is to enrich the dataset of images to have variation of contexts, backgrounds lighting, viewpoints and shapes. It is also useful
to incorporate images taken by different photographers and camera types.

Now, for something completely different, I would like to present a *visual explainer* of a CNN model.
It is a webpage that runs a CNN model called "Tiny VGG" *directly in your browser*, allowing to upload your own image and 
see the classification model crunching through it before your own eyes.
However, this model only accepts tiny images (64x64 pixels) and sorts the images to one of 10 pre-defined classes.
This is intentional; firstly, it enables the model to run smoothly in a web browser. Secondly (and even more importantly), 
this allows the model to be simple enough to visually illustrate what really happens at each step. Try clicking on different 
steps to get an intuitive understanding of what happens at various steps and how the model "sees" the image.

A word of warning, though - since my overview of the topic has been rather high-level, I have not given all of the necessary
definitions for understanding CNNs. I have not explained concepts like *convolutional layers*, *kernel layers*, *ReLu activation*,
*max pooling* that are used in the visual explainer page. If you want to learn those definitions, open the collapsible accordion 
box below. If not, just head directly to the `visual explainer page <https://poloclub.github.io/cnn-explainer/>`_.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to learn the technical terms about CNNs used in the visual explainer page</summary>
         <ul>
            <li><em>Convolutional layer</em> - A layer in CNN model where each neuron is connected to all neurons in the previous layer.</li>
            <li><em>Kernel layer</em> - A layer in CNN model where each neuron is only connected to a small amount of the neurons from 
            the previous layer, e.g. those that correspond to the closest 3x3 pixels (the <em>kernel</em>).</li>
            <li><em>ReLu activation</em> - An activation function that maps negative values to 0, but keeps positive values intact. Imagine a 
            neuron in the brain that blocks negative (inhibitory) signals.</li>
            <li><em>Max pooling</em> - A layer that applies the <em>softmax</em> operation, normalizing the sum of all weights to be 1.</li>
            <li><em>Hyperparameter</em> - Any parameter of the model that is not trained; the machine learning researchers have to 
            manually choose those instead based on their experience / intuition.</li>
         </ul>
      </details>
   </embed>

In this section, we looked at the process that AI researchers go through for producing a useful AI model like AlexNet (++).
All of those steps can be shortly summarized as such (++): 

* Collect sufficient **input data**, classified with sufficiently high accuracy.
* Define the **goal function**.
* Choose a **model architecture** (e.g., CNN).
* Initialize the model with **random weights**.
* Run the **training process**.

================================================
How to look inside the model?
================================================

Lets consider a seemingly simple question - "do we fully understand how those models work?"

On the one hand, for a given local model, we fully know what is the model's architecture. 
Also, at any point of training, all of the weights are known and can be inspected.
But there are things which are harder to assess:

* What kind of patterns or capabilities has the model learned?
* Which neurons are relevant or necessary for a given pattern or capability?

It is entirely possible to follow the mathematical calculations - understanding the meaning behind the weights is harder to do.

Neuroscientists face the exact same challenge when studying biological brains. If you show someone an image of a cat, you can observe which 
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
One of those techniques is a `saliency map <https://en.wikipedia.org/wiki/Saliency_map>`_. 
It is used to high-light the pixels in the input image that were most strongly used in the 
process of assigning the category label (e.g., "a chair" or "a cow"). Recall the earlier example where detection of cows relied on detection of 
grass by an extensive amount. In that case, the saliency map would strongly high-light the pixels containing grass, which would inform the 
researchers of the problem. Researchers could then fix it by enlarging the dataset by cows in other context (e.g., on
a paved road).

There is another very interesting technique for visually understanding what a given neuron (or a group of neurons) in the neural net reacts to.
For this, an image with random noise is taken. After that, it is gradually modified so that it becomes an image that makes the *previously chosen
neuron* to be maximally active. This often produces some quite psychedelic images that are filled with the object that this neuron reacts to.
In the next image, we can see a feature visualisation for a group of neurons that activates *for dog eyes*.

.. image:: /images/part2/feature_visualisation_dog.png
   :alt: Example of a feature visualisation.

*Example of a feature visualisation (dog eyes). Source: Distill*

This page allows to `navigate through feature visualisations <https://distill.pub/2017/feature-visualization/appendix/>`_ of a CNN model
called GoogLeNet. Notice that initial layers (3a and 3b) correspond to simple textures, whereas later layers correspond to more 
complicated concepts. For each layer, there are visualisations that maximally excite a group of neurons ("positive channel") and visualisations that 
least excite that same group of neurons ("negative channel"). More explanations can be found `here <https://distill.pub/2017/feature-visualization/>`_.

===================================================
The importance of choosing a good goal function
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

=========================================
What else has deep learning given us?
=========================================

After AlexNet was released in 2012, the field of deep learning experienced an avalanche of renewed interest. 
Progress was made (using various deep learning techniques) in areas such as speech recognition, image generation, 
image classification, and machine translation. 

One of the major sources for innovation in that time period was a company called DeepMind 
(founded in 2010 by Demis Hassabis, acquired by Google in 2014). 
I would like to mention 3 areas where they successfully applied deep learning methods.

.. raw:: html

    <embed>
         <h3>Playing 1980s computer games</h3>
    </embed>

In 2014, Google Deepmind 
`published research <https://deepmind.google/blog/deep-reinforcement-learning/>`_
about a model (**DQN** - "deep Q-learning") that could learn to play a wide range of classical 1980s computer games 
(such as Pong, Breakout or Space Invaders) without given *any description* about how those games work.
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
that there exists some well defined goal function (like the game's score).

This also means that in the case of reinforcement learning, the model might find solutions that humans did not anticipate or 
were not aware of. Here is a video of how this happened in the game of Breakout - model discovered a
`nice strategy <https://www.youtube.com/watch?v=TmPfTpjtdgg>`_
that the team in DeepMind had not been aware of.


.. raw:: html

    <embed>
         <h3>AlphaGo</h3>
    </embed>

After the dramatic chess matches between Garry Kasparov and a computer algorithm named Deep Blue (developed by IBM) in 1996 and 1997, 
chess engines continued to improve. Chess players slowly came to accept that machines are and will remain superior to human players.
The game of Go, however, was a different story - until 2015, the strongest computer programs played at intermediate level at best.
The board size is huge (19x19) and the number of possible games is staggering (that number has 173 digits). The difference with chess is 
that it is much harder to assess a position and say who is in the lead; the advantages become clear only in the end-game, where 
the score is solidified. Playing the game requires relying significantly more on one's intuition and experience.

Google Deepmind 
`developed AlphaGo <https://research.google/blog/alphago-mastering-the-ancient-game-of-go-with-machine-learning/>`_
using a combination of machine learning and tree search techniques, combined with extensive training, 
both from human and computer play. It is fascinating that the models that they trained for playing Go were CNNs -
the same architecture that AlexNet used. However, this time the inputs to the models were states of Go games, not images.

Since I want to keep this post length reasonable, I leave the choice to the reader - feel free to read the technical details of how AlphaGo
works at a technical level, or skip it.

.. raw:: html

   <embed>
      <details>
         <summary>Click here to read how Deepmind trained two CNN models for playing Go</summary>
         <p>The first neural network, the <strong>policy network</strong>, predicts the next move, and is used to narrow the search 
         to consider only the moves most likely to lead to a win. The second neural network, the <strong>value network</strong>, is 
         then used to reduce the depth of the search tree - estimating
         the winner in each position in place of searching all the way to the end of the game.</p>
         <p>The training process started with training (++) the policy network, which predicts the next move. (++rep)
         It was initially trained by using <em>supervised learning</em> on 30 million moves from games played by human experts,
         until it could predict the human move 57% of the time.
         After that, the policy network was improved by reinforcement learning - AlphaGo played thousands of games with itself
         and used the game's final result (win or loss) as the <em>goal function</em> to reinforce the weights behind the strategies that
         consistently lead to winning (++).</p>
         <p>This policy network was then used to train a <em>value network</em> via reinforcement learning and self-play.
         The obtained value networks were able to evaluate any Go position and estimate the eventual winner with high reliability -
         a problem so hard it was previously
         <a class="reference external" href="https://www.sciencedirect.com/science/article/pii/S0004370201001217">believed to be impossible</a>.
         For a more in-depth description, I recommend to read either their
         <a class="reference external" href="https://research.google/blog/alphago-mastering-the-ancient-game-of-go-with-machine-learning/">blog post</a> or
         <a class="reference external" href="http://www.nature.com/nature/journal/v529/n7587/full/nature16961.html">paper in Nature</a>.</p>
      </details>
   </embed>

In 2016, AlphaGo played a match against Lee Sedol, one of the best Go players in the world - and won 4:1.
There is an `excellent movie <https://www.youtube.com/watch?v=WXuK6gekU1Y>`_ on YouTube which captures the dramatic events and how the world 
of Go was ever changed through it. It also gives some nice visual explanations of the technology behind the breakthrough.

.. raw:: html

    <embed>
         <h3>AlphaFold</h3>
    </embed>

123

https://en.wikipedia.org/wiki/The_Thinking_Game

=========================
Narrow AI vs general AI
=========================

**GOAL: KEEP SIMPLE**

+++
// One of the ways to divide AI systems is between narrow AI and general (or "wide") AI. 
Narrow AI systems are trained to fulfil one function and do it well; general AI systems can execute a wide variety of tasks, depending on the prompt. (ALT: general AI systems can fulfil various goals, depending on the input prompt). LLMs and other generative models (e.g., for video and audio generation) are examples of general AI; here are some examples of narrow AI systems that are still in use today (with the year number of when the model was released ++). (ALT: TO_THINK: "are relevant today or were when they were introduced)

+++ Hm. Does not make sense: calling video generation "general". Hm.

Some of the functions of narrow AI models have been taken over (superceded by) LLMs (++? general AI): ...

TODO: Read about image classifiers, ... etc. various examples. Have they been beaten by LLMs altogether?

?? +++?? image: Venn-diagram type of different terms and taxonomy. Transformer. General. Narrow. LLM. Video generation. Audio generation. Generative AI.

Narrow AI has also given a wide range of medical breakthroughs:
+++

..
   Add? In common discourse about AI models and their implications for the society, narrow and general AI models are often lumped together, which creates confusion and makes it harder to have constructive dialogue with the public;
   Add? The security properties for narrow and general AI models are vastly different, with narrow AI systems being much safer by their nature (you do not need to worry about an image classification network causing malicious actions in your computer network).

==============
Conclusion
==============

**GOAL:  KEEP SIMPLE AND SHORT. Name: summary / conclusion**.

Although neural networks are inspired by neural structures in brains, there are limits to that analogy, which are important to keep in mind. (++)
Also, machine learning experts are not trying to emulate or replicate human brains exactly - instead, they try to build on neural nets that have 
previously worked, and try to improve and find algorithms that work well on machines (GPUs and all). (++++++)

Ways how brains are different from artificial neural nets: (++)

* Much more complex
* Biological, quantum effects
* Neural networks in brains often run in loops (most neural nets do not loop; but there are `exceptions <https://en.wikipedia.org/wiki/Recurrent_neural_network>`_)
* Learning happens completely differently

++ In next post: ...

++ disclaimer below

.. raw:: html

    <embed>
        <p class="ai-disclaimer"><b>Disclaimer of AI usage</b>: AI was used to find additional sources; all sources were manually verified before citing. AI was used to simplify some of the more complex & technical concepts.</p>
    </embed>

====================================
Turing award in .. (Nobel ..)
====================================

**GOAL: KEEP SHORT**

In 2014, GAN (Generative adversarial network) .. was introduced by Ian Goodfellow and others (under supervision of Yoshua Bengio) 
... - one network (discriminator) tries to detect AI-generated images, 
another network tries to fool it. At the same time, the discriminator also keeps learning and improving.
This creates an "arms race" between the two models. 

+++?
Yoshua Bengio, Geoffrey Hinton and Yann LeCun were awarded the 2018 Turing Award for 
"conceptual and engineering breakthroughs that have made deep neural networks a critical component of computing".
https://awards.acm.org/about/2018-turing

+++?
While the use of artificial neural networks as a tool to help computers recognize patterns and simulate human 
intelligence had been introduced in the 1980s, by the early 2000s, LeCun, Hinton and Bengio were among a small group 
who remained committed to this approach.

+++?
Though their efforts to rekindle the AI community’s interest in neural networks were initially met with skepticism, 
their ideas recently resulted in major technological advances, and their methodology is now the dominant paradigm in the field.
(2018)

+++? https://awards.acm.org/about/2018-turing
In addition to the products we use every day, new advances in deep learning have given scientists powerful new tools—in areas 
ranging from medicine, to astronomy, to materials science.”

+++
weaknesses of deep learning models about text:
Key Concept: Contrast old sequential models (like RNNs/LSTMs that read word-by-word and forgot the beginning of a long essay) with 
Transformers, which look at an entire block of text all at once.

Yann LeCun
In the late 1980s, while working at the University of Toronto and Bell Labs, LeCun was the first to train a convolutional 
neural network system on images of handwritten digits. 
<-- lisan ülesse?

Yann LeCun
backpropagation
<-- lisan ülesse

