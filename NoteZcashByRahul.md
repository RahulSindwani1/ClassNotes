# An Empirical Analysis of Anonymity in Zcash, by George Kappos, Haaroon Yousaf, Mary Maller, and Sarah Meiklejohn  #
## Notes by Rahul ##

### **[Background]** ###  

Zcash is one with the strongest anonymity guarantees, due to its basis in well-regarded cryptographic research. 

#### How Zcash Works : ####

Zcash (ZEC) is an alternative cryptocurrency developed asa(code) fork of Bitcoin that aims to break the link between senders and recipients in a transaction. In Bitcoin, recipients receive funds into addresses(referred to as the vOut in a transaction),and when they spend them they do so from these addresses (referred to as the vIn in a transaction). Any transaction which interacts with the so-called shielded pool in Zcash does so through the inclusion of a vJoinSplit, which speciﬁes where the coins are coming from and where they are going. To receive funds, users can provide either a transparent address(t-address) or a shielded address (z-address). Coins that are held in z-addresses are said to be in the shielded pool.

To specify where the funds are going, a vJoinSplit contains
1. a list of output t-addresses with funds assigned to them (called zOut)
2. two shielded outputs, and 
3. an encrypted memo ﬁeld. 

To specify where the funds are coming from, a vJoinSplit also contains 
1. a list of input t-addresses (called zIn), 
2. two double-spending tokens, and 
3. a zeroknowledge proof.

![alt text](/Images/Capture1.PNG)

**Figure 1 :** . An illustrative example of the Ripple network. For readability, every Ripple wallet is represented by a name with superscript ∗ instead of a hashed public key used in practice. Values in {} represent the XRP currency balance, and edges represent credit links between pairs of connected nodes. The edge weights show IOU credit values on the edges. The edges weights are lowerbounded by zero and upper-bounded by ∞. For readability, we show only one currency on the edges. 

#### Transactions in Ripple Network : ####

Ripple allows two types of transactions: direct XRP payments and path-based settlement transactions. A direct payment involves a transfer of XRP between two wallets which may not have a credit path between them. Path-based settlement transactions transfer any type of credit (ﬁat currencies, cryptocurrencies and user-deﬁned currencies) between  two wallets having a suitable set of credit paths between them.

### **[Paper Contribution]** ### 
The paper visualize the Ripple network in Figure 2. In total there are 470 communities composed only of two or more nodes. The communities composed of bigger number of nodes include the gateways wallets. Finally, communities with 2 to 7 nodes are the most frequent in the Ripple network. This community structure indicates the Ripple network is developing.

![alt text](/Images/Capture2.PNG)

**Figure 2 :**  A visualization of the Ripple network as of December 2015. We show only nodes with at least one link in the network. Different colors represent the communities (as computed by Gephi) in the network.


This work aims at improving the understanding of the traceability of Ripple ﬂows and using it to explore the privacy breaches. The paper contributed by clustering diﬀerent Ripple wallets belonging to same users which further allows to recognize previously unlinked transactions performed by the known Ripple users and deanonymization of businesses performed over Ripple. The paper presents two novel heuristics to cluster Ripple wallets. 

#### Heuristic 1 : ####

The ﬁrst heuristic presented by the paper is based on a settlement transaction between two wallet owners over their Ripple link to settle their bitcoin exchange. This heuristic enables linking of Bitcoin and Ripple wallets owned by the two involved users. The paper use the publicly available information regarding deposit and withdrawal transactions at the gateways to link together Ripple and Bitcoin wallets that belong to the same user. When deploying the heuristic in practice, the paper do not take into account the
change wallet and Bitcoin mixing transactions. The paper avoid them by only considering Bitcoin transactions with at most 2 output wallets (the receiving wallet and the change wallet). In the results the paper observe 2 Bitcoin wallets that are linked to 15 and 49 Ripple wallets each, while the rest are linked to at most 5 Ripple wallets. Therefore,
the paper consider them as outliers and discard them.

#### Heuristic 2 : #### 

The second heuristic leverages the transaction patterns performed by a user when deploying the hot-cold wallet security mechanism [1], which limits her risk proﬁle on the Ripple network by enforcing a separation of roles that promotes stronger security. This heuristic allows to link several hot and cold Ripple wallets belonging to the same user. Ripple defines the hot-cold wallet security mechanism to issue IOUs of any currency. The cold wallet is publicly linked to a certain user. However, actual issuing of the IOUs in a credit link extended to the cold wallet is performed by the hot wallet as follows. First, the hot wallet creates a credit link with the cold wallet. Then, when the owner of the cold wallet must extend credit to a user, she uses the hot wallet to extend that credit, using for this settlement transaction the existing path (hot wallet) ← (cold
wallet) → (user wallet). The clusters acheived by heuristics are shown in Figure 3.

![alt text](/Images/Capture3.PNG)

**Figure 3 :**  Visualization of the deanonymization process over our clustered graph. The sizes of the nodes correspond with the number of transactions involving the nodes. Nodes with the same color belong to the same cluster. Gray nodes depict wallets not deanonymized by our heuristics. Links are colored with the color of the sending wallet

The paper further studied the privacy implications of the heuristics by applying the deanonymization process over the transactions for whichat least a wallet has been clustered by the heuristics. The paper deanonymized 85,962 XRP payments and 649,640 settlement transactions, which jointly represent the 78.7% of the total transactions considered in the de-anonymization process. These results follow the fact that the probability that a Ripple wallet gets deanonymized is bigger when the wallet is clustered with our heuristics

### **[Challenges and Differences with Related Works]** ### 

The most prevalent approach to improve anonymity for Bitcoin users is the idea of hiding in a group by Bitcoin mixing: the users in the group exchange their coins with each other to hide the relations between users and coins from an external observer. Several Bitcoin mixing approaches have been proposed
[1, 2, 3, 4, 5, 6, 7, 8, 9]. Several research works [10, 11] propose mechanisms to cluster accounts from different social networks that are owned by the same person. There are several approaches to enhance social networks with privacy [12, 13, 14]. All of these approaches modify the network connectivity so that the
privacy of the link is preserved and the loss of system reliability is bounded.  Nevertheless, none of these works show how privacy of users can be thwarted. This work characterizes the current state of the Ripple network along with its complete set of transactions. Additionally, it shed light on the gap–due to certain patterns of use and interaction between parties in the network—between the (supposedly) provided privacy available in the Ripple network and the actual privacy achieved by the current Ripple users and, most importantly, their transactions.

### **[Conclusions]** ### 

The heuristics allow to cluster wallets belonging to the same user, not only from the Ripple network but also from several (publicly verifiable) blockchain-based cryptocurrency systems such as Bitcoin. More interestingly, this clustering has enabled the deanonymization of more than 78% of the clustered transactions, which in turn has allowed us to reconstruct the complete amount of trade of the most widely deployed gateways in the Ripple network. Finally, the analysis characterizes the privacy challenges faced by the emerging transaction networks, paves the way towards further deanonymization by forensic techniques and motivates the imperative need for better privacy preserving transactions mechanisms for Ripple

### **[References]** ### 
[1] Bitcoin Wiki: Mixing Services. https://en.bitcoin.it/wiki/Category:Mixing_Services.

[2] CoinJoin: Bitcoin Privacy for the Real World. Post on Bitcoin Forum, Aug. 2013. https://bitcointalk.org/index.php?topic=279249.

[3] Barber, S., Boyen, X., Shi, E., and Uzun, E. 16th International Conference Financial Cryptography and Data Security. 2012, ch. Bitter to Better — How to Make Bitcoin a Better Currency, pp. 399–414.

[4] Bissias, G., Ozisik, A. P., Levine, B. N., and Liberatore, M. Sybil-resistant mixing for bitcoin. In Proceedings of the 13th Workshop on Privacy in the Electronic Society,
WPES ’14, pp. 149–158.

[5] Bonneau, J., Narayanan, A., Miller, A., Clark, J., Kroll, J. A., and Felten, E. W. Mixcoin: Anonymity for Bitcoin with accountable mixes. In Proc. of the 17th International Conference on Financial Cryptography and Data Security, FC’14, Springer.

[6] Heilman, E., Baldimtsi, F., and Goldberg, S. Blindly signed contracts: Anonymous on-blockchain and offblockchain bitcoin transactions. IACR Cryptology ePrint Archive 2016 (2016), 56.

[7] Ruffing, T., Moreno-Sanchez, P., and Kate, A. CoinShuffle: Practical Decentralized Coin Mixing for Bitcoin. Computer Security - ESORICS 2014: 19th European Symposium on Research in Computer Security. pp. 345–364.

[8] Valenta, L., and Rowan, B. Blindcoin: Blinded, Accountable Mixes for Bitcoin. FC 2015 International BITCOIN Workshops Financial Cryptography and Data Security.
pp. 112–126.

[9] ] Ziegeldorf, J. H., Grossmann, F., Henze, M., Inden, N., and Wehrle, K. Coinparty: Secure multi-party mixing of bitcoins. In Proceedings of the 5th ACM Conference on Data and Application Security and Privacy (2015), pp. 75–86.

[10] Korayem, M., and Crandall, D. J. De-anonymizing users across heterogeneous social computing platforms. In ICWSM (2013), E. Kiciman, N. B. Ellison, B. Hogan, P. Resnick,
and I. Soboroff, Eds., The AAAI Press.

[11] Narayanan, A., and Shmatikov, V. De-anonymizing social networks. In Proceedings of the 2009 30th IEEE Symposium on Security and Privacy, pp. 173–187.

[12] Hay, M., Miklau, G., Jensen, D., Towsley, D., and Weis, P. Resisting Structural Re-identification in Anonymized Social Networks. Proc. VLDB Endow. 1, 1 (2008), 102–114.

[13] Mittal, P., Papamanthou, C., and Song, D. X. Preserving Link Privacy in Social Network Based Systems. In Network and Distributed System Security 2013.

[14] Sala, A., Zhao, X., Wilson, C., Zheng, H., and Zhao, B. Y. Sharing graphs using differentially private graph models. Proceedings of the 2011 ACM SIGCOMM Conference on Internet Measurement Conference, pp. 81–98.
