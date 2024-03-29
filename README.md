# Network Contention Simulator for LoraWAN.

Scalability is an important consideration for Low Power Wide Area (LPWAN) networks. As part of a research study into LoRaWAN at UCL, a network contention simulator was developed in Java (thread-based). The objective of the simulation is to establish baseline figure for packet loss at different modulation rates. Real world packet loss will be higher due  to losses incurred in the Radio Frequency (RF) channel. 

The simulator code has the following features:

* The Java class (runner) is the primary test harness.
* This instantiates threads to simulate the behaviour of LoRaWAN nodes. These nodes wait a random length of time then spawn connection requests.
* Connection threads attempt to acquire an available channel from the connection manager. Successful connections increment the channel occupancy count.
* When the connection drops, the occupancy count is decremented.
* If the selected channel is unavailable, the packet is marked as lost. The percentage of packets lost is recorded.
* The simulation is repeated with more nodes in each run (up to 1000)

**Class (UML) and Sequence diagram**
![UML Diagram](ContentionSimulator/UML.png?raw=true "UML Diagram")

Typical results from the simulation are shown in the figure below:
![Results](ContentionSimulator/results.png?raw=true "Simulation results")

Using spreading factor 7, approximately one thousand nodes can be served with a peak loss of 65%. Increasing the spreading factor to 12 reduces this number to below 30 nodes. It should be noted that this simulation is based on peak packet loss. This provides an indication of the worst-case scenario.

The table below lists assumptions made in creating the simulation.

|	Assumption	|	Detail	
|	:---	|	:---	|
|	Fixed transmission rate	|	For the purposes of simplifying the simulation, each node was assumed to transmit at set intervals. An initial random delay was introduced to ensure separation between transmissions.	|
|	Fixed packet length	|	Time on-air figures for each spreading factor assumed transmission of a 105 byte payload [54]	|
|	Concurrent processing of incoming packets	|	Multi-channel gateways can process packets arriving simultaneously on different channels or on the same channel with different spreading factors. The exact number of incoming packets that can be processed simultaneously depends on the gateway hardware.	|

A full write up of the study can be found [here](ContentionSimulator/sroderick.pdf)

Steve Roderick 2019
