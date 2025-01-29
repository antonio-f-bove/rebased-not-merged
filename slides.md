---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
# background: ./shaken-not-stirred.jpg
layout: image-right
image: /shaken-not-stirred.jpg
# some information about your slides (markdown enabled)
title: Rebased, not merged
info: |
  come e perché mantenere una git history il più lineare possibile
  
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
# image: /rebasing-vs-merging-diagram.png
# backgroundSize: contain
---

# `git pull` == `git fetch` + `git merge`

---
layout: image-right
image: /rebasing-vs-merging-diagram.png
backgroundSize: contain
---

<br><br><br>
## Merge strategy

<br>

La strategia di default di Git, quando si `git pull`, è la merge: in caso di divergenza tra la remote e il nostro locale crea un **merge commit** (che ci siano conflitti o meno).

---
layout: image-left
image: /rebasing-vs-merging-diagram.png
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

<div v-click class="flex flex-col items-center">
  <div><img src="/git-history-rotated.png" class="mt-8 block mx-auto" /></div>
  <div><img class="h-70 pt-4" src="/stop-arnold.png" /></div>
</div>

---
layout: center
---

# Vantaggi di una storia lineare
- Maggiore facilità di visualizzazione
- Maggiore facilità nel *debugging* (`git bisect`)
- Possibilità di facile *rollback* (`git revert`)
- Maggiore facilità nel portare codice da un branch all'altro (`git cherry-pick` utile per portare changes da v4 in *shared-dataset*)

---
layout: cover
---

# Svantaggi

---
layout: center
---

# Alcuni cambi nel workflow legato al `git pull`
- In particolare sarà sempre necessario fare lo *stash* delle modifiche presenti non committate prima di poter pullare
- Mitigabile con un'altra configurazione: `git config rebase.autostash true`
- Attenzione: la riapplicazione automatica dello stash potrebbe introdurre conflitti non triviali

---
layout: center
---

# Cambio nella gestione dei conflictti
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
Tools > Options > Git Repository Settings > Rebase local branch when pulling => True
> È possibile configurarlo a livello globale oppure a livello di repository (consigliata la seconda)

---
layout: image
image: /vs-options.png
---

---
layout: cover
# image: /bond-martini-2.webp
background: /bond-martini-2.webp
---

<h3 class="mt-80">Grazie per l'attenzione</h3>

---
layout: center
---

# Bonus

copia-incolla nel terminale per settare tutto

```bash
git config pull.rebase true
git config rebase.autostash true
```
