---
layout: default
title: "Cook With MattAo"
description: "Il mio archivio personale di ricette. Testate, approvate e pronte da rifare."
---

<section class="recipe-hero">
  <p class="recipe-eyebrow">CookingTao</p>
  <h1>Cook With MattAo</h1>
  <p>Il mio archivio personale di ricette. Testate, approvate e pronte da rifare.</p>
</section>

<section class="recipe-section">
  <div class="recipe-section-heading">
    <h2>Ultime inserite</h2>
    <a href="#categorie">esplora per categoria →</a>
  </div>

  <div class="recipe-feature-grid">
    {% for recipe in site.recipes limit: 4 %}
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
            {% if recipe.categories contains category %}
              {% include recipe-card.html recipe=recipe compact=true %}
            {% endif %}
          {% endfor %}
        </div>
      </section>
    {% endfor %}
  </div>
</section>

<section class="recipe-section recipe-top-section">
  <div class="recipe-section-heading">
    <h2>Ricette Top</h2>
  </div>

  <div class="recipe-top-list">
    {% for recipe in site.recipes %}
      {% if recipe.top %}
        <a href="{{ recipe.url | relative_url }}">
          <span class="recipe-card-icon" aria-hidden="true">{{ recipe.icon }}</span>
          <span>{{ recipe.title }}</span>
        </a>
      {% endif %}
    {% endfor %}
  </div>
</section>

<section class="recipe-about">
  <p class="recipe-eyebrow">Dietro al Grembiule</p>
  <h2>Ciao, sono Matteo.</h2>
  <p>In questo spazio raccolgo solo le ricette che ho provato e che mi sono piaciute davvero. Niente storie infinite o introduzioni inutili: solo ingredienti, passaggi chiari e piatti che funzionano.</p>
</section>
