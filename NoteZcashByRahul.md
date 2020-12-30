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
There has been a significant volume of research in providing solutions for existing cryptocurrencies that allow interested users to mix their coins in a way that achieves better anonymity than regular transactions [1, 2, 3, 4, 5, 6]. There has also been a significantvolume of research on de-anonymizing Bitcoin [7, 8, 9, 10]. In comparison, this paper implements heuristics but also provides a broader perspective on the entire Zcash ecosystem, as well as a more in-depth analysis of all interactions with (and within) the shielded pool.

### **[Conclusions]** ### 
The study applied both well-known clustering heuristics that have been developed for Bitcoin and attribution heuristics developed in the study that take into account Zcash’s shielded pool and its unique cast of characters. As with previous empirical analyses of other cryptocurrencies, this study has shown that most users are not taking advantage of the main privacy feature of Zcash at all. Furthermore, the participants who do engage with the shielded pool do so in a way that is identifiable, which has the effect of significantly eroding the anonymity of other users by shrinking the overall anonymity set.  The only way for Zcash to truly ensure the size of its anonymity set is to require all transactions to take place within the shielded pool, or otherwise significantly expand the usage of it.


### **[References]** ### 
[1] J. Bonneau, A. Narayanan, A. Miller, J. Clark, J. A. Kroll, and E. W. Felten. Mixcoin: Anonymity for Bitcoin with accountable mixes. In N. Christin and R. Safavi-Naini, editors, FC 2014, volume 8437 of LNCS, pages 486–504, Christ Church, Barbados, Mar. 3–7, 2014. Springer, Heidelberg, Germany.

[2] L. Valenta and B. Rowan. Blindcoin: Blinded, accountable mixes for Bitcoin. In M. Brenner, N. Christin, B. Johnson, and K. Rohloff, editors, FC 2015 Workshops, volume 8976 of LNCS, pages 112–126, San Juan, Puerto Rico, Jan. 30, 2015. Springer, Heidelberg, Germany.

[3] E. Heilman, L. Alshenibr, F. Baldimtsi, A. Scafuro, and S. Goldberg. TumbleBit: an untrusted Bitcoin-compatible anonymous payment hub. In Proceedings of NDSS 2017, 2017.

[4] G. Maxwell. CoinJoin: Bitcoin privacy for the real world.bitcointalk.org/index.php?topic=279249, Aug. 2013.

[5] T. Ruffing, P. Moreno-Sanchez, and A. Kate. CoinShuffle: Practical decentralized coin mixing for Bitcoin. In M. Kutylowski and J. Vaidya, editors, ESORICS 2014, Part II, volume 8713 of LNCS, pages 345–364, Wroclaw, Poland, Sept. 7–11, 2014. Springer, Heidelberg, Germany. T. Ruffing, P. Moreno-Sanchez, and A. Kate. CoinShuffle: Practical decentralized coin mixing for Bitcoin. In M. Kutylowski and J. Vaidya, editors, ESORICS 2014, Part II, volume 8713 of LNCS, pages 345–364, Wroclaw, Poland, Sept. 7–11, 2014. Springer, Heidelberg, Germany.

[6] G. Bissias, A. P. Ozisik, B. N. Levine, and M. Liberatore. Sybilresistant mixing for Bitcoin. In Proceedings of the 13th Workshop on Privacy in the Electronic Society (WEIS), pages 149–158, 2014.

[7] F. Reid and M. Harrigan. An analysis of anonymity in the Bitcoin system. In Security and privacy in social networks, pages 197–223. Springer, 2013.

[8] D. Ron and A. Shamir. Quantitative analysis of the full Bitcoin transaction graph. In A.-R. Sadeghi, editor, FC 2013, volume 7859 of LNCS, pages 6–24, Okinawa, Japan, Apr. 1–5, 2013. Springer, Heidelberg, Germany.

[9] E. Androulaki, G. Karame, M. Roeschlin, T. Scherer, and S. Capkun. Evaluating user privacy in Bitcoin. In A.-R. Sadeghi, editor, FC 2013, volume 7859 of LNCS, pages 34–51, Okinawa, Japan, Apr. 1–5, 2013. Springer, Heidelberg, Germany.

[10] S. Meiklejohn, M. Pomarole, G. Jordan, K. Levchenko, D. McCoy, G. M. Voelker, and S. Savage. A fistful of bitcoins: characterizing payments among men with no names. In Proceedings of the 2013 Internet Measurement Conference (IMC), pages 127–140, 2013.
