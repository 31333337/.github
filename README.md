# 0KNetwork

## What is 0KNetwork?

0KN is a next generation decentralized and incentivized metadata-private mixnet-based anonymous broadcast network with cryptographic security guarantees.
0KN is a decentralized privacy network infrastructure that is designed to preserve user anonymity in the face of an adversary monitoring the entire network and while assuming a fraction of all network servers are malicious. It leverages the next generation state-of-the-art mixnet based metadata-private anonymous broadcast **Trellis**.

### What's next? 
We are in a research phase and preparing public testnet in the following weeks. Currently you can use some Ansible playbooks to deploy things yourself and even scale it ona k3s cluster. 
- after robust testing and r&d we will start integrating this into Cosmos-sdk but that might come after some form of first testnet.



## Network Overview

Trellis operates as a layered mixnet, with messages routed through random, anonymous paths.
Anytrust groups at the entry and exit points ensure the system resiliency against denial-of-service attacks.
Each server in the network verifies the routing instructions independently, ensuring each message is properly routed.
The system supports repeated broadcast rounds for efficient message mixing.

### Anonymous Routing Tokens (ARTs)

ARTs are generated by users and signed by an anytrust group to set up anonymous paths for message delivery.
Each ART encapsulates necessary information for servers to route messages, providing both anonymity and path randomness.
ARTs are designed to be untraceable and unforgeable, ensuring both sender anonymity and the integrity of the routing information.

### Boomerang Routing

Boomerang routing is a technique where messages are sent out and then returned, effectively doubling the anonymity provided.
It's used in Trellis to ensure all servers on the path verify the correct receipt and delivery of the message.
This method also helps to immediately assign blame in the case of dropped or altered messages, improving the system's accountability.

## Real-world scenario 

Alice, a whistleblower, and Bob, a journalist, to this story. Alice needs to share some sensitive information with Bob over Signal, but they're both concerned about a global adversary who might be watching. To protect their communication, they use Trellis.

Here's how it works:
- Random Path Selection: When Alice sends a message to Bob, it doesn't go directly to Bob. Instead, it travels through a sequence of servers, known as a mix-net. The path through this network is randomly chosen by Trellis and is unknown to any single server in the network. This random selection of the path makes it very difficult for an adversary to trace the message from Alice to Bob.
- Encryption and Anonymization: Each message that Alice sends is encapsulated within layers of encryption (similar to the layers of an onion) and signed with - Anonymous Routing Tokens (ARTs). These tokens contain the necessary information for each server to forward the message to the next server, but are designed in such a way that they can't be traced back to Alice. This ensures that even if an adversary is watching the network, they can't determine that the message came from Alice or where it's going to Bob.
- Protection Against Traffic Analysis: To protect Alice and Bob further, Trellis uses a technique known as 'dummy traffic'. Even when Alice isn't sending messages, dummy messages are sent through the network. This makes it harder for an adversary to correlate the timing or volume of messages with Alice's activities.
- Accountability Measures: If any of the servers in the mix-net deviate from the protocol, for example by dropping messages or failing to maintain the anonymity of its users, Trellis has mechanisms in place to identify and blame that server. This provides additional protection for Alice and Bob against potential inside attackers.
**
By using Trellis, Alice can send her sensitive information to Bob over Signal, without revealing her location or the fact that she is the sender of the message. This protects both Alice and Bob from the global adversary who might be trying to track their activities through metadata observation.**

### What if they did not use Trellis?
If Alice and Bob didn't use Trellis to protect their communication over Signal, they would be far more vulnerable to a global adversary. Here's why:

- Direct Path: Without Trellis, when Alice sends a message to Bob over Signal, it would travel directly from Alice's device to Bob's. This makes it far easier for an adversary who is watching the network to trace the communication from Alice to Bob.
Metadata Exposure: Even though Signal itself uses end-to-end encryption for the content of the messages, the metadata of the communication - such as the time the message was sent, the size of the message, and the fact that there was a communication between Alice and Bob - is still exposed. This metadata can reveal a lot about Alice's activities and connections.
- No Protection Against Traffic Analysis: Without the use of dummy traffic, an adversary could analyze the timing and volume of Alice's messages to gain additional insights about her behavior, which could potentially compromise her anonymity.
- Lack of Accountability Measures: Without the accountability measures provided by Trellis, any server that deviates from the protocol (for example, by dropping messages or failing to maintain the anonymity of its users) would go unnoticed. This could potentially expose Alice and Bob to inside attackers.
- Timing attacks


So, without Trellis, Alice and Bob's communication would be far less secure. Even though the content of their messages would be encrypted by Signal, the metadata of their communication would be exposed, making it far easier for an adversary to trace their activities. The use of Trellis provides an additional layer of security, protecting the metadata of Alice and Bob's communication and making it far more difficult for an adversary to track them.
