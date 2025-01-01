

---

# OSPF Configuration and Passive Interfaces Setup

This README describes the configuration of OSPF (Open Shortest Path First) for a simulated network, the implementation of passive interfaces, and general information about OSPF.

## About OSPF

Open Shortest Path First (OSPF) is a dynamic link-state routing protocol widely used in enterprise networks. It ensures efficient and loop-free routing by calculating the shortest path between routers using Dijkstra’s algorithm.

### Key Features of OSPF:
1. **Link-State Protocol**: Each router maintains a database of the network topology, ensuring accurate routing decisions.
2. **Area-based Hierarchical Design**: OSPF divides the network into areas, reducing the size of the routing table and minimizing flooding of link-state advertisements (LSAs).
3. **Fast Convergence**: Changes in the network topology are quickly propagated to all routers in the area.
4. **Scalability**: OSPF is suitable for large and complex networks.
5. **Authentication**: OSPF supports authentication to secure routing updates.
6. **Cost-based Metric**: OSPF uses cost (calculated from interface bandwidth) to determine the best path.

### OSPF States:
1. **Down**: No OSPF packets have been received.
2. **Init**: A hello packet is received from a neighbor.
3. **Two-Way**: Neighbors establish bidirectional communication.
4. **ExStart**: Routers negotiate the master-slave relationship for database exchange.
5. **Exchange**: Routers exchange link-state information.
6. **Loading**: Routers request and load additional LSA information.
7. **Full**: Routers have synchronized link-state databases.

### OSPF Packet Types:
1. **Hello**: Discovers and maintains neighbor relationships.
2. **Database Description (DBD)**: Summarizes the link-state database.
3. **Link-State Request (LSR)**: Requests specific link-state records.
4. **Link-State Update (LSU)**: Advertises routing information.
5. **Link-State Acknowledgment (LSAck)**: Acknowledges receipt of LSAs.

---

## Network Topology Overview

The network consists of six routers (R1 to R6), switches, and PCs interconnected with specific IP address schemes. The topology utilizes OSPF as the routing protocol, with all routers configured in Area 0.

### IP Addressing Scheme
- **R1**: 
  - 1.0.0.1/30
  - 3.0.0.1/30
- **R2**: 
  - 1.0.0.2/30
  - 2.0.0.1/30
  - 4.0.0.1/30
- **R3**: 
  - 2.0.0.2/30
  - 10.1.0.0/24
  - 10.2.0.0/24
- **R4**: 
  - 3.0.0.2/30
  - 4.0.0.2/30
  - 5.0.0.1/30
  - 6.0.0.1/30
- **R5**: 
  - 5.0.0.2/30
- **R6**: 
  - 6.0.0.2/30

---

## OSPF Configuration

Each router is configured with OSPF as follows:

### Router R1
```plaintext
router ospf 1
network 1.0.0.0 0.0.0.3 area 0
network 3.0.0.0 0.0.0.3 area 0
```

### Router R2
```plaintext
router ospf 1
network 1.0.0.0 0.0.0.3 area 0
network 2.0.0.0 0.0.0.3 area 0
network 4.0.0.0 0.0.0.3 area 0
```

### Router R3
```plaintext
router ospf 1
network 2.0.0.0 0.0.0.3 area 0
network 10.1.0.0 0.0.0.255 area 0
network 10.2.0.0 0.0.0.255 area 0
```

### Router R4
```plaintext
router ospf 1
network 3.0.0.0 0.0.0.3 area 0
network 4.0.0.0 0.0.0.3 area 0
network 5.0.0.0 0.0.0.3 area 0
network 6.0.0.0 0.0.0.3 area 0
```

### Router R5
```plaintext
router ospf 1
network 5.0.0.0 0.0.0.3 area 0
```

### Router R6
```plaintext
router ospf 1
network 6.0.0.0 0.0.0.3 area 0
```

---

## Passive Interface Configuration

To enhance security and efficiency, passive interfaces are configured to suppress OSPF hello packets on interfaces connected to end devices or unused links.

### Configuration Example on Router R3
```plaintext
router ospf 1
passive-interface GigabitEthernet 0/0
passive-interface GigabitEthernet 0/1
```

---

## Verification and Troubleshooting

1. **Verify OSPF Neighbor Relationships:**
   ```plaintext
   show ip ospf neighbor
   ```
2. **Check OSPF Routing Table:**
   ```plaintext
   show ip route ospf
   ```
3. **Debug OSPF Processes:**
   ```plaintext
   debug ip ospf events
   debug ip ospf packets
   ```

---

