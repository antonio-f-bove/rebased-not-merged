---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: ./shaken-not-stirred.jpg
layout: image-right
image: ./assets/shaken-not-stirred.jpg
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
---

<div class="h-100 flex flex-col justify-center">
    <h1>Rebased, not merged</h1>
    <div>come e perché mantenere una <em>git history</em> il più lineare possibile</div>
</div>

<!-- Setting `pull.rebase = true` in the Git config is a great way to avoid unnecessary merge commits and keep the Git history cleaner. However, it's important to educate your team about some **changes in behavior** they might encounter after enabling this setting, especially since they're used to their IDE handling Git operations for them. Here's what they might notice: -->

---
layout: center
# layout: image
# image: assets/rebasing-vs-merging-diagram.png
# backgroundSize: contain
---

# `git pull` == `git fetch` + `git merge`

---
layout: image-right
image: assets/rebasing-vs-merging-diagram.png
backgroundSize: contain
---

<br><br><br>
## Merge strategy

<br>

La strategia di default di Git, quando si `git pull`, è la merge: in caso di divergenza tra la remote e il nostro locale crea un **merge commit** (che ci siano conflitti o meno).

---
layout: image-left
image: assets/rebasing-vs-merging-diagram.png
backgroundSize: contain
---

<br><br><br>
## `git pull --rebase`

<br>

C'è una strategia alternativa: **rebase**. Con questo comando git, invece di effettuare una merge, *stacca* i nostri commit locali, per *riapplicarli* poi dopo le nuove changes introdotte con la pull

---
layout: center
---

# Un grosso vantaggio: una storia lineare
Non ci sono più i *merge commit*, e non verranno mantenuti nella *git history* i nostri branch **locali temporanei**...

<img v-click src="./assets/git-history-rotated.png" class="mt-8 block mx-auto" />
<!-- TODO: add meme: no more! -->

---
layout: center
---

# Vantaggi di una storia lineare
- Maggiore facilità di visualizzazione
- Maggiore facilità nel *debugging* (`git bisect`)
- Possibilità di facile *rollback* (`git revert`)
- Maggiore facilità nel portare codice da un branch all'altro (`git cherry-pick` utile per portare changes da v4 in *shared-dataset*)

---
layout: center
---

# Svantaggi
- ### Alcuni cambi nel workflow legato al `git pull`
    - In particolare sarà sempre necessario fare lo *stash* delle modifiche presenti non committate prima di poter pullare

<!-- <div v-click>boom baby</div> -->

- ### Cambio nella gestione dei conflictti
    - gestire conflitti (nessuna differenza)
    - `git rebase --continue`
    - In rari casi potrebbe rendersi necessario risolvere lo stesso conflitto più di una volta...

---
layout: center
---

## In questi casi si giustifica semplificare usando la classica merge!
<div class="flex flex-col justify-center items-center mt-8">
    <div v-click><code>git rebase --abort</code></div>
    <div v-click><code>git pull --no-rebase</code></div>
    <div v-click class="text-red">Linea di comando necessaria!</div>
</div>

---

# Configurazione

## Linea di comando
`git config pull.rebase true`

## Visual Studio
Tools > Options > Git Repository Settings > Rebase local branch when pulling
> È possibile configurarlo a livello globale oppure a livello di repository (consigliata la seconda)

---
layout: image
image: ./assets/vs-options.png
---

---
layout: cover
# image: ./assets/bond-martini-2.webp
background: ./assets/bond-martini-2.webp
---

<h3 class="mt-80">Grazie per l'attenzione</h3>
