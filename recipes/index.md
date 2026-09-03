---
layout: default
title: "Ricette"
permalink: /recipes/
---

<section class="recipe-section recipe-archive">
  <div class="recipe-section-heading">
    <h1>Ricette</h1>
    <span class="recipe-section-note">{{ site.recipes.size }} ricette</span>
  </div>

  <div class="recipe-archive-grid">
    {% for recipe in site.recipes %}
      {% include recipe-card.html recipe=recipe %}
    {% endfor %}
  </div>
</section>
