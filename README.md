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
