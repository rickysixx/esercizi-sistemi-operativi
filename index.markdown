---
layout: default
---

* Table of contents
{:toc}

# Domande d'esame

{% for domanda in site.data.domande %}

{{ domanda.domanda | markdownify }}

<details>
    <summary><strong>Soluzione</strong></summary>

    {{ domanda.soluzione | markdownify }}
</details>

{% endfor %}

---

{% for lezione in site.data.lezioni %}
# Lezione {{ lezione.numero }} - {{ lezione.titolo }}

{% for esercizio in lezione.esercizi %}
## Esercizio {{ esercizio.numero }} (slide {{ esercizio.slide }})

{{ esercizio.traccia | markdownify }}

<details>
    <summary><strong>Soluzione</strong></summary>

    {{ esercizio.soluzione | markdownify }}
</details>

{% endfor %} {% comment %} esercizio {% endcomment %}
{% endfor %} {% comment %} lezione {% endcomment %}
