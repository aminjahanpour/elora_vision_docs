Workflow
========

Network layout
--------------

This project builds around LoRa module which is a low price and long range radio module.

.. image:: ./images/layout.png



Data flow
---------


Here is the flow of information from the Sender Unit to the Receiver Unit(s) for one payload.



You webcam or the Android Phone in the Sender Unit takes a picture. If you are using a phone, GPS info are also acquired. Next, the Elora Vision app performs following operations on the raw image data:

- run image processing algorithms to mask out the less informative blocks of the image (read more about the algorithm here in the :ref:`image_processing` page).
- save the image as JPEG
- add GPS data to the payload (only if you are using a phone)
- encrypt the payload

The app then sends the payload to the Goober via the USB Cable.
The Goober, in turn, transmits the encrypted payload over the on-board LoRa radio module.
At this point, the Sender Unit has finished its job. Now it's the receiver Unit's turn.
The on-board LoRa radio module on your Receiver Unit's Goober picks up the signals from the Sender Unit.
The Goober collects all the encrypted data transmitted by the Sender Unit.
Once ready, the Goober sends the assembled payload to host device.
The Elora Vision app on the Receiver Unit host device decrypts the payload and displays the image (and GPS if available) on the screen.
Finally the Elora Vision app archives all the received information for future references and reports.



.. note::
    **Even if you and other nearby users are on the same frequency, your Goober will ignore the signals from other Goobers.**
    To make this happen, I designed a mechanism similar to how packets are transferred on the Internet.
    Every transmission contains a header which includes a hash term created based on your private encryption key.
    Your Goober only cares about the payloads that carry these specific hash bytes.
    Also similar to the IP mechanism used on the Internet protocol, a payload stores addresses of its sender and the receivers in its header.
    These are all set up automatically for you so don't worry about them. Just know that there will be no interference with other
    nearby users even if you are all on the same exact frequency.







