# 分页
> 现在这一章节来看看怎么实现分页功能

* 首先添加包
* 重写home方法
* 修改模板

在my_blog/my_blog/views.py中引入包


![10-django-page-import](_images/django-blog/10-django-page-import.png)

修改my_blog/my_blog/views.py中的home函数


![10-django-view](_images/django-blog/10-django-view.png)

修改my_blog/templates下的home.html

```
{% extends "base.html" %}

{% load custom_markdown %}
{% block content %}
<div class="posts">
    {% for post in post_list %}
        <section class="post">
            <header class="post-header">
                <h2 class="post-title"><a href="{% url 'detail' id=post.id %}">{{ post.title }}</a></h2>

                    <p class="post-meta">
                        Time:  <a class="post-author" href="#">{{ post.date_time |date:'Y M d'}}</a> <a class="post-category post-category-js" href="{% url 'search_tag' tag=post.category %}">{{ post.category|title }}</a>
                    </p>
            </header>

                <div class="post-description">
                    <p>
                        {{ post.content|custom_markdown|truncatewords:10 }}
                    </p>
                </div>
                <a class="pure-button" href="{% url 'detail' id=post.id %}">Read More >>> </a>
        </section>
    {% endfor %}

    {% if post_list.object_list and post_list.paginator.num_pages > 1 %}
      <div>
      <ul class="pager">
      {% if post_list.has_previous %}
        <li><a href="?page={{ post_list.previous_page_number }}">上一页</a></li>
      {% endif %}

      {% if post_list.has_next %}
        <li><a href="?page={{ post_list.next_page_number }}">下一页</a></li>
      {% endif %}
      </ul>
      </div>
    {% endif %}
</div><!-- /.blog-post -->
{% endblock %}
```





