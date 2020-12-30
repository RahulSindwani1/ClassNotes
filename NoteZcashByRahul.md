# An Empirical Analysis of Anonymity in Zcash, by George Kappos, Haaroon Yousaf, Mary Maller, and Sarah Meiklejohn  #
## Notes by Rahul ##

### **[Background]** ###  

Zcash is one with the strongest anonymity guarantees, due to its basis in well-regarded cryptographic research. Zcash does not require all transactions to take place within the shielded pool itself: it also supports so-called transparent transactions, which are essentially the same as transactions in Bitcoin in that they reveal the pseudonymous addresses of both the senders and recipients, and the amount being sent. It does require, however, that all newly generated coins pass through the shielded pool before being spent further, thus ensuring that all coins have been shielded at least once as shown in Figure 1.


![alt text](/Images/Capture4.PNG)

**Figure 1 :** A simple diagram illustrating the different types of Zcash transactions. All transaction types are depicted and described with respect to a single input and output, but can be generalized to handle multiple inputs and outputs.


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

#### Participants ####
 
There are four participants in Zcash network.
1. **Founders** took part in the initial creation and release of Zcash,and will receive 20% of all newly generated coins (currently 2.5 ZEC out of the 12.5 ZEC block reward). 
2. **Miners** take part in the maintenance of the ledger, and in doing so receive newly generated coins (10 out of the 12.5 ZEC block reward), as well as any fees from the transactions included in the blocks they mine.
3. **Services** are entities that accept ZEC as some form of payment. These include exchanges like Bitﬁnex, which allow users to trade ﬁat currencies and other cryptocurrencies for ZEC (and vice versa), and platforms like ShapeShift 
4.  **Users** are participants who hold and transact in ZEC at a more individual level.


### **[Paper Contribution]** ### 
The paper provide the first in-depth empirical analysis of anonymity in Zcash, in order to examine these claims and more generally provide a longitudinal study of how Zcash has evolved and who its main participants are. The paper discuss the aspect of Zcash by adapting the analysis that has already been developed for Bitcoin, and ﬁnd that exchanges typically dominate this part of the blockchain. The study performed the analysis using a custom set of Python scripts equipped with PySpark and parsed the block chain on January 21 2018, at which point 258,472 blocks had been mined. Overall, 3,106,643 ZEC had been generated since the genesis block, out of which 2,485,461 ZEC went to the miners and the rest (621,182 ZEC) went to the founders. Across all blocks, there were 2,242,847 transactions. A complete breakdown of the transaction types is in Table 1

![alt text](/Images/Capture5.PNG)

#### T-address clustering ####

**Heuristics 1** If two or more t-addresses are inputs in the same transaction (whether that transaction is transparent,shielded, or mixed), then they are controlled by the same entity.

**Heuristics 2** If one (or more) address is an input taddress in a vJoinSplit transaction and a second address is an output t-address in the same vJoinSplit transaction, then if the size of zOut is 1 (i.e., this is the only transparent output address), the second address belongs to the same user who controls the input addresses.

**Results** Running Heuristic 1 resulted in 560,319 clusters, of which 97,539 contained more than a single address. As can be seen in Table 2, many of the exchanges are associated with some of the biggest clusters, with four out of the top five clusters belonging to popular exchanges.

![alt text](/Images/Capture6.PNG)

**Heuristics 3/ Founder Heuristic** Any z-to-t transaction carrying 250.0001 ZEC in value is done by the founders.

**Heuristic 4/Miner Heuristic**  If a z-to-t transaction has over 100 output taddresses, one of which belongs to a known mining pool, then we label the transaction as a mining withdrawal (associated with that pool), and label all non-pool output t-addresses as belonging to miners. As a result of running this heuristic, the paper tagged 110,918 addresses as belonging to miners, and linked a much more significant portion of the z-to-t transactions as shown in Figure 1.

![alt text](/Images/Capture7.PNG)

**Figure 1 :** The z-to-t transactions associated with miners, founders, and ‘other’, after running some combination of  heuristics. 


### **[Challenges and Differences with Related Works]** ### 
There has been a significant volume of research in providing solutions for existing cryptocurrencies that allow interested users to mix their coins in a way that achieves better anonymity than regular transactions [15, 41, 21, 24, 39, 14, 22, 25]. There has also been a significantvolume of research on de-anonymizing Bitcoin [37, 38,12, 27, 40]. In comparison, this paper implements heuristics but also provides a broader perspective on the entire Zcash ecosystem, as well as a more in-depth analysis of all interactions with (and within) the shielded pool.

### **[Conclusions]** ### 
The study applied both well-known clustering heuristics that have been developed for Bitcoin and attribution heuristics we developed ourselves that take into account Zcash’s shielded pool and its unique cast of characters. As with previous empirical analyses of other cryptocurrencies, our study has shown that most users are not taking advantage of the main privacy feature of Zcash at all. 


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
