# Master-Guide
Primary KanBan Board across projects and quickstart guide introducing new devs

## Quickstart
To replicate the Nvidia Jetson board on your machine, you can use Nvidia-Docker (https://github.com/nvidia/nvidia-docker) to make sure your environment is sane and correctly set up.

Once you know this works, you can clone the base docker image in our Docker-Devenv (https://github.com/UND-Robotic-Mining-Team/docker-devenv) and fork off a new project for additional functionality.

Inside of these projects is where the majority of work will be done. Inter-container communication will be established through REST requests (http://code.mrtazz.com/restclient-cpp/), allowing containers to request the CAN interface to direct the rover. This means that switching from automatic control to e.g. an Xbox Controller would be a simple matter of shutting down one service and waiting for operational commands from another.

What work needs to be done to get here?

1. Implement a REST server within the primary motor controlling software (See https://gitlab.com/eidheim/Simple-Web-Server/blob/master/http_examples.cpp for examples)

2. Implement REST requests within the current controller interface on Windows, and within the existing software.

3. Work on creating two separate docker images: one that will interface with the front camera, and another that will interface with the back one. Have a separate sensor-tasker project that will manage the information from these, make decisions, and allow a UI over the network to control decisions.

4. (Optional) create a minimal data converter to keep full REST requests from going over the network, to minimize data transmission.


## Other Tasking ##

SystemD Unit Scripts need to be written for process management and startup. Firstly, on boot the CAN bus needs to be initialized. There's likely existing scripts that will search for USBCAN devices and help with this, may be worth some searching on Github.

OpenCV and YOLO need to be looked into. Specifically, AruCo markers in OpenCV need to be used to localize our rover with the rest of the region.
