---
layout: post
title:  "Jekyll Rocks!"
date:   2016-04-07
---
I have to admit, I've been looking for something like [Jekyll][jekyll] for a long time!
Guys at [GitHub][github] just know how to create awesome products.
 
My personal website used to be written in ASP.NET, and it felt not the right tool for the job.
Of course, you don't need active server pages for a couple of HTML documents, but you do for the blog.
There is always WordPress, however it's too heavy, slow, requires to remove almost everything before desired look-and-feel.
No, WP, thanks, next time. 

Not speaking of free hosting!

Ok, I'm a fan now, let's create our awesome blog. 
We would need a couple of useful things: Comments and Analytics.

## Disqus comments
It seems that [Disqus][disqus] commenting system is everyone's favourite, We'll use it as well. 
Comments will be enabled by default, to disable just add `comments: false` to post [Front Matter][frontmatter]
{% highlight liquid %}
{% raw %}
{% if jekyll.environment == "production" and page.comments != false %}
   {% include disqus.html %}
{% endif %}
{% endraw %}
{% endhighlight %}

By the way, to highlight a Liquid template inside Liquid template we need to use `raw` tag
{% highlight liquid %}
{% raw %}
{% highlight liquid %}
{% raw %}
 ...
{% endraw %}
{% endhighlight %}
Don't forget to close tags with `endraw` and `endhighlight`.
This was skipped from the example, because Liquid throws syntax errors for nested tags.

`disqus.html` is located in `_includes` folder and contains [universal embed code][disqus-embed-code]

Disqus asks to provide two config variables, page's canonical URL and page's unique ID. 
To get unique ID we'll use additional hash generator ([author][js-hash-generator]).
{% highlight javascript %}
{% raw %}
String.prototype.hashCode = function() {
    var hash = 0, i, chr, len;
    if (this.length === 0) return hash;
    for (i = 0, len = this.length; i < len; i++) {
        chr   = this.charCodeAt(i);
        hash  = ((hash << 5) - hash) + chr;
        hash |= 0; // Convert to 32bit integer
    }
    return hash;
};

var disqus_config = function () {
    this.page.url = {{ page.url | prepend: site.url }};
    this.page.identifier = this.page.url.hashCode();
 };
{% endraw %}
{% endhighlight %}

## Google Analytics
We just need to add a snippet to our default page template

{% highlight liquid %}
{% raw %}
{% if jekyll.environment == "production" %}
  {% include ga.html %}
{% endif %}
{% endraw %}
{% endhighlight %}

## [Github Pages][github-pages] hosting 

Everything is pretty straightforward: we need to push our code to `sbedulin.github.io:master` 
and add CNAME file for a [custom domain][custom-domains]. Github gives a [good overview][custom-domains] on how to 
set up a custom domain, subdomains, configure DNS records, differences between CNAME and A, etc, 
make sure to check it out. 

BTW, Github Pages sets `JEKYLL_ENV` to `production` for us.

[jekyll]: http://jekyllrb.com
[github]: http://github.com
[disqus]: https://disqus.com
[disqus-embed-code]: https://help.disqus.com/customer/portal/articles/472097-universal-embed-code
[frontmatter]: https://jekyllrb.com/docs/frontmatter/
[js-hash-generator]: http://werxltd.com/wp/2010/05/13/javascript-implementation-of-javas-string-hashcode-method/
[github-pages]: https://pages.github.com/
[custom-domains]: https://help.github.com/articles/using-a-custom-domain-with-github-pages/
