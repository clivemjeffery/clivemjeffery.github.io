---
layout: default
---

# Books

A reading list, of the books I've completed recently, ordered roughly by the date I've finished them and written them up.

{% for post in site.categories.book %}
* {{ post.author }}, [{{ post.title }}]({{ post.url | prepend: site.baseurl }})
{% endfor %}
