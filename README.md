Rate Limiting and Traffic Shaping16.
===================================

16. Would you use a leaky bucket or a token bucket to traffic shape a constant bit rate (CBR)audio stream? Explain
why.

  - you would use a leaky bucket. According to the lectures, leaky buckets are for constant bit rates and token buckets are for bursty

17.  If you want to traffic shape a variable bit rate (VBR) video stream with average bit rate 6Mbps and maximum bit rate 10 Mbps, should you use
a leaky bucket or a token bucket? Whatvalues should you use for rho and beta if you want to allow bursts of up to 500 ms?

  - token (bursty)
  - rho should be 6Mbps and beta should be 250KB

18.  Suppose you’re running an ISP and get the crazy idea that implementing Power Boost foryour own network would be a good idea. For the 6 Mbps service plan (i.e., customers can
havea sustained rate of 6 Mbps), you’d like to allow them to burst up to 10 Mbps for up to 10seconds. In megabytes (MB), what should you set the beta
parameter of your token bucket to?(Round to the nearest tenth of a MB, i.e., one decimal place.)

```
(10Mbps - 6Mbps)*10sec => 40Mb
40Mb/(8bits per Byte) => (10/2)MB
=> 5MB
```


19.  Read about the following two ​Active Queue Management (AQM)​ techniques: ​Random EarlyDetection (RED)​ and​​CoDel​.
  Although they vary in specifics, these two algorithms share acommon basic approach to solving the buffer bloat problem. Explain what that approach is andwhy it works.

  - they both drop packets before the buffer is full. This forces senders to reduce their sending rates early enough to prevent buffer bloat.

20.  If you want to find out if a remote host (i.e., not ​your ​server) is currently under a DoSattack, would you use active or passive
     measurement? Explain why.

### Original
  - you should use passive measurement. First off, looking at flow rates would determine if an enormous flow (DDoS) is happening. Second, adding to
    the traffic by attempting to inject active measurement will probably just add to the attack. You'll most likely lose the response.
  - **this is wrong**

### Actual
  - It's wrong because only the server owners can inspect their own logs and flows. You would need to use ping (or other active measurement).

21.  If you want to compute the traffic intensity, I=La/R, on a router interface (i.e., the ratiobetween arrival rate
and forwarding rate), would you use Counters, Flow Monitoring, or PacketMonitoring? Explain why.

  - you only need to use counters in this particular case

Reading – CUBIC TCP
======================

6. Why does the linear growth rate of TCP-RENO (1/RTT) perform poorly for short lived flows innetworks with large bandwidth and delay products?
  - INITIAL: because tcp slow-start doesn't lend itself to short lived flows. It never encounters a congestion event

7. Describe the operation of BIC-TCP’s binary search algorithm for setting the congestionwindow. Once stable, how does BIC-TCP react to changes in available bandwidth, i.e. whathappens when there is a sudden increase or decrease in available bandwidth?
  - this is worded poorly. Basically describe how the previous Wmax is now the plataeu area

8. How does the replacement of this congestion control algorithm with a cubic growth functionin CUBIC-TCP improve on BIC-TCP? Discuss.
  - BIC approximates a cubic growth  function, but inefficiently. It uses multiple algorithms for each section of the curve.

9. What is the purpose of the following regions of the CUBIC growth function:
a. Concave
  - This is the logarithmic increase to the previous value of Wmax
b. Plateau
  - once the previous value of Wmax is reached, the flat portion is to allow the competing flows to achieve stability
c. Convex
  - max probing

10. How does CUBIC’s fast convergence mechanism detect a reduction in available bandwidth(i.e. a new flow competing for bandwidth)?
  - packet loss happens (congestion event)

Reading – TCP Fast Open
=====================

11.  What kinds of web traffic stand to benefit most from utilizing the TFO option?  How doesTFO improve the performance of these flows?
WRONG  - sites that initial network response exceeds the 2xRTT
CORRECT - exactly the opposite. On short-lived connections that are dominated by the RTT

12.  Describe how a trivial implementation of TCP Fast Open (in which the server replies to a allHTTP GET requests with a TCP SYN-ACK packet with data attached) can be exploited to mount asource address spoof attack.  How does TFO prevent this?
  - the server issues a TFO cookie to prevent this kind of spoofing

Reading - Multi Path TCP (MPTCP)
=================================

13.  What threat do network middleboxes pose to negotiating MPTCP connections?  How doesthe design of MPTCP mitigate this?
14.  Why are receive buffer sizes required to be larger for MPTCP enabled connections?  Whatcontrols does MPTCP put in place to maximize memory usage?


Content Distribution
======================

27.  If your browser has a page in the cache and wants to know if the page is still fresh and can be used, or is too old and should be replaced with fresh content from the server, which HTTPmethod should it use to find out?(If you are familiar with the If-Modified-Since header field, which we have not discussed in thisclass, please assume that we are not using If-Modified-Since.)

  - HEAD is the one you want. Otherwise you'd use a GET

28.  Consider the HTTP protocol. What will cause a server to send a response message with thestatus code...
  a. 404 Not Found ?
    - this is a client-side error. If the client requests a url or subdomain that doesn't exist, the server will respond with a 404.

  b. 302 Moved Temporarily (also sometimes called 302 Found) ?
    - this is a redirect. If the application code (server side) implements a redirect, it with repyl with a 302.

  c. 200 OK ?
    - success response

29.  Consider the HTTP protocol. What would the following header fields be used for?
  a. Last-Modified
  b. Host
  c. Cookie

30.  Of the various methods to redirect web requests to CDN servers, DNS redirection is themost common. Why would this method be more popular than the alternatives?

31.  How does BitTorrent implement the tit-for-tat algorithm? Be sure to explain in detail,including the roles of both choking and unchoking.

32.  In a distributed hash table, how many steps (hops) are required to lookup an item if thefinger table is a constant size (i.e., its size does not depend on the number of DHT nodes in thesystem)? Explain why that is the right answer.

33.  For a more typical DHT setup where the finger table has O(log N) entries, for N DHT nodesin the system, explain why the number of steps to access an item is O(log N).
