100 % de revue de code
======================


Bonjour, blablabla

Aujourd'hui, suite à la conf d'Anthony et Julien, je vais vous donner un retour d'expérience sur la manière dont nous pratiquons les revues de code chez TEA… puisque vous avez bien compris que les revues de code, c'est bien ! Et donc, comment on a fait pour en arriver à 100 % de revue de code. 

Je vais commencer par vous présenter le contexte. TEA, c'est une startup lyonnaise où je suis arrivée il y a un an et demi. Nous avons monté une plateforme de logistique autour du livre numérique, et on propose aussi des magasins web intégrés dans les liseuses, des applications d'achat et de lecture d'ebooks, ou des catalogues prêts à intégrer dans un site. L'idée, comme l'indique le nom de l'entreprise, c'est de proposer une alternative ouverte aux géants de l'ebook comme Amazon ou kobo.

L'environnement technique est… comment dire ? Touffu. Nous avons une plateforme logistique et des sites de e-commerce écrits en PHP, des applications Android écrites en java, des scripts d'import-exports en bash et en SQL… et progressivement, on écrit de plus en plus d'applications en Ruby On Rails pour remplacer certaines briques en PHP. Évidemment, les parties front utilisent lourdement HTML, CSS et Javascript, avec parfois des contraintes spécifiques au matériel "liseuse"…

Comment travaille-t-on sur ces logiciels divers et variés ?
Déjà, on versionne tout sous git. Tout petits, on a pris l'habitude de créer des branches de feature à chaque fois, et vous allez voir que ça va être intéressant pour la suite.
On fait du déploiement continu. Ça veut dire qu'une à plusieurs fois par jour, quand c'est tout testé et vérifié, on déploie notre code en prod. Sauf le vendredi. #estcequonmetenprodaujourdhui #non

Nous sommes une équipe de 6 développeurs. C'est trop peu pour dire que l'un ou l'autre doit être spécialisé dans une techno en particulier. On peut être amené à travailler sur n'importe quelle partie du projet, donc on doit maîtriser à peu près tout. Même si on aime forcément plus certaines parties du code que d'autres. #css #oh #css

C'est pour ça qu'on a décidé de faire des revues de code entre nous : les revues de code nous permettent de partager ce qu'on sait avec les autres, d'uniformiser les pratiques de développement, de valoriser les bonnes pratiques… Je précise que nous faisons de la "peer review" en anglais : de la revue de code par les pairs. Il ne s'agit pas de faire relire le code par un super développeur ou par un directeur technique, mais bien de faire relire le code par un collègue développeur.

Tout ça pour ça ? Et donc, comment on les pratique, ces revues de code ?

Les revues de code en présentiel
--------------------------------

Quand je suis arrivée chez TEA, il y avait 4 développeurs, et, comme maintenant, on travaillait en Scrum, sur des sprints de 2 semaines.

On avait donc des "user stories" qui sont des fonctionnalités "macro", chacune découpée en "tâches", qui sont des unités de développement plus petites. La revue de code se passait en gros à chaque fois qu'on finissait une tâche. On appelait ça "croiser".

Voici comment ça se passait : je finissais ma tâche, et je lançais à la cantonnade « coucou ! Quelqu'un est dispo pour croiser ? »

Un des 3 autres arrêtait ce qu'il était en train de faire et venait s'asseoir à côté de moi. J'expliquais ce que j'avais fait, je lui montrais des morceaux de code, on discutait, si une des bonnes pratiques était vraiment piétinée, le collègue le relevait. Si je manquais quelque chose, si j'avais réinventé la roue… ça se corrigeait… à condition que ça appartienne au code que j'avais montré au collègue.

C'était bien, comme technique ! Déjà, ça faisait un peu de sociabilité. On n'était pas enfermé avec notre PC, on parlait un peu. On transformait notre code en mots, en phrases en français. Quand on faisait ça, il y avait un petit effet "canard en plastique" : d'expliquer comme ça le code avec des mots, à voix haute, ça donnait parfois la petite étincelle pour détecter des grosses bêtises. En plus, le collègue avait souvent des remarques bien intéressantes qui amélioraient la qualité du truc.
 
Par exemple… TODO

Par contre, ça avait quelques inconvénients. Déjà, on ne croisait qu'à deux, toute l'équipe n'était pas impliquée… en général. Donc l'information ne circulait pas forcément dans toute l'équipe.

Ensuite, on ne croisait pas sur la totalité du code modifié, mais seulement sur les parties qu'on trouvait intéressantes au moment de la revue. Ça peut être bien si ça peut éviter de relire toutes les modifs inintéressantes (quand on ajoute des getters et des setters…) ou celles des fichiers de config, mais… par exemple, les modifs de CSS ne sont pas forcément considérées comme "intéressantes" par mes collègues, car ce sont des modifs "juste cosmétiques"… Sauf que j'ai souvent mon mot à dire sur un positionnement ou sur un sélecteur ou sur l'accessibilité !

TODO inconvénient : ça pousse quelqu'un d'autre à s'interrompre dans son travail

Et enfin, dernier désavantage et non des moindres : parfois, on ne croisait pas. On oubliait, ou alors il n'y avait personne de dispo au moment où on avait fini… Et petit à petit, on a perdu l'habitude de « croiser ». Et donc notre pourcentage de code revu avant mise en prod… chutait… inéluctablement.

Comment on a évité le naufrage ?

La revue de code par _pull request_
-----------------------------------

Le naufrage de la revue de code a été évité grâce à un petit nouveau qui est arrivé et qui a demandé :

« hey ! Vous faites pas des PR pour _tout_ ? »

et nous, on a répondu :

« oui, tiens, pourquoi ? »
« on pourrait essayer ? Ça coûte rien, on est déjà sur github ! »
« yeah ! faisons ça ! »
« youpi ! »

Nous avons la chance d'être autonomes dans notre organisation de travail, ou au moins d'avoir des managers qui sont preneurs de tout changement qui nous permet de coder mieux.

C'est comme ça qu'on a commencé à parler de pull request. Qu'est-ce que c'est, une pull request ? Ça n'a rien à voir avec la blague bête « tire mon doigt ». Non.

Une pull request, c'est tout simplement une branche qui demande gentiment à être fusionnée dans le master. Comme on bossait déjà par branche de feature, il n'y a pas eu besoin de changer radicalement nos habitudes de dev. Maintenant, au lieu de demander à la cantonnade « coucou, quelqu'un veut croiser ? », on pousse notre branche sur Github, et on clique sur "create pull request".

Là, il y a une vision des modifs, assez sympa, et on peut commenter ligne par ligne, ou l'ensemble. Les échanges qu'on a sont souvent intéressants…

par exemple, voici du JS…
tiens, du PHP…
ici, du css
ici, du mysql
ici, une faute d'orthographe dans un commentaire
ici, on a évité un bug en prod
… et ici, on a mis des gifs…
… et là aussi
… bon…
… voilà

Le fait de travailler comme ça en pull request a beaucoup d'avantages (outre les gifs).
- on apprend, la connaissance circule : les codeurs apprennent beaucoup grâce aux remarques des relecteurs. Souvent des petits détails (classList, astuces CSS), parfois des trucs plus conséquents (utilisations des Generator en PHP 5.5 par exemple)
- comme les développeurs apprennent, la qualité du code augmente : non seulement on tend à écrire du code plus propre parce qu'on sait qu'on va être relu, mais aussi, on "oublie" difficilement d'ajouter des tests automatisés si on sait que les collègues vont nous tomber dessus à la relecture.
- l'information (≠ connaissance) circule aussi : on sait quelles fonctionnalités sont en prod (c'est celles qui sont mergées dans le master, a priori…)… et on a une vague idée de l'explication de ce bug bizarre qui pourrit la prod depuis 20 minutes.
- on a un historique lisible (un jolibô arbre des commits, certes — c'est important -) mais aussi exploitable : en revenant de deux semaines de vacances, on peut relire les PR qui ont été effectuées pendant les vacances, ça donne une idée de ce qui s'est passé, des problèmes qui sont survenus, etc..

exemples

Bon, les PR c'est chouette… mais ce n'est pas non plus le pays des bisounours sur des poneys. Il y a aussi des inconvénients.

- d'une part, il ne faut pas croire que de faire relire le code va vous empêcher de déployer des boulettes en prod. Voici la dernière boulette qui a été déployée. Vous trouvez que ça a l'air d'une boulette ? Nous non plus, on n'avait pas l'impression.
- ensuite, ça demande quand même pas mal de temps et d'énergie de bien relire une PR. Ça peut avoir deux types de conséquences. Soit les relecteurs vont s'arrêter de bosser très longtemps pour bien relire votre PR… soit ils vont mal la relire et laisser passer des bêtises. Je vous laisse deviner ce qui s'est passé sur cette PR-là…
- et finalement, la revue de code asynchrone par écrit, c'est bien, mais parfois c'est plus simple d'expliquer quelque chose à l'oral en s'asseyant l'un à côté de l'autre et en discutant 5 minutes.

Voilà, j'ai à peu près fait le tour du pour et du contre. Maintenant, si je donne cette conf, c'est pour que vous aussi, vous vous mettiez à relire votre code et celui de vos collègues.

Je vous rappelle mes arguments ? La revue de code, ça rend le code meilleur. Vous avez moins de bugs. Vous apprenez. Vous êtes heureux.

Concrètement, comment pouvez-vous faire ?

Vous avez git, mais pas de github : il y a des outils libres, open source, qui permettent de faire de la code review, que vous pouvez installer sur un serveur en local chez vous. Par exemple, vous avez Crew, développé par des gens bien, à Lyon, qui tourne en PHP avec une petite base MySQL.

Vous avez pas git, mais un gestionnaire de version quand même : il y a des outils qui permettent de faire de la revue de code avec SVN, bazaar, CVS… (Mais git reste mon petit préféré choupi.) http://en.wikipedia.org/wiki/List_of_tools_for_code_review
Le principe est toujours le même.

Vous n'avez pas de gestionnaire de version : installez git ! MAINTENANT

--------

Code reviews turn individual knowledge into distributed knowledge.

http://en.wikipedia.org/wiki/List_of_tools_for_code_review