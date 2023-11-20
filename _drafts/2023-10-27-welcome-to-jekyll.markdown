---
layout: post
title:  "Welcome to Jekyll!"
date:   2023-10-27 11:57:45 +0200
categories: jekyll update
---


You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/


## Benji: Wow I hope this works?

```
Is this a code snippet?
def f(x): asdf
```

How about some latex? $$x^2$$?

$$
\sum_{i=1}^n blah = \int blah blah dx
\\
x + y = z
$$

 {% raw %}
  $$a^2 + b^2 = c^2$$ --> note that all equations between these tags will not need escaping! 
 {% endraw %}

How to get latex working - see:
https://www.iangoodfellow.com/blog/jekyll/markdown/tex/2016/11/07/latex-in-markdown.html
Basically, we had to go and edit the minima theme _layouts/post.html.
We find minima theme location by `bundle show minima` (somewhere in our file system)
And then add in a little snippet
```
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
```

# Testing out latex

$$ \nabla_\boldsymbol{x} J(\boldsymbol{x}) $$

## Testing out Markdown

- bullet points?
- I guess

> quotes?
> unsure

1. number?
2. Do I have to type out each number...