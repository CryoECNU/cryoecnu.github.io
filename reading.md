---
layout: post 
title: "Reading" 
description: "思想有多远，我们就可以走多远. <br>(We can go as far as we thought)" 
header-img: "img/top.png" 
---

{% for post in paginator.posts %}
<div class="post-preview">
    <a href="{{ post.url | prepend: site.baseurl }}">
        <h2 class="post-title">            
            {{ post.title }}
        </h2>
        {% if post.subtitle %}
        <h3 class="post-subtitle">
            {{ post.subtitle }}
        </h3>
        {% endif %}
        <div class="post-content-preview">
            {{ post.content | strip_html | truncate:150 }}
        </div>
    </a>
    <p class="post-meta">Posted by {% if post.author %}{{ post.author }}{% else %}{{ site.title }}{% endif %} on {{ post.date | date: "%B %-d, %Y" }}</p>
</div>

<hr>
{% endfor %}

<!-- Pager -->
{% if paginator.total_pages > 1 %}
<ul class="pager">
    {% if paginator.previous_page %}
    <li class="previous">
        <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&larr; Newer Posts</a>
    </li>
    {% endif %}
    {% if paginator.next_page %}
    <li class="next">
        <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Older Posts &rarr;</a>
    </li>
    {% endif %}
</ul>
{% endif %}
annual mean surface albedo feedback in the SH sea ice zone contributes to it having one of the smaller equilibrium temperature changes and a small SH polar amplification** (see Table 1).

> Source: Crook, J.A., P.M. Forster, and N. Stuber, 2011: Spatial Patterns of Modeled Climate Feedback and Contributions to Temperature Response and Polar Amplification. J. Climate, 24, 3575–3592, https://doi.org/10.1175/2011JCLI3863.1 