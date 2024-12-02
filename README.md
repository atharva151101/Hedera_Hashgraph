# Hedera-Hashgraph
Implementation of the Hashgraph Consensus Algorithm along with its visualization.

Based on the paper https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf

## Running the code
 - Install the dependencies from requirements.txt
   ```
   pip install -r requirements.txt
   ```
 - The program can be run by importing the IPython/Jupyter notebook `hedera_hashgraph.ipynb` (recommended) or directly running the python program `hedera_hashgraph.py`.  
 - The program requires the input to be given in the following format
   - The first line should be a single integer containing the number of nodes.
   - All the subsequent lines describe an event. The event is described but providing the following information each separated by a space -
     - The creator of the event i.e the number of the member who created the event
     - The unique id of the event (A unique integer)
     - The id of the parent event i.e. the event id of the member who sent the current event to the creator. (NULL if the parent does not exist)
     - The id of the self parent  i.e. the event id of the last event that was created by the creator of the current event. (NULL if this is the first event by the creator)
     - The timestamp when this event was created.
   - The last line should contain a single word "Done" indicating the end of the input
 - The program would generate the following files -
   - A .txt file containing the consensus order for the events.
   - A .dot file with the dot code for the Hashgraph.
   - A PNG image for the Hashgraph using the above dot file for visualizing the consensus algorithm.
 - Additionally, the program can be used to visualize the intermediate steps too in the consensus algorithm.
  

## Example HashGraph Visualizer Output

  ![alt text](https://github.com/atharva151101/Hedera_Hashgraph/blob/main/Hashgraph2_full.png)


- The first graph shows the bare Hashgraph without any application of the consensus algorithm. The second graph shows the events in Hashgraph divided into separate rounds and the witness events also being decided for each round. The third graph shows the witness events being marked as famous or infamous. The fourth graph shows the complete Hashgraph with the events being marked according to their order number in the consensus order after the consensus algorithm is applied.
- Each member in the Hashgraph is shown by a vertical line.
- Each circle represents an event in the Hashgraph.
- The circles that are of the same color are events that belong to the same round.
- Witness events are the double-circled events in the image.
- Witness events (Double Circles) which are decided as famous are colored/filled with light grey, while Witness events which are decided as infamous are colored/filled with dark grey. Witness events that are not colored/filled are the witnesses whose fame is undecided.
- The number inside the circle gives the order number of that event in the consensus order. No number present implies that the order for that event hasn't yet been determined.



## About Hashgraph
Hashgaph is a distributed ledger used to achieve Byzantine agreement and is considered a 
more efficient alternative to the current blockchain technology. https://hedera.com/ is
a decentralized, proof-of-stake public ledger that utilizes the Hashgraph consensus 
algorithm.

Hashgraph achieves consensus through frequent communication (aka gossip) between all the members. A gossip can entail any real-life practical event like a transaction. The protocol in short can be termed as "gossip about gossip", where the participating members not only gossip about the individual events but the whole Hashgraph itself i.e. the complete history of all the "gossip" or events that a member has created or received from other members.

## Outline of the Consensus Algorithm 
 - Each member of the population maintains a Hashgraph, which contains the history of all the gossip that has happened until now. Every member can have a separate copy of the Hashgraph which differs in the recent history of events, but the algorithm ensures these Hashgraphs are consistent i.e. the ordering of events that is determined as per the consensus algorithm would be the same for all.
 - Alice (one of the members) chooses another member Bob randomly and gossips all the events that Alice knows. This communication event of Alice to Bob is itself marked as a new event by Bob.
 - The consensus algorithm divides all the events into separate rounds. For any given member, the first that the member creates for a given round is termed a "witness" event.
 - There is a virtual voting that occurs between the witness events to determine whether a witness is "famous" or "infamous", once this information is calculated a total ordering can be calculated on the events.

For more details on how the algorithm works refer to the original paper https://www.swirlds.com/downloads/SWIRLDS-TR-2016-01.pdf


## Output for a larger graph 
  
  ![alt text](https://github.com/atharva151101/Hedera_Hashgraph/blob/main/Hashgraph1_full.png)
