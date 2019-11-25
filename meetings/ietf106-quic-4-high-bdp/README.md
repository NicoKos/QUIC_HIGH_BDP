## Minutes of the Quic4Sat side meeting at IETF-106
The workshop is organized by CNES (Nicolas), U. of Aberdeen (Gorry) and Orange (Emile). 
Number of participants : 34 + 1 remote (more joined later)

# 1-side-meeting-quic-high-bdp 
Introduction of the side-meeting, agenda bashing and note well. 

# 2-side-meeting-quic-high-bdp-sat-charac-challenges

Currently satellite use pair of  proxies (PEP) to transfer TCP/IP traffic. 
This architecture does not work for QUIC because QUIC headers are end-to-end authenticated and encrypted.

Nicolas presented a SWOT analysis of QUIC in SATCOM. draft-kuhn-quic-4-sat motivated the desire to find new solutions for QUIC to replace PEPS currently deployed for TCP. We shared John Border's early results, and initial results from Nicolas and Gorry.

Aaron: I think the focus could have been explicitly on satellite, not high BDP, because most impacts are due to latency. 

Gorry: The term high BDP covers many things some people move data via long-fat satellite segments. Some cellular links have less delay than satellite, but can have higher rate, and may share other properties. Some people move terabits over short-very-fat networks e.g., data centres and between data centres. Sometimes BDP is the issues sometimes RTT, we should probably separate those topics.

Nicolas: The objective of this meeting is also to try gathering people involved in "high bandwidth-short RTT" networks to see if we have a common interest.

Aaron : Is there anyone involved in such networks in the room ?  
No-one wanted to discuss that at that time.

# 3-quic-satellite-return-link

Gorry presented the results of measurement of the impact of ACK frequency on satellite communication. The platform was based on Fastly QUIC implementation. 

Jana - I couldn't read the vertical axes on gorry's charts.

Gorry - Aha - They're bytes/transfer. I have criticised other people that way before, so sorry. I'll fix and post the updated slides.

Jana - We should be careful we don't benchmark Quicly or some other implementation.

Gorry - I think we were careful to make sure what we tested was allowed in the QUIC Spec - any small bugs we found, we were careful to  fix - and w’ll tell you, so the effects are permitted by the spec - but may not be in other implementations...

Ian Swett - Google have lots of data about looking at different ACK ratios - and in Chrome have experimented with adapting to 10.

Jana - There was an issue in the tracker about this and we stopped taking this forward.

Christian - I've experimented with an adaptive method in picoquic that grows the window exponentially.

Gorry - Since using 2 is a real issue, I would like to re-open that discussion - at least to recommend a simple method. For us, 2 then 10 could be enough to have a large effect - really interested in knowing more about Chrome.

Christian - Why an ACK Ratio of 1:10?

Gorry - This happens to be enough for the sorts of links we currently look at. It also means that bursts are upto 10 packets  (the rationale for IW=10, was that this burst could be accommodated in buffers).

Gorry - Flow control is another area that can really impact performance and sender behaviour, but underspecified at present.

Ian Swett - I think all the flow control is implemented differently and I agree the spec does not say much about this.  I think in the next version we can have a frame to explicitly set this sort of parameters.

Kazuho - I could say more about why we did flow control this way for our use case and discuss this.

Gorry - I would like to open this issue again and see if we can take it just a little further because it is also a real problem, and we are gathering experience already.

Jana - We should continue the exchange on this and other parameters. We should focus on data and what can be introduced to QUIC.

# 4-side-meeting-quic-high-bdp-loss

Nicolas presented briefly the results (already presented during MAPRG) of the measures of on-path packet loss made by Orange (Alex), the CNES and Louvain Univ.

Christian Huitema asked for a model to share to enable comparisons. Nicolas will check for the reusability of their models. 

There was some general questions on the current and expected satellite characteristics : satellite characteristics are not known (bandwidth, loss location, loss occurrence, delay). We suggested an initial focus on GEO satellite for home broadband.

Christian suggested it would be useful to have parameters that could be used to run regression tests for different types of satellite systems.

Nicolas/Gorry : Described some of the many systems. We will add details in a document. 

# 5-COPE-ETOSAT-IETF106 side meeting

Not enough time to discuss the "Performance Enhancement via QUIC Proxy" slides. 

# 6-QUIC-tunnels-in-the-VIBeS-project
We are sorry if we lacked time to present the QUIC experiments from the VIBES project [https://artes.esa.int/projects/vibes]. 
If you are interested, you can contact Simon Pietro Romano <spromano@unina.it>.
