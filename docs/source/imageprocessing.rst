.. _image_processing:
Image Processing
================

We need to keep in mind that LoRa radios, despite their great range, have very limited throughput.

So to reduce the time lag between transmitted frames, I needed to reduce the image size by whatever means necessary.

Image compression can only get us so far.
To make the payload even smaller, I came up with an algorithm that cherry-picks important parts of the image and transmits only those.
More precisely, the less informative blocks of an image frame are masked out before transmission.

Here is an overall look at the algorithm:
The image frame is divided into 64 blocks.
Next, image processing and statistical methods are applied to sort the 64 blocks by how informative they are.
A certain number of the high-ranking blocks are then picked and transmitted. The block count is determined by the user in the Settings page of the Elora Vision app.

This algorithm is designed to spot **anomalies** in the frame. I'm good at spotting anomalies. This is what I did for my PhD thesis. Different anomalies, different context, however.

Here are some examples of the algorithm output.

.. image:: ./images/masking_1.jpg
Here we can see that the sky has been excluded from the output frame, as it does not provide too much critical information to the viewer :-)

.. image:: ./images/masking_2.jpg
Perhaps the most informative part of this image is the tractor. It successfully made it through the masking process.

.. image:: ./images/masking_3.jpg
In this drone shot, the campers and their vehicle are highlighted by the algorithm.



In short, the Elora Project app on the Sender Unit can either transmit the full image frame or only parts of it, depending on your choice in the Settings page of the app.


Here is a more detailed explanation of the algorithm workflow.

Every image block is analysed from two perspectives:

1) How many unique hue values exist in the block? Histogram analysis is performed to figure this out.

2) How diverse are the unique hue values in the block? Weighted variance is calculated for this.

Once we have these two ranks figured out for each block, we need a logic based on which we can decide which blocks are the most informative ones.
The logic I used here is the one used in multi-objective optimization. Simply plot the ranks as a Pareto-front and perform a dominance check. The blocks that survive are the ones that are not dominated by any other block.
Finally, pick a pre-determined number of the non-dominated blocks to include in the final image frame.