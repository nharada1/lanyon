---
layout: post
title: List of Gotchas for Matlab/Python, In Order of Annoyance
comments: True
---
While the SciPy project already maintains a [complete list](http://wiki.scipy.org/NumPy_for_Matlab_Users) of the differences between NumPy and Matlab, that list is big and random and this list is small and somewhat ordered. My research is written in both Matlab and Python and, like the musician who yells the wrong city at their show, these are the mistakes I make most commonly when switching back and forth.

* Matlab indexes beginning with 1, Python with 0. This is well known, but can still trip you up when you frequently switch back and forth. This applies to *all* indexed values, such as the axis to apply a function to (the first axis is 1 in Matlab, 0 in Python).

* Numpy arrays are by default element-wise for multiplication and division. To perform traditional matrix multiplication you will need to use `np.dot`, because both `*` and `np.multiply` are element-wise. Python 3.5 will be [introducting the @ symbol](https://www.python.org/dev/peps/pep-0465/) for infix matrix multiplication, which will hopefully resolve some of the confusion. Similarly, Numpy offers `matrix` as an alternative to `ndarray`, but if you value your sanity you should stick with the arrays. The `matrix` class makes traditional matrix multiplication the default operator for the `*` symbol, at the expense of adding [restrictions](http://stackoverflow.com/questions/4151128/what-are-the-differences-between-numpy-arrays-and-matrices-which-one-should-i-u) and [caveats](http://stackoverflow.com/questions/12024820/danger-of-mixing-numpy-matrix-and-array) to literally everything else.


**Python:**
{% highlight python %}
A*B            # Element-wise
np.dot(A, B)   # Matrix multiplication
{% endhighlight %}


**Matlab:**
{% highlight matlab %}
A*B            # Matrix multiplication
A.*B           # Element-wise
{% endhighlight %}

* In Numpy, many functions require a tuple as an argument. This happens in functions like `concatenate` and `reshape`:

**Python:**
{% highlight python %}
A.reshape((5, 5)) # This works
A.reshape(5, 5)   # This doesn't
{% endhighlight %}

**Matlab:**
{% highlight matlab %}
reshape(A, 5, 5)
{% endhighlight %}

* In Numpy, arrays are not inherently multidimensional. Creating an array can create a 1d array, which does not even have a second dimension. Compare this to Matlab, where vectors are 1xN or Nx1 2d arrays. This small difference is a common source of pain, especially because it isn't caught by static checkers and will inevitably end up crashing the very end of your long script, right after you finish training a huge model and right before you display the results.

**Python:**
{% highlight python %}
a = np.arange(10)
a.shape => (10, )
a.reshape((10, 1))
a.shape => (10, 1)
{% endhighlight %}
