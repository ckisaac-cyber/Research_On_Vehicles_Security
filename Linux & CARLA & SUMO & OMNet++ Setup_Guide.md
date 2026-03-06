# Linux & CARLA & SUMO & OMNet++ Setup_Guide

    Since there are no clear guide online for Co-Simulate Linux & CARLA & SUMO & OMNet++ at this point(2025/03/19) so we conclude the our own version that work on the Ubuntu 24.04.2 LTS

## Our System Setup

    - CPU: i9-12900H
    - GPU: RTX 3070 Ti (Laptop)
    - RAM: DDR5 24 Gb
    - System: Ubuntu 24.04.2 LTS
        - Codename: noble
        - build: x86_64
    - Python Version: 3.8.20/3.10.2
        - PIP: 24.0
        - pygame: 2.6.1
        - numpy: 1.21.0
        - traci: 1.22.0
        - lxml: 5.3.1
    - CARLA Version: 0.9.13/0.9.15
    - OMNet++ Version: 6.1/5.4.2
        - inet: 4.5.4/4.2.2
        - veins: 5.3.1 / SimuLTE: 1.2.0
    - SUMO Version: 1.22.0

## Linux Setup 

    1. After Install Ubuntu 24.04.2 LTS
        sudo apt update
        sudo apt upgrade
    2. Check Linux Version:
        lsb_release -a
    3. Check Python Version:
        python -V
        python3 -V    
    4. Install pip3
        sudo apt-get update
        sudo apt install python3-pip
    5. Install python 3.8
        sudo apt update
        sudo apt install software-properties-common
        sudo add-apt-repository ppa:deadsnakes/ppa
        sudo apt install python3.8 python3.8-dev python3.8-distutils
        **Don't Change the defult python version Ubuntu it will cause major system failure**   
    6. Install Nvidia CUDA Toolkit 12.8
        - Check Architecture
            uname -a
        - Install Nvidia CUDA 12.8
            x86_64 version: https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=24.04&target_type=deb_local            
                
            **Don't install NVIDIA Driver just install CUDA Toolkit**

## CARLA 0.9.13 Setup

    1. Install numpy & pygame & limbo5 & carla
        sudo apt update
        python3.8 -m pip install numpy
            - make sure it is numpy: 1.21.0
        python3.8 -m pip install pygame
            - make sure it is pygame: 2.6.1
        python3.8 -m pip install carla==0.9.13
            - make sure it is carla 0.9.13
        python3.8 -m pip install pyCarla
            - make sure it is pyCarla: 0.3.3        
        sudo apt install libomp5
            - Just intstall it don't ask me why
    2. Install Carla 0.9.13
        - Download from https://github.com/carla-simulator/carla/releases/tag/0.9.13/ choose Ubuntu
        - Move the tar file to any location you want to run CARLA
        - Unzip Carla 0.9.13 
            - tar -xvzf CARLA_0.9.13.tar.gz
    3. Run CALA
        - cd to location where you store CARLA
        - Run CARLA
            - ./CarlaUE4.sh
        - Gerenate Traffic in other Terminal
            - cd to /PythonAPI/example
            - run Generate Traffic
                python3.8 generate_traffic.py
            - run Munal Control
                python3.8 manual_control.py

## OMNet++ 6.1 Setup
    
    1. Download from https://omnetpp.org/download/ 
    2. Follow Rule in INSTALL.md
    3. Make folder to store veins & inet
        - Import and Build veins & inet
            - Follow https://youtu.be/PfAWhrmoYgM?si=KDdkgviKtTaXmOjm&t=491

## OMNet++ 5.4.2 Setup
    
    1. Download from https://omnetpp.org/download/ 
    2. Follow Rule in INSTALL.md
    3. Install
        tar xvfz omnetpp-5.4.2-src.tgz
        sudo apt install -f
        sudo apt update
        sudo apt install build-essential gcc g++ bison flex perl qt5-default libqt5opengl5-dev tcl-dev tk-dev libxml2-dev zlib1g-dev default-jre doxygen graphviz
        - Set python to read pyhthon3
        - Use "sudo nano /etc/apt/sources.list.d/
        - Run "sudo apt upgrade qtbase5-dev" to upgrade qtbase5-dev

        ubuntu.sources" to install "libwebkitgtk-1.0"
            - Write the following into the documents
                Types: deb
                URIs: http://cz.archive.ubuntu.com/ubuntu
                Suites: bionic
                Components: main universe
                Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg

        sudo apt update
        sudo apt install libwebkitgtk-1.0
        sudo apt install openscenegraph-plugin-osgearth libosgearth-dev //This might not work

        sudo apt install openscenegraph


        sudo apt-add-repository universe
        sudo apt update
        sudo apt install libopenscenegraph-dev

        cd omnetpp-5.4.2
        sudo apt install openjdk-8-jdk
        sudo apt install libgeos-dev
        ./configure WITH_OSGEARTH=no
        make
        omnetpp

    2.2 Seet up the Command for Pyton
        - sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.12 2

    3. Make folder to store veins & inet & SimuLTE
        - Import and Build inet

    4. File -> Import -> General -> Existing Project -> Select archive file
        - Fow Project such us veins & SimuLTE
            - Right Click Mouse on Project -> Properties -> Project Reference -> selece inet(unselect inet4 for veins)

        - Build veins & SimuLTE
    
    5. Test veins & SimuLTE
        - veins
            Connect SUMO to OMNet++
            - cd where you store veins
            - Use command "python3.8 sumo-launchd.py -vv -c sumo-gui" to listen to OMNet++
            - In IDE open veins/example/veins -> Right Click "omnetpp.ini" -> Select "Run As" -> Switch to Release Configureation "No"
        - SimuLTE
            In IDE open lte/simulations/demo -> Right Click "omnetpp.ini" -> Select "Run As" -> Switch to Release Configureation "No"


## SUMO 1.22.0 Setup

    1. Install pip package 
        python3.8 -m pip install traci
        python3.8 -m pip install lxml
    2. Follow https://sumo.dlr.de/docs/Installing/index.html
        sudo apt install sumo sumo-tools sumo-doc
        sudo apt-add-repository ppa:sumo/stable
        sudo apt update
        sudo apt install sumo sumo-tools sumo-doc
        export SUMO_HOME=/usr/share/sumo


## Testing Guide to run OMNet++ & SUMO
    1. Run OMNet++
        - cd to omnet folder
        - run "source setenv" to run container
        - run "omnetpp" to run OMNet++ IDE
    2. Run SUMO
        - run "sumo-gui" to start the SUMO GUI
    3. Connect SUMO to OMNet++
        - cd where you store veins
        - Use command "python3.8 sumo-launchd.py -vv -c sumo-gui" to listen to OMNet++
        - In IDE open veins/example/veins -> Right Click "omnetpp.ini" -> Select "Run As" -> Switch to Release Configureation "No"


## Testing Guid to run SUMO & CARLA 0.9.13

    1. Install Sumo Version 1.22.0 & CARLA 0.9.13
    2. Run a CARLA simulation with Town04. 
        cd ~/carla
        ./CarlaUE4.sh
        cd PythonAPI/util
        python3 config.py --map Town04
    3. Fix the code in "sumo_simulation.py"
        - File "/Carla/Co-Simulation/Sumo/sumo_integration/sumo_simulation.py", 
            line 304, in _get_sumo_net sumo_net = traci.sumollxmlib.net.readNet(net_file) 
            AttributeError: module 'traci' has no attribute 'sumolib'
        - Change Line 304 from "sumo_net = traci.sumolib.net.readNet(net_file)" to "sumo_net = sumolib.net.readNet(net_file)"
    4. run the SUMO co-simulation example
        cd ~/carla/Co-Simulation/Sumo
        python3 run_synchronization.py examples/Town04.sumocfg  --sumo-gui