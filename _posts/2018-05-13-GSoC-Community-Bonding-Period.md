---
layout: post
title:  "Start of GSoC 2018: Community Bonding Period"
date:   2018-05-13
excerpt: "Community Bonding Period: April 24 — May 14, 2018."
tag:
- GSoC
comments: true
---

# Start of GSoC 2018: Community Bonding Period

## Community Bonding Period: April 24 — May 14, 2018
I started with GSoC on 24 April. I made contact with my mentors. I came to know that my primary mentor is Huijian Lv, littleowen and Mark Turner. I am talking to them since then. They also created a slack team for this year’s GSoC projects.

### CWRU HPC Accounts
All students under Red Hen Lab were given access to HPC cluster at CWRU. Prof. Mark Turner asked us some details and our RSA public keys. In one or two days, our accounts were ready. Initially, I faced some problems while making a login into HPC cluster (password problems 😉). But after some days, that problem also resolved.

It turns out that the RedCat cluster is going away at the end of this month. So we finally use the Rider cluster (rider.case.edu) instead.

{% highlight shell %}
CynthiaHsus-MacBook-Pro:~ suwi$ ssh sxx186@redhen1.case.edu
Last login: Tue May  8 13:44:37 2018 from 174.104.175.117

sxx186@redhen1:~$ ssh sxx186@rider.case.edu
Last login: Mon Apr 30 15:02:00 2018 from 129.22.100.134

[sxx186@hpclogin ~]$ cd /mnt/rds/redhen01/redhen/
[sxx186@hpclogin redhen]$ ls
home  tv

[sxx186@hpclogin redhen]$ cd home
[sxx186@hpclogin home]$ ls
axd500   dxc496  exs449  hxx124  kxs784  naa56   skv19   sxk1195  vlt6
axh617   dxl574  fxs161  ixg82   lxr181  pxu17   stg32   sxk1299  vma15
axs1559  dxp329  gxs393  jxj442  mbt8    rxs926  sxa684  sxt313   wxl430
cxt283   ekj9    hxs503  kxs675  mxp523  skr63   sxg755  sxx186   zxx302
{% endhighlight %}

### Chinese pipeline
To go to a particular day, issue "day" with the date or the number of days ago:
{% highlight shell %}
day + 5
day - 30
{% endhighlight %}

To navigate between dates, use:
{% highlight shell %}
module load ffmpeg
for DAY in {08..31} ; do day 2018–01-$DAY ; for FIL in *_CN_*.txt ; do echo $FIL ; grep 'DUR|' $FIL ; ffprobe ${FIL%.*}.mp4 ; done ; done
{% endhighlight %}

View all the files related to Chinese Pipeline:
{% highlight shell %}
mbt8@dtn1 /mnt/rds/redhen01/redhen/tv/2018/2018–01 $ ls */*_CN_* -d
{% endhighlight %}

### Deep Speech 2
My GSoC project is an extension to DeepSpeech2 on PaddlePaddle.
- The first work in the future for me is to understand and run existing code in my system: Practice on DeepSpeech2 Project using PaddlePaddle.
- Another work which should be accomplished is to download the training data from the server.

## Conclusion
Now the bonding period is over, and coding has started. I am strictly following my timeline, as proposed by me during GSoC application period (given on my proposal). I will be talking about the first week very soon. The first week gets over on 21 May. Till then, happy coding and cheers.
