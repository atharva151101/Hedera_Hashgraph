# Hedera-Hashgraph
Simple Implementation of the Hashgraph Consensus Algorithm along with its visualization.

Based on the paper https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf

## Running the code
 - Install the requirements from requirements.txt
   ```
   pip install -r requirements.txt
   ```
 - Run the Python notebook.
 - The program just requires the graph as the input in the following format
   - The first line should be a single integer containing the number of nodes
   - All the subsequent lines describe an event. Each 
   The last line should contain a single word "Done" indicating the end of input
 - The program would generate the following files -
   - A txt file containing the consensus order for the events
   - A .dot file with the dot code for the Hashgraph
   - A PNG image for the Hashgraph using the above dot file
 - Additionally, the program can be used to visualize the intermediate steps too in the consensus algorithm.
  
  

## About Hashgraph
Hashgaph is a distributed ledger used to achieve Byzantine agreement and is considered a 
more efficient alternative to the current blockchain technology. https://hedera.com/ is
a decentralized, proof-of-stake public ledger that utilizes the Hashgraph consensus 
algorithm.

Hashgraph achieves consensus through frequent communication (aka gossip) between all the members. A gossip can entail any real-life practical event like a transaction. The protocol in short can be termed as "gossip about gossip", where the participating members not only gossip about the individual events but the whole Hashgraph itself i.e. the complete history of all the "gossip" or events that a member has created or received from other members.

## Outiline of the Consensus Algorithm 
 - Each member of the population maintains a Hashgraph, which contains the history of all the gossip that has happened until now. Every member can have a separate copy of the Hashgraph, but the algorithm ensures these Hashgraphs are consistent i.e. the ordering of events that is determined as per the consensus algorithm would be the same for all.
 - Alice (one of the members) chooses another member Bob by random and gossips all the events that Alice knows. This communication event of Alice to Bob is itself marked as a new event by Bob.
 - The consensus algorithm divides all the events into separate rounds. For any given member, the first that the member creates for a given round is termed a "witness" event.
 - There is a virtual voting that occurs between the witness events to determine whether a witness is "famous" or "infamous", once this information is calculated a total ordering can be calculated on the events.

For more details on how the algorithm works refer to the original paper 


## Example HashGraph Visualizer Output
- Each member in the Hashgraph is determined by a vertical line.
- Each circle represents an event in the Hashgraph.
- The circles that are of the same color are events that belong to the same round.
- Witness events are the double-circled events in the image.
- Witness events (Double Circles) which are decided as famous are cloured/filled with light grey.
- Witness events (Double Circles) which are decided as infamous are coloured/filled with dark grey.
- The number inside the circle gives the order number of that event in the consensus order. No number present implies that the order for that event hasn't yet been determined.

  ![alt text](https://github.com/atharva151101/Hedera_Hashgraph/blob/main/Hashgraph2_full.png)

## Output for a larger graph 
  
  ![alt text](https://github.com/atharva151101/Hedera_Hashgraph/blob/main/Hashgraph1_full.png)
