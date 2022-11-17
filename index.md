---
layout: base
---
*test*

<h2>Blog</h2>
<ul>
  {% for post in site.posts %} {% if post.category != "terrible_vegan" and
  post.category != "recipe" %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </li>
  {% endif %} {% endfor %}
</ul>

<h2><a href="/projects">Projects</a></h2>
<p>Complete, ongoing, concepts.</p>

<h2><a href="/music">Music</a></h2>
<p>Playlists. Music blog coming soon.</p>

## Some Of My Favorite Recipes.
- [Dosas](http://www.happyandharried.com/2018/04/04/idli-dosa-batter/)
- [Two-Ingredient cookies (Oatmeal+Banana)](https://theburlapbag.com/blog/2012/07/2-ingredient-cookies-plus-the-mix-ins-of-your-choice/)
- [Banana Peel Bacon](https://skillet.lifehacker.com/this-bacon-is-bananas-peels-that-is-1833479569)
- [Sourdough](https://www.kingarthurbaking.com/recipes/no-knead-sourdough-bread-recipe)
- [Vegan Sourdough Pancakes](https://zerowastechef.com/2020/02/19/vegan-sourdough-pancakes/)
- [Vegan Biscuits](https://minimalistbaker.com/the-best-damn-vegan-biscuits/)
- [Vegan Sourdough Flatbread](https://theveganasana.com/easy-sourdough-flatbread/)
- [Yabra aka Malfouf (vegetarian version)](https://plantbasedfolk.com/malfouf/)

## My Recipes
<ul>
  {% for post in site.posts %} {% if post.category == "recipe" %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </li>
  {% endif %} {% endfor %}
</ul>

<h2>Terrible Vegan Podcast</h2>
<ol start="0">
  {% for post in site.categories.terrible_vegan reversed %}
  <li class="episode-{{post.episode}}">
    <a href="/assets/terrible_vegan_{{ post.episode }}.mp3"
      >{{ post.title }} ({{ post.length }})</a
    >
  </li>
  {% endfor %}
</ol>

<div style="display: flex; justify-content: space-between;">
  <div style="width: 60%;">
    <h2>About</h2>
    <p>
      I'm Razzi Abuissa, a software engineer currently in the city of Iowa City,
      IA. My interests include free software, social justice, and
      sustainability.
    </p>
    <p>
      <a
        href="mailto:&#114;&#97;&#122;&#122;&#105;&#64;&#97;&#98;&#117;&#105;&#115;&#115;&#97;&#46;&#110;&#101;&#116;"
        >&#114;&#97;&#122;&#122;&#105;&#64;&#97;&#98;&#117;&#105;&#115;&#115;&#97;&#46;&#110;&#101;&#116;</a
      >
    </p>
    <p>
      <a href="/feed.xml">
        RSS
      </a>
    </p>
    <h2>Links</h2>
    <a href="https://razzi.abuissa.net/mtg-score-counter/">MTG Score Counter</a>
  </div>
  <div style="max-width: 200px;">
    <img
      style="width: 100%;"
      alt="Drawing of Razzi"
      src="img/razportrait-edit3.jpg"
    />
    <p style="text-align: center;">
      Drawing by <a href="https://helloarielliu.com/">Ariel Liu</a>
    </p>
  </div>
</div>
