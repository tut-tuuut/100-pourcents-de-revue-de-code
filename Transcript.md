100 % de revue de code
======================


Bonjour, blablabla

Aujourd'hui, suite à la conf d'Anthony et Julien, je vais vous donner un retour d'expérience sur la manière dont nous pratiquons les revues de code chez TEA… puisque vous avez bien compris que les revues de code, c'est bien ! Et donc, comment on a fait pour en arriver à 100 % de revue de code. 

Je vais commencer par vous présenter le contexte. TEA, c'est une startup lyonnaise où je suis arrivée il y a un an et demi. On fait des trucs autour du livre numérique, c'est chouette.

L'environnement technique est… comment dire ? Touffu. Nous avons du PHP, du Java, du Bash, du SQL, du Ruby… et évidemment, du HTML, du CSS et du JS. Tout ça en responsive sur des écrans à encre électronique, s'il vous plaît.

Niveau méthodes de travail, comment est-ce qu'on fonctionne ?
Déjà, on versionne tout sous git. Tout. Tout petits, on a pris l'habitude de créer des branches de feature à chaque fois, et vous allez voir que ça va être intéressant pour la suite.
On fait du déploiement continu, avec capistrano. Ça veut dire qu'une à plusieurs fois par jour, quand c'est tout testé et vérifié, on déploie notre code en prod. Sauf le vendredi. #estcequonmetenprodaujourdhui #non
Et finalement, on travaille en scrum, sur des sprints de 2 semaines.
pourquoi c'est intéressant

Nous sommes une équipe de 6 développeurs. C'est suffisant pour qu'on puisse se permettre d'avoir des préférences pour l'une ou l'autre des nombreuses briques de l'archi… mais trop peu pour qu'on soit vraiment spécialisés. On est obligés d'être polyvalents et de partager la connaissance le plus possible. Sinon, le bus factor explose… (image de bus)

C'est pour ça qu'on a décidé de pratiquer des revues de code entre nous : ça nous permet de partager ce qu'on sait avec les autres, d'uniformiser les pratiques de développement, de valoriser les bonnes pratiques… Je précise que nous faisons de la "peer review" en anglais : de la revue de code par les pairs. Il ne s'agit pas de faire relire le code par un super développeur ou par un directeur technique, parce que notre DT est déjà assez occupé comme ça. Mais bien de faire relire le code par un collègue développeur.

Tout ça pour ça ? Et donc, comment on les pratique, ces revues de code ?

Les revues de code en présentiel
--------------------------------

Avant, après avoir fini une tâche, je lançais à la cantonnade « coucou ! Quelqu'un est dispo pour croiser ? »

Un des 3 autres arrêtait ce qu'il était en train de faire et venait s'asseoir à côté de moi. J'expliquais ce que j'avais fait, je lui montrais des morceaux de code, on discutait. Si une des bonnes pratiques était vraiment piétinée, le collègue le relevait. Si je manquais quelque chose, si j'avais réinventé la roue… ça se corrigeait… Ça durait de cinq minutes à une petite demi-heure.

C'était bien, comme technique ! Déjà, ça fait socialiser un peu, c'est pas mal. On transformait notre code en mots, en phrases en français. Expliquer le code comme ça, ça avait un petit effet "canard en plastique" : ça donnait parfois la petite étincelle pour détecter des grosses bêtises. Les échanges avec le collègue étaient bien aussi.

Par contre, ça avait quelques inconvénients. Pour résumer, on ne faisait pas une revue de tout le code, seulement de ce qui nous intéressait… Ensuite on le faisait seulement quand on y pensait… et on y pensait pas toujours. Et puis interrompre les collègues, c'est pénible. Donc on le faisait de moins en moins…

La revue de code par _pull request_
-----------------------------------

Le naufrage de la revue de code a été évité grâce à un petit nouveau (enfin, plutôt grand, le petit nouveau) qui est arrivé et qui a demandé :

« hey ! Vous faites pas des pull request pour _tout_ ? »

et nous, on a répondu :

« oui, tiens, pourquoi ? »
« on pourrait essayer ? Ça coûte rien, on est déjà sur github ! »
« yeah ! faisons ça ! »
« youpi ! »

C'est comme ça qu'on a commencé à parler de pull request. (Ouais, on aime bien essayer des nouvelles choses dans nos méthodes de travail — et les chefs nous laissent faire, c'est cool !)

Qu'est-ce que c'est, une pull request ? Ça n'a rien à voir avec la blague bête « tire mon doigt ». Non.

Une pull request, c'est tout simplement une branche qui demande gentiment à être fusionnée dans le master.

Comme on bossait déjà par branche de feature, il n'y a pas eu besoin de changer radicalement nos habitudes de dev. Maintenant, au lieu de demander à la cantonnade « coucou, quelqu'un veut croiser ? », on pousse notre branche sur Github, et on clique sur "create pull request".

Là, il y a une vision des modifs, assez sympa, et on peut commenter ligne par ligne, ou l'ensemble. Les échanges qu'on a sont souvent intéressants…

par exemple, voici du JS…
tiens, du PHP 5.5…
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
- l'information (≠ connaissance) circule aussi : on sait quelles fonctionnalités vont passer en prod (c'est celles qui sont mergées dans le master, a priori…)… et on a une vague idée de l'explication de ce bug bizarre qui pourrit la prod depuis 20 minutes.
- on a un historique lisible (un jolibô arbre des commits, certes — c'est important -) mais aussi exploitable : en revenant de deux semaines de vacances, on peut relire les PR qui ont été effectuées pendant les vacances, ça donne une idée de ce qui s'est passé, des problèmes qui sont survenus, etc..

exemples :

Bon, les PR c'est chouette… mais ce n'est pas non plus le pays des bisounours sur des poneys. Il y a aussi des inconvénients.

- d'une part, il ne faut pas croire que de faire relire le code va vous empêcher de déployer des boulettes en prod. Voici la dernière boulette qui a été déployée. Vous trouvez que ça a l'air d'une boulette ? Nous non plus, on n'avait pas l'impression. Il faut quand meme des tests automatisés.
- ensuite, ça demande quand même pas mal de temps et d'énergie de bien relire une PR. Ça peut avoir deux types de conséquences. Soit les relecteurs vont s'arrêter de bosser très longtemps pour bien relire votre PR… soit ils vont mal la relire et laisser passer des bêtises. Je vous laisse deviner ce qui s'est passé sur cette PR-là…
- et finalement, la revue de code asynchrone par écrit, c'est bien, mais parfois c'est plus simple d'expliquer quelque chose à l'oral en s'asseyant l'un à côté de l'autre et en discutant 5 minutes.

Voilà, j'ai à peu près fait le tour du pour et du contre. Maintenant, si je donne cette conf, c'est pour que vous aussi, vous vous mettiez à relire votre code et celui de vos collègues.

Je vous rappelle mes arguments ? La revue de code, ça rend le code meilleur. Vous avez moins de bugs. Vous apprenez. Vous êtes heureux. Et c'est pas cher.

Concrètement, comment pouvez-vous faire ?

Vous avez git, mais pas de github : il y a des outils libres, open source, qui permettent de faire de la code review, que vous pouvez installer sur un serveur en local chez vous. Par exemple, vous avez Crew, développé par des gens bien, à Lyon, qui tourne en PHP avec une petite base MySQL.

Vous avez pas git, mais un gestionnaire de version quand même : il y a des outils qui permettent de faire de la revue de code avec SVN, bazaar, CVS… (Mais git reste mon petit préféré choupi.) http://en.wikipedia.org/wiki/List_of_tools_for_code_review
Le principe est toujours le même.

Vous n'avez pas de gestionnaire de version : installez git ! MAINTENANT

Vous avez un chef qui pense que ça ne sert à rien de se fatiguer pour si peu : demandez-lui quand même, expliquez que ça ne coûte pas grand-chose, et que ça apporte beaucoup. Apportez une idée de solution technique. Proposez d'expérimenter pendant un mois.




Allez-y ! Revoyez !
Et racontez-moi vos expériences. :)

Agnès H.
@tut_tuuut — http://tut-tuuut.github.io



--------

Code reviews turn individual knowledge into distributed knowledge.

http://en.wikipedia.org/wiki/List_of_tools_for_code_review