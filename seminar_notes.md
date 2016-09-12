# Monday Morning 1

Personal presentations and logistics overview.

# Monday Morning 2

## ICN Overview [Börje]

(no slide numbers)

* On-path and namespace hijackers are still part of the threat model.

    * Attackers can provide bogus data (signed or not).

    * There’s no guarantee that a consumer actually gets content.

* We have a lot of experience from object security that we can build on.

* ICN does not necessitate in-network caching.

    * Caching is an optimization, not a requirement.

    * Security (especially privacy) problems are different with and without caching.

* Q: what is the difference between the two network graphs?

    * Thickness indicates data volume.

    * Maybe use Bitcoin to incentivize p2p traffic?

* IP didn’t win, the others just couldn’t keep up.

    * IPv4 was more or less free, others were not.

    * Early and rapid deployment and earning wins.

* Is NetInf still active?

    * Not much -- switching to NDN/CCN.

    * Many FIA projects have stagnated.

* Threat model is still unclear. We need strict definitions. Current attackers:

    * Go after key infrastructure, tap cables, inject traffic, etc.

    * Attackers will adapt to ICN.

* Disagree with "All private information is gone after first hop." 

    * Not necessarily true. What if the anonymity set is small?

* Maybe we should focus on passive adversaries.

    * This is the most elementary one.

    * Passive attacks are invisible, e.g., by tapping wire.

* Caching (router) infrastructure is not authenticated in NDN (?).

* ICN assumes that everyone gets the same object. Not necessarily true with access control with per-person key encryption. 

    * Data is not re-encrypted -- only the keys are re-encrypted.

* Cannot address consumer in ICNs.

* Future security should be controllable, i.e., the publisher should has control over who can access data and the system (network) should enforce that policy.

    * C: Do you mean routers? Routers probably shouldn’t be doing any enforcement.

* Audi didn’t pay enough to handle the traffic overload.

## Threat Models [Ersin]

* [4] IPSec does provide some integrity protection

* [4] There are solutions to the security problems, but they are not built into the network.

    * IP has been patched at different layers (and that causes patches for patches).

* [6] We need to be clear about what we mean by infrastructure.

    * Technology has an ecosystem, and the infrastructure is that ecosystem.

* [6] Does network enforcement break end-to-end enforcement.

    * What is end-to-end in ICN?

    * C: Since the network requires memory, the end-to-end argument no longer applies.

    * If you turn "packet" into “object” then you can still talk about end-to-end.

    * End-to-end applies in a layered communication system.

    * Is the goal to put stuff into the network so that apps do not do them?

    * The point of end-to-end is that data is authenticated from "source" to “destination.” It doesn’t matter what’s in between.

        * We don’t necessarily have to throw out end-to-end.

    * Functionality like PEPs, CDNs, etc. mean that the end-to-end don’t really apply anymore. The question should be about how much be put in the network.

* [6] If the network provides more security services then app development may become easier and less error-prone.

* [7] What’s the definition of confidentiality?

    * It used to mean that third parties can’t learn anything.

    * … but traffic analysis reveals a lot. 

    * There’s a difference between content and metadata confidentiality.

        * C: Metadata confidentiality is more about privacy.

    * Should confidentiality really be in the network?

* [9] Context is important when determining the threat model.

    * Netflix model is different from the IoT publish/subscribe model.

* [9] Threat modeling requires defining the assets before anything else.

* [9] Context-specific threat modeling approach was omitted from this slide.

    * Could be another dimension for the existing approaches (e..g, asset-, system-, and attacker-centric).

* [10] C: We should stop talking about trust -- it’s mostly a solved problem.

    * Do not agree that it’s a "solved problem" for an architecture. 

    * How to do "trust" in ICN is about the mechanics, not about the ecosystem.

* [10] It’s not about authentication, it’s about policy. How do we know which keys that I trust?

    * The "Who" is the client.

* [10] Is it the network’s job to control access?

    * GTS: No.

* How do we carve up the confidentiality, access control, and privacy services across the stack?

* [13] There is no key management in the (Internet) network. It’s done at a higher layer.

* [14] We can discuss the entire field of communication security, but we should be focusing on things that are specific to ICN.

    * Signatures in (some) ICN architectures are not opaque to the network -- they can be used.

* [14] Name privacy is not possible in ICN since a routable prefix reveals a great deal of information (more than an IP address and port)?

* [14] Not all applications need all types of privacy. How does ICN deal with this?

* [14] We want a system that offers privacy by default. 

* [14] There is a (bad) tendency to try and application new and fancy crypto schemes in ICN.

# Monday Afternoon 1

## New Crypto Tools [Chris]

* ICN in stack (native approach vs. overlay approach)

* Security services for ICN

* [5] What’s the difference between anonymity (hide the source of the packet) and privacy (content privacy)?

* [5] What’s the difference between confidentiality and privacy?

* Hash-based signatures : Merkle Tree, XMSS Tree, Stateless Hash-Based Signature (e.g. SPINCS)

* [16] Is Stateless or state-based hash-based signature more efficient?

* [16] Ersin: There are quantum computing secure encryption and signature schemes.

* [16] Post-quantum primitive for future architecture

* Privacy: encrypted DPI

* [19] Why do we want to do encrypted DPI? e.g. http header is already in the name in ICN.

* [20] Someone can distinguish part the ciphertext with encrypted DPI? Would it be a violation to privacy? 

* Privacy - key exchange (Password AKE, non-interactive key exchange (NIKE))

* [28] identity means prefix here?

* KE Recap: NIKE creates group "sessions" without any key exchanges

* [30] How to generalize one-to-one to group sessions?

* [30] NIKE is a scheme that we can look at and see if it can improve ICN

* [30] What is the general use case of ICN?

* [30]  Multicast security is existing, so as multi-user security schemes for NDN  

* Privacy: PIR (skipped due to time limit)

* Forward-secure public key encryption (e.g. Binary tree encryption)

* Randomized signatures

* [47] How to solve the problem of un-encrypted names? What about obfuscation?

* [47] Do we trust the routers? How does the router make the fundamental routing forward decision (if we follow our definition of privacy)? 

## Whither ICN Privacy [Gene]

* There is a difference between a publisher and creator.

    * A book author is a creator but a publisher is the one that makes the content available.

    * When are they same and when are they different?

    * The outermost "identity" is what’s revealed.

* Is meta info included in the properties of content?

    * No, properties refer to the "upper layer" properties.

    * Meta-info includes name, signature, key locator, etc.

    * List is not complete.

* Some ICNs allow requests to describe attributes instead of specific versions.

    * Maybe attributes should be included in the list of content properties.

* How long does the "name to content" binding last? Do we assume that the binding lasts forever?

    * NDN has a loose definition of what immutable means.

    * NDN allows different names to be returned to enable fresh content discovery.

    * Publishers have to obey the immutability rules.

* An active attacker that is manipulating links could violate privacy.

## Transport Privacy [Christian]

* Taking privacy into account, what is the boundary what you can ask the network to do for you and what it cannot?

* What is the definition of metadata?

    * Two types: (1) metadata that is provided by parties to the conversation/system, and (2) metadata that we can infer from observing. 

    * In case (2), traffic analysis can be used to reveal plaintext content (if it’s encrypted).

        * Mixnet data can generally be decrypted given long enough conversations.

    * They’re all properties.

* What do we expect network services to provide in conjunction with privacy-protection mechanisms?

    * Broadcasting packets encrypted with a OTP is great for privacy, but awful for the network. 

    * What’s the balance?

## Network Coding & Privacy in ICN [Cedric]

* Content privacy difficult in current ICN

* Cached content exposes the content 

* Content can be provided by 3rd party without control

* Potential solution: 

    * to use network coding in the network

    * To use coded caching in the caches

* Network coding in the network:

    * Interest request for network coded chunks

    * On-path observers see opaque packets

    * Would need to see all paths to reconstruct the packet, thereby creating on-the-wire privacy

    * Expands on the 2012 "Network Coding meets ICN" paper

* Coded caching:

    * Caches do not cache the whole packet, but only a subset; content server still hold a fraction of the content

    * Requests for content as served by the cache and by the server

    * Requests from the cache are the partial answers that exist in the cache; requests from the server are encoding across multiple requests from multiple users, depending on the content of their cache

    * Therefore: on the wire privacy again (need the cache content to decode); and the server can transmit the missing bits only to authorized users (control over distribution, even using caches)

    * Furthermore: there is literature which shows a bandwidth saving in the traffic from the server, and a higher hit rate from the caches (see paper from Maddah-Ali, Niesen, etc)

* In summer: two solutions to use coding as a mechanism to BOTH provide privacy AND reduce bandwidth consumption/network response time.

* Question: is this worth investigating? Is the answer positive?

    * Hope so.

## Anonymity in ICN [Mauro]

* Exactly what routing information is made available to routing-aware adversaries, and how useful is it?

* By observing past traffic, can I infer where interests will be routed in the network?

    * May not be able in ICN.

    * Or does ICN give you a better guarantees about the router path?

    * What capabilities does the adversary possess?

* Timestamping and strategically placed observes in IP can use routes to be predicted.

* There has been geolocation work in IP, but it’s not as easy in IP.

# Monday Afternoon 2

Breakout meetings.

## Transport privacy [Christian] 

[These are my personal reflections from the discussion, *not* formal notes.]

* Broadcast for receivers  works fine for privacy. Can we do broadcast for publishers? Everyone needs to publish at the same rate.

* A group of entities can communicate in a way that noone outside the group can tell who is communicate with whom within the group.

* Use of broadcast of all messages to all group participants combined with ABR could provide this functionality.

* An issue is how information can be exchanged between groups without revealing privacy. Can scoping be helpful here?

* We concluded that for our very limited use case this could be done. But there are serious scaling and efficiency issues. On the other hand 20 years ago nobody would have believed that you could have a Google search service where you get search responses for each character you type. Even if someone came up with the idea it would have been killed for being too wasteful of network resources.

* We can implement all of this on top of email using all the spam traffic as background traffic.

## Routing on encrypted names [Chris]

* (Notes in slides)

## Non-privacy security issues in ICN [Craig]

* Availability is the security goal and Denial of Service is the opposite of it.

* Consistency: I got the version that I asked. Why is it important? (Postponed to later)

* Why not focus on network functions? Relation between identity and network location. Is problem specific to ICN? There are examples where this issue is slightly pronounced. However, this problem bears similarities with existing traditional networks.

* We are not concerned with:

    * Privacy

    * Application functionality (routing is an application)

    * Application deciding which name to ask for. No network hints on the name.

    * Key management

* Identity? Consumer does not have an identity. Content producer (such as publishers) have identities, that are pre-fixed. More generally, whatever affects routing information should have identities.

* Content producer vs publisher: subscribers vs publisher. Subscriber is a consumer, yet it produces information in the routing structure. Push vs pull model. Anybody that can change routing information should require some form of authorization.

* Should we treat all publishers the same? Some publishers are more "powerful" than others. We need to authenticate some publishers? Routing is a fundamental application, so security is important there. @google -> packet has to go to google. How can we ensure that?

* Gene: Let us step away from routing protocols..

* A router takes a packet, and can do: forward/cache/drop/duplicate. IP router receives one type of traffic. What kind of security processing has to take place on two kinds of packets in ICN?  

* The router will not verify the authenticity of requests. This will cause serious performance degradation in the network (bad signature DoS, Swamped PIT/DoS). Serious disagreement among audience about the need for authentication of notifications. One way notifications might add a FIB, but should not change the state of the network (this is a bug in the system). One way to do this is reverse path forwarding -> assigning names to addresses and bind public keys to those names. People seem to be thinking about different architectures. Multicast requests can cause serious problems if they are not authenticated.

    * We should probably authenticate response since they affect the cache.

    * The router should be capable to do integrity checks on objects

        * The router should be capable to perform authenticity checks. How? It can accept instructions from outside and be mechanical about it (e.g., the public key could be embedded in the message). Disagreement about this in the group. The public key should not be put automatically in the cache. Requests must include the public key. If so, there is no problem.

    * The router does not need an identity

* Gene: we should distinguish between ICN that do push and ICNs that do pull.                	

* How can we authenticate and verify the integrity of routing information given by the routing applications? Why is it different in ICN vs traditional IP networks? There is no conceptual difference. There is a difference between structure vs unstructured namespace.

* Summary:.

    * 1) We discussed things to exclude

    * 2) We decided who should have an identity in the network

    * 3) We discussed what a router should/could process. Router does not need identity. Should perform authenticity/integrity checks.

    * 4) No consensus on whether the router should authenticate requests.

    * 5) Need to authenticate and verify routing information given by routing applications. Problem not fundamentally different in ICN from traditional IP networks.

* * *


# Tuesday Morning 1

## Non-privacy security issues in ICN [Craig]

* Do routers have identities? They may or they may not. At a minimum they may not need identities.

    * Only for routing (control), not for the data plane.

* Does authentication apply to interests that are pushed?

    * Do notifications (with data) need to be authenticated? Probably.

* Routers should not be doing key resolution and management in real-time.

* CCNx specs do not mandate interest signature verification. Producers make the decision to verify signatures if they expect them.

* There is a difference between intended authenticated notifications and re-using requests as notifications and deciding how to handle signatures or authentication checks.

    * What kind of application would do that? Notifications should be done on a distinguished "channel."

    * This is hard to avoid with only requests and responses. Maybe we need a distinguished push or notification message.

* Routers should never authenticate interests en route to the producer else fall to bad signature DoS or PIT flooding.

## Transport privacy [Christian] 

* Are messages appended in the summing process?

    * Vector of participant responses are combined and given the the receiver.

    * Results could be provided in order or permuted.

* Trying to achieve privacy by mixing? What is the adversary?

    * Not protecting against the mixer, but against something else.

    * The "summer" should not learn who is communicating with who.

    * Think of it as a broadcast channel.

* We don’t trust the receivers? How?

    * If a subset are communicating then they cannot trust anyone else, e.g., others can’t infer anything about the communication. 

    * Whoever has the key can be trusted. Others cannot. (Communicating parties share a key.)

    * Conclusion: maybe retract this statement.

* What about collusions between receivers and the summer?

* Are you assuming that everybody trusts everyone else in the same group? Do they share the same key?

* This seems to compete with existing systems like TOR. What’s the difference?

    * Tries to go to the other extreme about how much the network can help you.

* Perfectly reasonable for transport, but not for the network.

    * This is a type of overlay.

* All three clusters store all three types of data, but data does not be duplicated.

    * Does data need to exist everywhere? Is this sufficient or just necessary?

    * Queries with chaffing can be sent everywhere, but not every server can provide a response.

* Consumers need to know where blocks are stored to direct their queries to the right servers.

* What about the Popcorn paper? And ORAM solutions?

    * [http://www.cs.utexas.edu/~trinabh/papers/popcorn-PIR-nsdi16.pdf](http://www.cs.utexas.edu/~trinabh/papers/popcorn-PIR-nsdi16.pdf) 

    * Popcorn ensures that all videos have the same length so side channels (size leakage) is minimized.

    * This solution tries to solve that at the block level.

* Have you considered CPIR?

    * Better bandwidth. Not much else would change. 

    * IPIR solution was easy to implement, but it requires more bandwidth and non-colluding servers.

## Routing on encrypted names [Chris]

* Assumptions

    * No discovery service for names

    * Content requests based on IDs (hashes)

    * Consumers know PKs of producers

    * Names: routable prefix, app-specific suffix + more

    * Jan: these are some strong assumptions (eg., knowing producer PK)

* Terms

    * Name privacy: routable prefixes reveal no more than IP address and port, app-specific suffix reveals nothing about content

    * Assume: revealing content id is not a problem

    * Clarification: app-specific suffix as seen on the network

* Requests with Content ID

    * Requests with locator and a content ID

    * Discussion about names & locators

* Name encryption

* Response encryption

* Outcome

    * Need a way to discover routable prefix

        * Upper layer service

    * Access control for response

    * Locator and content id are obtained via some other means

    * Antonio: isn’t that equivalent to (efficient) HTTPS?

# Tuesday Morning 2

## Agenda Re-Bashing

## Revisiting "Securing the data, not the pipe" [Marc]

* Q: Can you explain why object security gives us confidentiality?

    * Hybrid encryption (encrypting data with symmetric key, wrapping key with public key for consumer) means that only authorized parties can get it.

        * Requires an online relationship? No.

    * ABE schemes don’t require an online key-fetch process, but they must get the private keys somehow.

* Q: Does group-key encryption not allow a publisher to publish to a group that is independent managed?

    * That’s not how it’s done currently -- most existing solutions have publishers publishing and managing the group.

    * NDN-NBAC separates these roles.

* Do we need forward secrecy?

## ABE [Ashish]

* Are the distributed authorities responsible for independent attribute sets or are they part of the same attribute set?

* Questions about the size of attribute trees for experiments.

    * Less than a dozen leaf nodes in the policy tree.

## Forward Secrecy in ICN? [Chris]

* (N/A)

# Tuesday Afternoon 1

## Quantum Computing and Cryptography [Ersin]

* Quantum communication is not quantum cryptography.

* Only up to 3 qubits right now.

    * Can currently only factor the number 15.

* Pairing based schemes, based on ECs, are also broken. (Missing from slides.)

* The security of lattice-based and other related PQ schemes is questionable. The only one that’s guaranteed are hash-based cryptography.

    * All hash-based schemes require some bootstrapping.

    * A session lets us bootstrap things.

* What part of PQ-PKC affect ICN?

* RSA is nice because it’s easy to understand. PQ schemes are much more complex. Probability of implementation errors is much higher.

    * RSA implementations are still incorrect (?)

* Existing PKC schemes can use better key rotation.

    * Maybe properties of PQ schemes means they cannot be swapped with existing schemes.

* Maybe we don’t want to go into PQ yet. Don’t use data that will have a long lifetime.

    * The architecture needs to support algorithm agility.

* Current CCN architecture encoding supports hash agility.

    * Hash TLVs specify their type and length.

## Trust [Gene]

* Outcome from yesterday’s working group: network layer elements (routers) should not be concerned with trust.

* Is trust binary or contextual?

    * Binary at the network layer (i.e., a router is involved or not).

    * Network layer = data plane.

* ICN allows for better business models where parties pay for publishing or requesting data, since the network does more as a service.

    * Not done in IP.

    * Maybe there’s a proxy between the consumer and backbone and trust is transitive.

* Can you envision a trust relationship between a consumer and a long-haul backbone?

    * Maybe -- not a direct relationship, but the consumers can have "credential relationships" (through some external service) with the backbone.

    * BGPSEC does that, but BGP is not a customer.

* Can you (ISP) attest (verify) routers?

    * So that means routers have identities and consumers know those identities?

    * Is this a control or data plane? 

* Minimizing trust in the data plane is a good thing.

* DNS provides verifiable key identification a la DANE.

* If the application puts a certificate hash in the name and that’s used for routing, is that considered application-layer or network-layer trust?

    * If the router is given knowledge of the public key, fine, but what do you expect the router to do?

    * Routers will not do certificate revocation, but they might do verification.

    * Interest-Key-Binding rule allows application-layer trust to map to the network.

        * Any less than this trust is nothing.

* Why is certificate revocation insanity?

    * The router’s job is to route not to fetch packets to do that job. That’s way too much.

    * Benefits? Maybe it saves the applications from doing this certificate retrieval step?

        * If routers do this, they must understand all of the application-specific trust models.

* Offloading certificate verification can be a service. The implications on the architecture (below the service) are much more severe.

* Network-layer trust is done to prevent content poisoning.

    * We don’t want routers to cache *and serve* invalid content.

## P2P and ICN [Marc]

* Is this bittorrent over CCN?

    * It ends up being that way.

* Why is this necessary when we have caches everywhere?

    * How does a consumer know the other consumer/seeder prefixes? Or what consumers are in possession of which chunks?

* Does this require updates to the routing protocol?

    * There are no routing updates.

* This isn’t a publish subscribe mechanism, but there is some influence notion of pub-sub mechanics.

    * Since seeders advertise (publisher) their prefixes for content.

* Seeders could be network caches.

* Does this deviate from finding stuff in CCN/NDN?

    * What is the traditional way? 

    * Nothing addresses the problem of how to advertise content prefixes without affecting the routing table.

* This is an application-layer custodian network on top of ICN, right?

    * Yes.

* Why not just put this on top of IP?

    * That’s possible. But you’d be using CCN constructions on an overlay.

* How does this relate to the NDN construction of the LINK? Isn’t this similar?

    * LINKs in NDN are forwarding hints. They require discovery.

* Are you replacing NDNS?

    * LINKs (here) are locators, they are not names, of endpoints.

    * Endpoints themselves indicate their locator. Endpoints query the network for their locator.

* Anyone can update the tracker so long as they have the data hash.

    * Details about authentication and relationships between publishers, trackers, and peers are omitted.

* This seems more complex than one would expect for implementing bittorrent over ICN.

    * Is it just as hard as in ICN? What are the advantages?

    * We need a way to distribute locators.

        * That brings in a mobility problem.

* How does this relate to security?

    * Goal: enable hash-based content verification from arbitrary seeders located under different prefixes.

## Crypto Tools [Chris]

* (N/A)

# Tuesday Afternoon 2

## Trust and Identity [Jan]

* Application should be able to specify policy and the "middleware" should enforce it, right?

* What do we expect the router/network to be doing with respect to trust?

* Applications specify schemas -- is that a common denominator for all applications?

    * No, one can easily come up with other ones.

    * Network layer "trust enforcement" should not prohibit or prevent other application-layer trust models.

* Is there a difference between getting a discrete piece of named data vs a stream of named data?

    * No real technical difference -- streams can be authenticated as a set.

* Is routing security out of scope? 

* Is it different than BGP security?

    * Not really. The trust model will be the same. Only the number of prefixes will increase (substantially).

    * In IP, addresses are not identities. In ICN, locators are associated with identities. Maybe that’s the distinction.

* Incentives, stakeholders, and responsibility are all related.

* Current ISP model is that users want the ISP (or groups of independent ISPs) to move packets from A to B and for all packets from other users (not just B) to be sent to A.

    * The ICN model provides two services:

        * Name in and content out (consume)

        * Content publication (producer)

    * These could be paid for as separate services.

    * Could also have an additional storage service.

    * It’s more clear what and consumers and producers are paying for in ICN.

* Trust is about the publisher making assertions about the validity of content so that consumers can verify said content. We need a mechanism to build this network. 

* Schemas are policies that network should abide by?

* Are arbitrary trust models (e.g., are the last 5 bits of the content has zero?) enforceable by content?

* How many core authentication mechanisms are we willing to put into the "network"?

* Routers (network elements) should not be doing any certificate resolution.

* How are names registered in this model?

* How can names possibly be location agnostic?

* There must be some globally accountable namespace manager. Not everyone should be advertising DOI namespaces. It won’t scale.

* Namespace advertising under different namespaces or in different networks must be authenticated.

* How are DNSSEC records modified?

    * Not a real-time activity. It’s "disgusting and terrifying." There are sections in the DNS where this cannot happen.

* Do we not really know how ICN deployment would work in the real world?

    * The consequences of decisions are not resolved.

* Will trust only be hierarchical?

    * It’s the first thing that comes to mind.

    * What about PGP and web-of-trust?

        * Jan experimented with this -- see ICN 2014.

* Consensus:

    * "Network": end systems are supersets of routers in terms of functionality.

        * Routers: only single signature verification or hash verification.

        * End systems: everything else.

    * No answer on the presence of the "namespace authority manager" or “structure.”

* Suspicious about the existence of a global namespace.

* How do NATs work in a non-global namespace?

    * Just do arbitrary conversion from one name to another.

    * Name better not be part of the hash. 

* * *


# Wednesday Morning 1

## Locators [Marc]

* Group consensus: use locators and defer application name redirection/binding to some other entity.

* Should anyone be allowed to inject names into a router?

    * It can be done now, but that’s not good.

* Two extremes:

    * Application-defined network names require routing protocol support.

    * A service that maps application names to locators does not induce a global name.

        * Why does the routing protocol have to be distributed? Why can’t it be centralized?

* Maybe we should accept the fact that there is a service that uses application names. The architecture then reduces to IP.

    * Maybe that’s the revelation..

* The only differentiation with respect to IP is that the application can decide names.

    * DNS scales because applications cannot choose their names. 

* How can we cope and scale with application-chosen names?

* How do we stitch together and compose namespaces?

* Routing in CCN/NDN is done on a name, but matching is done on a predicate (e.g., with restrictions).

* If you had a lookup service then routers don’t need attributes and LINKs, etc.

* We can do hop-by-hop forwarding with routing information in ICN.

* How do we scale?

    * Limit application freedom in choosing names, or…?

* From IPv6: "naming without routing is a path to hell."

* Can we have name-independent routing or do we settle with name-dependent routing?

## ICN and IoT [Edith]

* Q: What is relevant to ICN?

    * We concluded that security problems were not different from traditional sensor networks.

* Don’t compromise crypto when the real expense is the radio.

* What is the size of the attribute space for these schemes?

    * The time to process the tree is about 10 attributes/second.

        * Might see a 10x improvement now (100 attributes/second).

* Sensors just produce streams of data. Not every data stream needs to be known to other streams.

    * Some sensors produce streams upon request.

    * Some people expect computations to happen at gateways.

        * This depends on the scenario.

        * There’s no cost to having the sensor encrypt everything.

* Security is easier in isolated/local networks.

    * No need to do fancy cryptography when it’s not needed.

* Does ABE assume a management system?

    * Yes, that infrastructure is required. But that can be offline.

## Trust and Identity [Ken]

* Reviewed schematized trust.

    * Schema parsing is not onerous -- it’s simple.

* Reviewed Internet service incentives.

    * In IP you pay to move packets.

    * In ICN you pay for two services: publishing and retrieving data.

        * No conclusion here, but good to highlight.

* Hard questions surrounding billing, service payment, and related issues.

* No consensus on the necessity of a namespace authority.

    * Future Dagstuhl seminar?

    * Need more experience here.

## In-Network Processing and Related Laws [Tohru]

* [Slide 10] Are these speaker’s interpretations or the interpretations of the court?

    * Court decided in 2004, but copyright law was modified in 2009. Currently no problems.

* In the Western world, data can be stored for the "amount of time it’s technically needed to forwarded it," i.e., it’s not a copyright violation. 

* It’s not just a legal framework problem -- one must consider what the owner says. For instance, cache control headers might be needed to express owner concerns. 

* Content encryption also affects what a publisher determines is able to be placed on the network.

* In the US, handing off communications to a third party is interpreted as given up your 4th amendment rights to communication. 

    * Stored communications act allows data to be searched.

* Sending data through an ISP is different than through a third party.

* "It’s complicated."

# Wednesday Morning 2

## User-Generated Content in the FIB [Thomas]

* Is shortest-path routing the goal for user-generated names?

    * Maybe. Could have triangular routing. Redirection is possible.

* How are names trusted?

    * See earlier discussion.

* People publish under a DNS name or under a service-centric names. 

    * User-centric names can be injected into the network.

* There will be policies that restrict what names can be published in what parts of the network.

    * Policies will be applied before insertion into FIBs.

* The argument is not "completely open vs. completely closed" -- it’s that there will be policies and what are those policies?

* How is the hierarchy used in ICN?

    * Name-based routing with LPM and aggregation.

    * IP address space can be enumerated. Namespace in ICN cannot be enumerated.

* Assuming distributed routing. What if we had a centralized routing service?

## Summary [Börje]

* A lookup service does not solve routing problems, security or otherwise.

* Need to support crypto agility.

* Do architectures distinguish between names and locators? Should they?

* One name and one piece of data isn’t an axiom.

* People once believed that LPM would not be possible at line speeds.

    * Putting unbounded crypto in the data plane is bad, bounded crypto is good.

