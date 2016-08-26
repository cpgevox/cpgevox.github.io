---
layout: papage
title: En Mathématiques
---

<!-- Load jQuery -->
<script src="//code.jquery.com/jquery-1.11.1.min.js"></script>
<!-- Load KaTeX -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.js"></script>

L’essentiel est de démarrer l’année reposé et très motivé. Le cours de mathématiques de PTSI est certes ambitieux mais progressif. Nous prendrons le temps nécessaire à l’acquisition des concepts essentiels.

L’usage des calculatrices restera anecdotique et son usage sera même interdit durant les devoirs surveillés. Néanmoins, l’informatique prend une part de plus en plus importante dans toutes les sciences, les mathématiques ne font pas exception. Pour illustrer certaines parties du cours nous utiliserons des logiciels de calcul formel ou de représentations graphiques. Pour vous familiariser avec ces outils vous pouvez éventuellement installer le logiciel gratuit [Sage](http://www.sagemath.org) (on peut en trouver une présentation rapide [ici](http://doc.sagemath.org/html/fr/a_tour_of_sage/index.html), un tutoriel [là](http://doc.sagemath.org/html/fr/tutorial/index.html) et même un [manuel plus complet](http://sagebook.gforge.inria.fr)) ou [Xcas](https://www-fourier.ujf-grenoble.fr/~parisse/giac_fr.html) sur vos ordinateurs personnels (si vous en possédez un, évidemment).

Nous commencerons l’année par une grande révision et des compléments d’analyse. Pour vous entraîner et rester mathématiquement actif durant les vacances voici quelques exercices que nous corrigerons à la rentrée. Si vous rencontrez des difficultés, pas de panique, les notions seront revues et ré-expliquées.

MM. Stival et Brunet, professeurs de Mathématiques.

# Quelques exercices de révision

## Exercice 1

On considère la fonction $$f$$ définie par $$f(x) = \frac {2x^2+1} {x^2+x}$$.

1. Déterminer le domaine définition de $$f$$.
1. Résoudre l’équation $$f(x)=\frac{3}{2}$$ et les inéquations

$$ f(x)\ge \frac{3}{2} \qquad \mathrm{et} \qquad f(x)\le \frac{5}{2} $$

1.  Déterminer la limite de $$f(x)$$ quand $$x$$ tend vers $$+\infty$$.
4.  À l’aide d’une machine (calculette ou ordinateur) tracer la courbe de $$f$$ et visualiser sur votre graphique les résultats précédents.

## Exercice 2

On considère la fonction $$f$$ définie par $$f(x) = x^4 - 2 x^2$$.

1. Dresser le tableau de variations de $$f$$ en indiquant les limites.
2. Puis, sans vous aider d’une machine, représenter la courbe de&nbsp;$$f$$.

## Exercice 3

On considère les fonctions $$ f $$ et $$g $$ définies, pour tout $$ x \in \mathbf R $$,&nbsp;par

$$f(x) = \frac 1 {1 + x^2} \qquad \mathrm{et} \qquad g(x) = f(2x + 3) $$

1.  Déterminer la fonction $$g'$$.
2.  Déterminer une équation des tangentes à la courbe $${\mathcal{C}}$$ de&nbsp;$$g$$ en&nbsp;$$0$$ et&nbsp;$$-{\frac{3}{2}}$$. Puis déterminer l’intersection entre ces droites.
3.  Visualiser vos résultats sur un graphique obtenu à la machine

## Exercice 4

Résoudre dans $$ \mathbf R $$ les équations suivantes. On précisera pour chaque équation le domaine de résolution.

1.  $$\ln(x^2 + x) = \ln 2$$
2.  $$\ln x - \ln(x + 1) = -1$$
3.  $${\mathrm{e}}^{2x + 1} - 2 = 0$$
4.  $$ {\mathrm{e}}^{2 x} + 2 {\mathrm{e}}^x - 3 = 0 $$

## Exercice 5

On considère l’intégrale

$$I = \int_0^2 (2x+1) \, \mathrm{d} x $$

1. Visualiser à l’aide de la courbe d’une fonction une surface d’aire $$I$$.
2. Calculer $$I$$.

## Exercice 6

On se place dans le plan muni d’un repère orthonormale $${(O, \vec {\!\!\imath}, \vec {\!\!\jmath})}$$.

1. Représenter la surface $$\mathcal{D}$$ délimitée par la courbe d’équation $$y = x^2 - x - 3$$ et les droites d’équations $$y = 2 x - 3$$, $$x = 1$$ et $$x = 2$$.
2. Déterminer l’aire de $$\mathcal{D}$$.

<script type="text/javascript">
    $(document).ready(function() {
        $("body").append("Bonjour");
        $("script[type='math/tex']").replaceWith(function(){
            var tex = $(this).text();
            return "<span class=\"inline-equation\">" + 
                katex.renderToString(tex) +
                "</span>";
        });
        $("script[type='math/tex; mode=display']").replaceWith(
        function(){
            var tex = $(this).text();
            return "<div class=\"equation\">" + 
                katex.renderToString("\\displaystyle "+tex) +
                "</div>";
        });
        $("body").append("Au revoir");
    });
</script>
