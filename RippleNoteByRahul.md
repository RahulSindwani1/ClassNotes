# Listening to Whispers of Ripple: Linking Wallets and Deanonymizing Transactions in the Ripple Network, by Pedro Moreno-Sanchez, Muhammad Bilal Zafar, and Aniket Kate #
## Notes by Rahul ##

### **[Background]** ###  

Ripple is a decentralized I owe you (IOU) transaction network that enables transactions in any currency between arbitrary pairs of agents. Ripple keeps track of IOU credit its users have granted to their business partners or friends, and settles transactions between two connected Ripple wallets by appropriately changing credit values on the connecting paths. Ripple has the potential to bounce into not only big banks but also into smaller ones as an interesting alternative to avoid large fees charged by intermediate banks while performing world-wide transactions.

#### Ripple IOU Network : ####

The Ripple network is a weighted, directed graph G = (V,E). The set V of vertices represents the wallets in the network. The set E of weighted edges represents the IOU credit links between wallets. The credit available on an edge is lower-bounded by 0 and is upper-bounded by ∞ by default, while a more strict upper bound can optionally be adopted by the wallet owner. A new wallet willing to interact with others in the Ripple network, and not yet having any trusted wallet to interact with, needs to receive some IOUs on a credit link. The Ripple network solves this bootstrapping problem by introducing gateways.A gateway isa well-known reputed wallet that several wallets in the system can trust to create and maintain a credit line in a correct manner.

#### Transactions in Ripple Network : ####

Ripple allows two types of transactions: direct XRP payments and path-based settlement transactions. A direct payment involves a transfer of XRP between two wallets which may not have a credit path between them. Path-based settlement transactions transfer any type of credit (ﬁat currencies, cryptocurrencies and user-deﬁned currencies) between  two wallets having a suitable set of credit paths between them.

### **[Paper Contribution]** ### 
The paper visualize the Ripple network we crawled in Figure 3.
This work aims at improving the understanding of the traceability of Ripple ﬂows and using it to explore the privacy breaches. The paper contributed by clustering diﬀerent Ripple wallets belonging to same users which further allows to recognize previously unlinked transactions performed by the known Ripple users and deanonymization of businesses performed over Ripple. The paper presents two novel heuristics to cluster Ripple wallets. 

#### Heuristic 1 : ####

The ﬁrst heuristic presented by the paper is based on a settlement transaction between two wallet owners over their Ripple link to settle their bitcoin exchange. This heuristic enables linking of Bitcoin and Ripple wallets owned by the two involved users.

#### Heuristic 2 : #### 

The second heuristic leverages the transaction patterns performed by a user when deploying the hot-cold wallet security mechanism [1], which limits her risk proﬁle on the Ripple network by enforcing a separation of roles that promotes stronger security. This heuristic allows to link several hot and cold Ripple wallets belonging to the same user.

