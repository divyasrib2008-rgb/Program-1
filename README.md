# Program-1Lab Problem Statement: Peer-to-Peer Local Area Network Verification
Scenario:
Expand the standalone host setup by connecting two workstations (PC0 and PC1) through a central Layer 2 switch (Switch0). You must configure both end devices with static IPv4 addresses in the same subnet, establish physical cabling, and verify point-to-point network connectivity.
Specifications
| Device | Interface | IPv4 Address | Subnet Mask | Default Gateway | Connected To |
|---|---|---|---|---|---|
| PC0 | FastEthernet0 | 192.168.10.25 | 255.255.255.0 | 192.168.10.1 | Switch0 (Fa0/1) |
| PC1 | FastEthernet0 | 192.168.10.26 | 255.255.255.0 | 192.168.10.1 | Switch0 (Fa0/2) |
| Switch0 | 2960 Series | Unmanaged / Default | — | — | — |
Implementation & Verification Steps
 1. Place Devices on Canvas
   * Keep the previously created PC0.
   * Under End Devices, drag a second generic PC onto the workspace (defaults to PC1).
   * Under Network Devices \rightarrow Switches, drag a 2960 switch onto the workspace.
 2. Cable the Network
   * Select Connections (lightning bolt icon).
   * Choose Copper Straight-Through (solid black cable line).
   * Connect PC0 (FastEthernet0) to Switch0 (FastEthernet0/1).
   * Connect PC1 (FastEthernet0) to Switch0 (FastEthernet0/2).
   * Wait roughly 30 seconds for the switch ports to transition from amber (spanning tree listening/learning) to green link lights (forwarding), or click the Fast Forward Time button twice.
 3. Configure IP on PC1
   * Click on PC1 \rightarrow select the Desktop tab \rightarrow click IP Configuration.
   * Select Static and enter:
     * IPv4 Address: 192.168.10.26
     * Subnet Mask: 255.255.255.0
     * Default Gateway: 192.168.10.1
   * Close the window.
 4. Verify Link and Test End-to-End Ping
   * Open PC0 \rightarrow Desktop \rightarrow Command Prompt.
   * Confirm PC0's interface is up:
   ipconfig

   * Ping the newly configured peer device:
   ping 192.168.10.26

   * Expected Output: The first packet may occasionally drop or delay due to initial ARP resolution, followed by consistent successful responses:
   Reply from 192.168.10.26: bytes=32 time<1ms TTL=128
Reply from 192.168.10.26: bytes=32 time<1ms TTL=128
Reply from 192.168.10.26: bytes=32 time<1ms TTL=128
Reply from 192.168.10.26: bytes=32 time<1ms TTL=128

 5. Inspect the ARP Table
   * Still in the Command Prompt on PC0, view the resolved hardware addresses:
   arp -a

   * Success Criteria: An entry for 192.168.10.26 must be listed alongside its corresponding physical (MAC) address, confirming complete Layer 2 and Layer 3 resolution.
