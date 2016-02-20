---
layout: default
---

# Training

I love to cycle and occasionally take part in cyclo-sportives or other cycling challenges. Therefore, I must train!

### Strava

<iframe height='160' width='300' frameborder='0' allowtransparency='true' scrolling='no' src='https://www.strava.com/athletes/98197/activity-summary/0a54d52cf7ece1a03ec181f60551e8495d50882d'></iframe>

### QBike

I use my QBike project to monitor indoor sessions on the rollers.

{% for file in site.static_files reversed %}
	{% assign folder = file.path | split:"/" %}
	{% if folder[1] == "qbike_session" %}
* {{folder[2]}} ![session]({{ file.path }})
    {% endif %}
{% endfor %}
