---
layout: default
title: Archive
permalink: /archive/
published: true
---

<script type="text/javascript">
function handle_selection(element) {
    window.location = element.value;
    if (element.value != "#all") {
        $('.catbloc_showing_all').removeClass('catbloc_showing_all').addClass('catbloc');
    } else {
        $('.catbloc').removeClass('catbloc').addClass('catbloc_showing_all');
    }
}
</script>

<nav>

    <select id="category_selector" name="Categories" onchange="handle_selection(this);">
        <option value="#all" selected="selected">All posts</option>
        {% for category in site.categories %}
            <option value="#{{ category | first | remove:' ' }}">{{ category | first }}</option>
        {% endfor %}
    </select>
        <!--<a href="#{{ category | first | remove:' ' }}"><strong>{{ category | first }}</strong></a>{% if forloop.last %}.{% else %}, {% endif %}-->

</nav>

{% for category in site.categories %}
<div class="catbloc_showing_all" id="{{ category | first | remove:' ' }}">
    <h2 class="category_header">{{ category | first }}</h2>
         
    <ul class="posts">
        {% for posts in category %}
            {% for post in posts %}
                {% if post.url %}
                    <li>
                        <span class="date">{{ post.date | date_to_string }}&raquo; </span><a href="{{ post.url }}">{{ post.title }}</a>
                    </li>
                {% endif %}
            {% endfor %}
        {% endfor %}
    </ul>
</div>
{% endfor %}