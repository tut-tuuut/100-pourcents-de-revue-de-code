100 % de revue de code
======================


Bonjour, blablabla

Aujourd'hui, suite à la conf de Truc et Machin, je vais vous donner un retour d'expérience sur la manière dont nous pratiquons les revues de code chez TEA… puisque vous avez bien compris que les revues de code, c'est bien ! 

TEA, c'est une startup lyonnaise où je suis arrivée il y a un an et demi. Nous avons monté une plateforme de logistique autour du livre numérique. Notre objectif est de fournir une alternative ouverte aux géants de l'ebook comme Amazon ou kobo.

L'environnement technique est… comment dire ? Touffu. Nous avons une plateforme logistique et des sites de e-commerce écrits en PHP, des applications Android écrites en java, des scripts d'import-exports en bash et en SQL… et progressivement, on écrit de plus en plus d'applications en Ruby On Rails pour remplacer certaines briques en PHP. Évidemment, les briques front utilisent lourdement HTML, CSS et Javascript, avec parfois des contraintes spécifiques au matériel "liseuse"…

Nous sommes une équipe de 6 développeurs. C'est trop peu pour dire que l'un ou l'autre est spécialisé dans une techno en particulier. Il y a donc beaucoup de langages à maîtriser, ou au moins à connaître, en même temps. Mais nous ne nions pas que nous avons chacun plus d'affinités avec l'une ou l'autre brique.

C'est pour ça qu'on a décidé de faire des revues de code entre nous : 

Les revues de code en présentiel
--------------------------------

Quand je suis arrivée chez TEA, il y avait 4 développeurs, et, comme maintenant, on travaillait en Scrum, sur des sprints de 2 semaines.

On avait donc des "user stories" qui sont des fonctionnalités "macro", chacune découpée en "tâches", qui sont des unités de développement plus petites. La revue de code se passait en gros à chaque fois qu'on finissait une tâche. On appelait ça "croiser".

Voici comment ça se passait : je finissais ma tâche, et je lançais à la cantonnade « coucou ! Quelqu'un est dispo pour croiser ? »

Un des 3 autres arrêtait ce qu'il était en train de faire et venait s'asseoir à côté de moi. J'expliquais ce que j'avais fait, je lui montrais des morceaux de code, on discutait, si une des bonnes pratiques était vraiment piétinée, le collègue le relevait. Si je manquais quelque chose, utilisé une solution trop compliquée, réinventé la roue… ça se corrigeait si ça appartenait au code que j'avais montré.

C'était bien, comme technique ! Déjà, ça faisait un peu de sociabilité. Il y avait un petit effet "canard en plastique" : d'expliquer le code avec des mots, à voix haute, ça donnait parfois la petite étincelle pour détecter des grosses bêtises.

Par contre, ça avait quelques inconvénients. Déjà, on ne croisait qu'à deux, toute l'équipe n'était pas impliquée… en général. Donc l'information ne circulait pas forcément dans toute l'équipe.
Ensuite, on ne croisait pas sur la totalité du code modifié, mais seulement sur les parties qu'on trouvait intéressantes au moment de coder. Ça peut être bien si ça peut éviter de relire toutes les modifs "cosmétiques", par exemple, mais… par exemple, les modifs de CSS ne sont pas forcément considérées comme "intéressantes" par mes collègues, alors que j'ai souvent mon mot à dire sur un positionnement ou sur un sélecteur !


--------

Code reviews turn individual knowledge into distributed knowledge.