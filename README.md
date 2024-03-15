# Part 1
## Overview
In the first part, we implemented a single key-value store server using UDP, TCP, and Java RMI protocols.
## Project Structure
- `GenericNode/executeAllPerformanceTest.sh`: This script executes performance tests for UDP, TCP, and RMI clients.
- `UDPClient`: This class is responsible for sending and receiving data over UDP.
- `TCPClient`: This class is responsible for sending and receiving data over TCP.
- `RMIClient`: This class is responsible for sending and receiving data over RMI.
- `bigtest_*.sh`: The script used to test our server. After executing the test script, the store command should output 70 lines.

## Usage
1. Start the Docker container to call `GenericNode/setupAllContainers.sh`.
2. Execute the `GenericNode/executeAllPerformanceTest.sh` script to do performance tests.

## Performance Tests
- `performanceTestUDP.sh`: Executes performance test for the UDP client.
- `performanceTestTCP.sh`: Executes performance test for the TCP client.
- `performanceTestRMI.sh`: Executes performance test for the RMI client.
- All of above can be done by calling `GenericNode/executeAllPerformanceTest.sh`

Each test measures the time it takes for the client to send a request to the server and for the server to respond. The results are measured using the `time` command and are displayed in three parts: `real` (actual elapsed time), `user` (CPU time used in user mode), and `sys` (CPU time used in system mode).



# Part 2
## Overview
In the second part, we created distributed TCP storage servers that synchronize values across all nodes in the system. Replication is implemented using a two-phase-commit algorithm on write operations. For membership track methods in the system, we use a config or a dedicated centralized TCP server to store the list of servers' IP and port.
## Performance Tests
Performance test can be executed by running GenericNode/docker_client/performanceTestDistTCP.sh
### Set Number of Servers
Number of servers can be set by editing three files below;
- GenericNode/docker_server/DistributedTCP_server/serverlist.cfg (only for the config file tracking method)
- GenericNode/haproxy/haproxy.cfg
- GenericNode/setup_distributedTCP_containers.sh
### Set Node Membership Tracking Methods
You can change node membership tracking methods by modifying GenericNode/GenericNode.java.
![image](https://github.com/tkus1/TCSS545-Assignment2/assets/146398096/7c73292f-922a-44af-9cdf-5e89caab65db)

- TCPServer server = new TCPServer(new ConfigFileGetOtherServersStrategy());
  
  Distributed TCP servers use a config file to track node membership (enericNode/docker_server/DistributedTCP_server/serverlist.cfg).
- TCPServer server = new TCPServer(new CentralizeMembershipGetOtherServersStrategy());

  Distributed TCP servers track node membership by using a centralized membership key/value store.
## Sequence Diagram
- Success

![image](https://github.com/tkus1/TCSS545-Assignment2/assets/146398096/5386216c-3d2c-4967-ac21-f1664783e1ab)

- Fail

![image](https://github.com/tkus1/TCSS545-Assignment2/assets/146398096/62285752-229e-4b1c-88a3-fb30792e0c07)
