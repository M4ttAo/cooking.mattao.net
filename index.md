---
layout: default
title: "Cook With MattAo"
description: "Il mio archivio personale di ricette. Testate, approvate e pronte da rifare."
---

<section class="recipe-hero">
  <h1>Cook With MattAo</h1>
  <p>Il mio archivio personale di ricette. Testate, approvate e pronte da rifare.</p>
</section>

<section class="recipe-section">
  <div class="recipe-section-heading">
    <h2>Ricette Top</h2>
    <a href="#ultime-inserite">vedi le ultime inserite →</a>
  </div>

  <div class="recipe-top-grid">
    {% for recipe in site.recipes %}
      {% if recipe.top %}
      {% include recipe-card.html recipe=recipe %}
      {% endif %}
    {% endfor %}
  </div>
</section>

<section class="recipe-section" id="ultime-inserite">
  <div class="recipe-section-heading">
    <h2>Ultime inserite</h2>
    <a href="#categorie">esplora per categoria →</a>
  </div>

  <div class="recipe-feature-grid">
    {% assign latest_recipes = site.recipes | sort: "date" | reverse %}
    {% for recipe in latest_recipes limit: 4 %}
      {% include recipe-card.html recipe=recipe %}
    {% endfor %}
  </div>
</section>

<section class="recipe-section" id="categorie">
  <div class="recipe-section-heading">
    <h2>Categorie</h2>
    <span class="recipe-section-note">scorri per esplorare</span>
  </div>

  <div class="recipe-board">
    {% for category in site.data.categories %}
      <section class="recipe-category">
        <h3>{{ category }}</h3>
        <div class="recipe-category-list">
          {% for recipe in site.recipes %}
            {% if recipe.tags contains category %}
              {% include recipe-card.html recipe=recipe compact=true %}
            {% endif %}
          {% endfor %}
        </div>
      </section>
    {% endfor %}
  </div>
</section>
