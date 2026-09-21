---
title: Get Started with C#
permalink: index.html
layout: home
---

The following exercises are designed to help you practice the skills you've learned in the [Get Started with C#](https://learn.microsoft.com/en-us/training/paths/get-started-c-sharp-part-1/) learning path on Microsoft Learn. Each exercise is self-contained and can be completed independently, but they are best used in conjunction with the corresponding modules on Microsoft Learn.

## Exercises

<hr>

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Exercises'" %}
{% for activity in labs  %}

### [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }})

{% if activity.lab.level %}**Level**: {{activity.lab.level}} \| {% endif %}{% if activity.lab.duration %}**Duration**: {{activity.lab.duration}} minutes{% endif %}

*{{activity.lab.description}}*
<hr>
{% endfor %}


> **Note**: While you can complete these exercises on their own, they're designed to complement modules on [Microsoft Learn](https://learn.microsoft.com/en-us/training/paths/get-started-c-sharp-part-1/); in which you'll find a deeper dive into some of the underlying concepts on which these exercises are based.