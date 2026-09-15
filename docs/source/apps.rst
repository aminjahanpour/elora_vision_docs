Apps
====

.. _installphoneapp:
How to install the Elora Vision android app on your phone
---------------------------------------------------------

`link to download the android app <https://github.com/aminjahanpour/elora_vision_android_app/releases/download/released/elora_vision.apk>`_


`Click on this link to download the APK file. <https://github.com/aminjahanpour/elora_vision_android_app/releases/download/released/elora_vision.apk>`_ Then, follow the steps to install the app on your phone.
Ignore the possible warnings. The app is completely safe. The source-code is open to the public to verify and evaluate.

.. image:: ./images/android_app_home.png
    :align: center


Expert users could also download the source code from `here <https://github.com/aminjahanpour/elora_vision_android_app>`_, build the project in Android Studio and upload it to their phones all by themselves.

.. note::
    The minimum required android version is Android 6 (Marshmallow).
    I intentionally did this so that older devices can run the app too.
    According to `apilevels.com <https://apilevels.com/>`_, 97.9% of android devices meet this requirement.


.. _installdesktopapp:
How to install the Elora Vision desktop app on your computer
------------------------------------------------------------

The desktop app is written in Python so it runs on any computer with any operating system which can run Python.
The app comes with a graphical user interface which makes it easy to use.

Here are steps to set up and run the app on your desktop computer.


Start a terminal in Windows/Ubuntu/Mac
run below commands:

.. code-block::

    git clone https://github.com/aminjahanpour/elora_vision_desktop.git
    pip install -r requirements.txt
    python main.py


**Notes for Ubuntu Users**

If you are getting error complaining that ``tkinter`` in not installed, run the below line of code to install it on your Ubuntu machine.

``sudo apt-get install python3-tk``


You also might get the below error after pressing *Play*:

``serial.serialutil.SerialException: [Errno 13] could not open port /dev/ttyACM0: [Errno 13] Permission denied: '/dev/ttyACM0'``

The port shown in your case could be different from ``ttyACM0``. The problem can be resolved by granting write permission on that port.
To do so you could run the below command. Replace ``ttyACM0`` with the port you get the error for.

``sudo chmod 666 /dev/ttyACM0``






