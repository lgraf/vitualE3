# virtual E3
Virtual E3 device for testing reading and writing DIDs for **testing of ioBroker adapter** [e3oncan](https://github.com/MyHomeMyData/ioBroker.e3oncan.git).

This is a fork of project [virtualE3](https://github.com/philippoo66/vitualE3.git).

For testing you need a **virtual CAN bus** to connect both the ioBroker adapter and virtual E3. To setup virtual CAN "vcan0" please refer to https://netmodule-linux.readthedocs.io/en/latest/howto/can.html. For typical linux setup it's done like this:
```
ip link add dev vcan0 type vcan
ip link set vcan0 mtu 72
ip link set up vcan0
```

Now you can setup and start virtual E3. After cloning the repo install required packages and start the application:
```
pip3 install -r requirements.txt
python3 virtualE3.py -cnfg devices.json
```

This version of virtual E3 brings two pre-installed virutal devices (HMI, VCMU) including sample data.

When virtual E3 is up and running you may start the ioBroker adapter e3oncan, connect it to vcan0 as external can adapter and complete the adapter setup for further testing. As of now, the testing works for **UDS functionality only**. Virtual E3 does not support the listener option ("collecting") of e3oncan.

There are further options available for use of virtual E3:

# Usage

    python3 virtualE3.py [-h] [-c CAN] [-dev DEV] [-old] [-dyn] [-a] [-addr ADDR] [-cnfg CONFIG]

    arguments:
    -h, --help            show this help message and exit
    -c CAN, --can CAN     use can device, e.g. vcan0 (default)
    -dev DEV, --dev DEV   boiler type --dev vdens or --dev vcal or --dev vx3 or
                        --dev vair or _680 or _6A1 or ... (ignored when -cnfg is set)
    -old, --old           -old for not universal list
    -dyn, --dyn           -dyn for dynamic values (virtdyndata.py required configured)
    -a, --all             respond to all COB-IDs
    -addr ADDR, --addr ADDR
                        ECU address (default 0x680)
    -cnfg CONFIG, --config CONFIG
                        json configuration file of Open3E (dev short for devices.json)

# Requirements

https://pypi.org/project/python-can/

https://github.com/pylessard/python-udsoncan.git
