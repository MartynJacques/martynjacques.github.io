---
layout: post
title: "Enable HTTPS on GitHub Pages"
---

HTTPS adds a layer of security on top of HTTP to allow encrypted data to
transfer between the web browser and web server.

All browsers flag non-HTTPS websites as potentially insecure, this shows an
ugly warning and it's also just bad practice. HTTPS is easy to add to a
GitHub Pages site, so let's just do it.

In your GitHub Pages repo, head to "Settings" and check the box labelled
"Enforce HTTPS". Allow GitHub to refresh your web server and that's all,
you're done.

Well, you might be.

You may need to update your static site generator to ensure any links from
your site use the HTTPS protocol. If your website serves links using
non-secure http, the browser will still display a warning.

In Jekyll, the generator I use, you achieve this by ensuring the `url` field
in your config file contains the https link to your site.
~~~ bash
$ grep url _config.yml
url: https://martynjacques.github.io
~~~
This link is prepended to any relative link via the following syntax, so you
can be assured you don't need to update each link individually.
{% raw %}
~~~ html
<link rel="canonical" href="{{ site.url }}{{site.baseurl}}{{ page.url }}" />
~~~
{% endraw %}

Let's check the site information to make sure we've now got a secure
connection.

![Firefox Site Info]({{ site.url }}/assets/images/site_info.png)

Looks like we have a happy browser and a happy user!
