---
draft: false
date: 2014-11-05
title: Movistar DNS
tags: DNS
---
I had been suffering connection issues lately which made the internet feel slow. Frustrating, as I have a 100 Mbps FTTH connection. The problem is the DNS.

Most of the time I use [Google's DNS](https://developers.google.com/speed/public-dns/):
- 8.8.8.8
- 8.8.4.4

At one point I decided I should use Movistar's own DNS because it pings in about 5ms, which is good, so I added them to my DNSs. However they are not reliable at all. I can only guess that the OS chooses the DNS based on their ping (*any help? How do Macs do it?*). The solution, remove them and stick to the Google ones. Although they ping in about 40ms (8x slower, this is because I am in Europe), they seem to be more reliable.
