---
layout: post
title: 32-bit Wave Files in Python
---

Python 2.7 is seriously lacking in support of 32-bit float wave files -- the wave file module is [shooting for support in 3.4](http://bugs.python.org/issue16525) and the `scipy.io.wavefile` module have support unless you [build from source](https://github.com/scipy/scipy/pull/2440). Which requires a FORTRAN compiler. Not my idea of fun just to support a feature that should be included out of the box.

For my current project I've been using the [scikits.audiolab](http://www.lfd.uci.edu/~gohlke/pythonlibs/#scikits.audiolab) module to deal with my wave files. You'll need the numpy/scipy installed, as well as setup tools, but once installed it's really easy to work with.

For example, to read in a file you can do:

{% highlight python %}
from scikits.audiolab import wavread
data, sample_freq, encoding = wavread(path)
{% endhighlight %}

Easy.
