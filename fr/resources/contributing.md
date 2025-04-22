---
layout: page
title: Contribuer à Express
description: Découvrez comment contribuer à Express.js, y compris des lignes directrices pour signaler les problèmes, soumettre des demandes d'ajout, devenir collaborateur et comprendre les politiques de sécurité.
menu: resources
lang: fr
redirect_from: ""
---

# Contribuer à Express

### Vous cherchez à contribuer à Expressjs.com? Click [here](#expressjs-website-contributing).

Express et les autres projets de l'organisation [expressjs sur GitHub](https://github.com/expressjs) sont des projets de la [Fondation OpenJs](https://openjsf.org/).
Ces projets sont régis par les politiques générales et les lignes directrices de la Fondation Node.js ainsi que par les lignes directrices supplémentaires ci-dessous.

- (#technical-committee)
- [Guide de contribution de la communauté](#community-contributing-guide)
- [Guide du collaborateur](#collaborators-guide)
- [Politiques et procédures de sécurité] (#security-policies-and-procedures)

## Comité technique

Le comité technique Express est composé de membres actifs du projet et guide le développement et la maintenance du projet Express. Pour plus d'informations, voir [Communauté expresse - Comité Technique] (community.html#technical-committee).

## Guide de contribution de la communauté

<!-- SRC: expressjs/express Contributing.md -->

L'objectif de ce document est de créer un processus de contribution qui :

- Encourage les nouvelles contributions.
- Encourage les contributeurs à rester impliqués.
- Évite les processus inutiles et la bureaucratie dans la mesure du possible.
- Creates a transparent decision making process that makes it clear how
 contributors can be involved in decision making.

### Vocabulaire

- Un **Contributeur** est toute personne qui crée ou commente sur un ticket ou une demande de fusion.
- Un **committer** est un sous-ensemble de contributeurs qui ont reçu un accès en écriture au référentiel.
- Un **Capitaine du projet** est le responsable principal d'un dépôt.
- Un **TC (Comité Technique)** est un groupe d'auteurs représentant l'expertise technique
 requise pour résoudre les litiges rares.
- Un **Triager** est un sous-ensemble de contributeurs qui ont reçu un accès triage au dépôt.

### Problèmes de journalisation

Enregistrez un problème pour toute question ou problème que vous pourriez avoir. En cas de doute, enregistrez un problème et
toute politique supplémentaire sur ce qu'il faut inclure sera fournie dans les réponses. La seule exception
est la divulgation de sécurité qui doit être envoyée en privé.

Les auteurs peuvent vous diriger vers un autre référentiel, demander des clarifications supplémentaires et
ajouter des métadonnées appropriées avant que le problème ne soit résolu.

Soyez courtois et respectueux. Chaque participant doit suivre le Code de conduite du projet
.

### Contributions

Toute modification des ressources de ce dépôt doit passer par des demandes de fusion. Ceci s'applique à tous les changements
à la documentation, code, fichiers binaires, etc. Even long term committers and TC members must use
pull requests.

Aucune pull request ne peut être fusionnée sans être revue.

For non-trivial contributions, pull requests should sit for at least 36 hours to ensure that
contributors in other timezones have time to review. Il convient également de prendre en considération les week-ends
et autres périodes de vacances pour s'assurer que tous les commutateurs actifs ont un temps raisonnable à
pour participer au processus de discussion et de révision s'ils le souhaitent.

La valeur par défaut pour chaque contribution est qu'elle est acceptée une fois qu'aucun validateur n'a une objection.
Lors d'un examen, les commutateurs peuvent également demander qu'un contributeur spécifique qui est le plus versé dans une zone
particulière donne un "LGTM" avant que la PR puisse être fusionnée. Il n'y a pas de processus supplémentaire de "déconnexion"
pour les contributions à la terre. Once all issues brought by committers are addressed it can
be landed by any committer.

In the case of an objection being raised in a pull request by another committer, all involved
committers should seek to arrive at a consensus by way of addressing concerns being expressed
by discussion, compromise on the proposed change, or withdrawal of the proposed change.

Si une contribution est controversée et que les auteurs ne peuvent pas s'entendre sur la façon de l'amener à la terre
ou si elle doit atterrir, alors elle devrait être escaladée vers le TC. Les membres de TC devraient régulièrement
discuter des contributions en attente afin de trouver une résolution. It is expected that only a
small minority of issues be brought to the TC for resolution and that discussion and
compromise among committers be the default resolution mechanism.

### Devenir un Triager

« N'importe qui peut devenir un triager! » En savoir plus sur le processus de triagerie en
[document sur le processus de triage](https://github.com/expressjs/express/blob/master/Triager-Guide.md).

Actuellement, tout [membre de l'organisme] (https://github.com/orgs/expressjs/people) existant peut nommer
un nouveau triager. Si vous souhaitez devenir un triager, notre meilleur conseil est de participer activement
à la communauté en aidant à trier les problèmes et les pull requests. De plus, nous recommandons à
de participer à d'autres activités de la communauté, comme assister aux réunions de TC et participer aux discussions de Slack
. If you feel ready and have been helping triage some issues, reach out to an active member of the organization to ask if they'd
be willing to support you. S'ils sont d'accord, ils peuvent créer une pull request pour formaliser votre candidature. En cas d'opposition à la mise en candidature, l'équipe de triage est chargée de travailler avec les personnes impliquées et de trouver une solution.

Vous pouvez également contacter n'importe lequel des [membres de l'organisme](https://github.com/orgs/expressjs/people)
si vous avez des questions ou si vous avez besoin de conseils.

### Devenir Commun

All contributors who have landed significant and valuable contributions should be onboarded in a timely manner,
and added as a committer, and be given write access to the repository.

Les développeurs doivent suivre cette politique et continuer à envoyer des pull requests, passer en revue
correctement et faire fusionner leurs pull requests par d'autres committers.

### Processus TC

Le TC utilise un processus de « recherche de consensus » pour les questions qui sont escaladées vers le TC.
Le groupe tente de trouver une résolution qui n'a aucune objection ouverte parmi les membres de TC.
Si un consensus ne peut pas être atteint qui n'a aucune objection, alors une majorité gagne le vote
est appelée. On s'attend également à ce que la majorité des décisions prises par TC passent par
un processus de recherche de consensus et que le vote ne soit utilisé qu'en dernier recours.

La résolution peut impliquer de renvoyer le problème aux capitaines du projet avec des suggestions sur
sur la façon de progresser vers un consensus. Il n'est pas prévu qu'une réunion du TC
résoudra tous les problèmes à son ordre du jour durant cette réunion et préférera peut-être continuer
la discussion qui se déroule parmi les capitaines du projet.

Les membres peuvent être ajoutés au TC à tout moment. Any TC member can nominate another committer
to the TC and the TC uses its standard consensus seeking process to evaluate whether or
not to add this new member. The TC will consist of a minimum of 3 active members and a
maximum of 10. If the TC should drop below 5 members the active TC members should nominate
someone new. If a TC member is stepping down, they are encouraged (but not required) to
nominate someone to take their place.

Les membres de TC seront ajoutés en tant qu'administrateur sur les organes Github, les organisations npm et d'autres ressources comme
nécessaire pour être efficace dans le rôle.

To remain "active" a TC member should have participation within the last 12 months and miss
no more than six consecutive TC meetings. Our goal is to increase participation, not punish
people for any lack of participation, this guideline should be only be used as such
(replace an inactive member with a new active one, for example). Les membres qui ne rencontrent pas cette
devraient se retirer. Si un membre de TC ne se déconnecte pas, un problème peut être ouvert dans le dépôt des discussions
pour le déplacer vers un statut inactif. Les membres TC qui se déconnectent ou sont retirés à cause de l'inactivité
seront transférés vers un statut inactif.

Inactive status members can become active members by self nomination if the TC is not already
larger than the maximum of 10. They will also be given preference if, while at max size, an
active member steps down.

### Capitaines du projet

Le TC Express peut désigner des capitaines pour des projets individuels ou des repos dans les organisations
. These captains are responsible for being the primary
day-to-day maintainers of the repo on a technical and community front.
Les capitaines du dépôt sont dotés de droits de propriété de dépôt et de publication de paquets.
En cas de conflit, en particulier sur les sujets qui affectent le projet Express
en général, les capitaines sont responsables de l'élever jusqu'à la TC et de conduire
à résoudre ces conflits. Captains are also responsible for making sure
community members follow the community guidelines, maintaining the repo
and the published package, as well as in providing user support.

Tout comme les membres de TC, les capitaines Repo sont un sous-ensemble de commetteurs.

Pour devenir capitaine d'un projet, le candidat devrait participer à ce projet
pendant au moins 6 mois en tant qu'entrepreneur avant la demande. Ils devraient avoir
aidé avec des contributions de code ainsi que des problèmes de triage. Ils sont également requis pour
avoir 2FA activé sur leurs comptes GitHub et npm.

Tout membre de TC ou capitaine existant sur le **même** repo peut nommer un autre committer
au rôle de capitaine. Pour ce faire, ils doivent soumettre une PR à ce document, mise à jour de la section
**Active Project Captains** (tout en maintenant l'ordre de tri) avec le nom du projet
le gestionnaire GitHub du candidat et son nom d'utilisateur npm (si différent).

- Les dépôts peuvent avoir autant de capitaines que de sens pour la portée du travail.
- Un membre de TC ou un capitaine de dépôt existant **sur le même projet** peut nommer un nouveau capitaine.
 Les capitaines Repo d'autres projets ne devraient pas nommer de capitaines pour un projet différent.

La PR nécessitera au moins 2 approbations de la part des membres de TC et 2 semaines de temps de attente pour autoriser
pour commentaires et/ou dissidents.  Lorsque la PR est fusionnée, un membre de TC les ajoutera aux groupes GitHub/npm propres à
.

#### Projets actifs et capitaines

- [`expressjs/badgeboard`](https://github.com/expressjs/badgeboard): @wesleytodd
- [`expressjs/basic-auth-connect`](https://github.com/expressjs/basic-auth-connect): @ulisesGascon
- [`expressjs/body-parser`](https://github.com/expressjs/body-parser): @wesleytodd, @jonchurch, @ulisesGascon
- [`expressjs/compression`](https://github.com/expressjs/compression): @ulisesGascon
- [`expressjs/connect-multiparty`](https://github.com/expressjs/connect-multiparty): @ulisesGascon
- [`expressjs/cookie-parser`](https://github.com/expressjs/cookie-parser): @wesleytodd, @UlisesGascon
- [`expressjs/cookie-session`](https://github.com/expressjs/cookie-session): @ulisesGascon
- [`expressjs/cors`](https://github.com/expressjs/cors): @jonchurch, @ulisesGascon
- [`expressjs/discussions`](https://github.com/expressjs/discussions): @wesleytodd
- [`expressjs/errorhandler`](https://github.com/expressjs/errorhandler): @ulisesGascon
- [`expressjs/express-paginate`](https://github.com/expressjs/express-paginate): @ulisesGascon
- [`expressjs/express`](https://github.com/expressjs/express): @wesleytodd, @ulisesGascon
- [`expressjs/expressjs.com`](https://github.com/expressjs/expressjs.com): @crandmck, @jonchurch, @bjohansebas
- [`expressjs/flash`](https://github.com/expressjs/flash): @ulisesGascon
- [`expressjs/generator`](https://github.com/expressjs/generator): @wesleytodd
- [`expressjs/method-override`](https://github.com/expressjs/method-override): @ulisesGascon
- [`expressjs/morgan`](https://github.com/expressjs/morgan): @jonchurch, @ulisesGascon
- [`expressjs/multer`](https://github.com/expressjs/multer): @LinusU, @ulisesGascon
- [`expressjs/response-time`](https://github.com/expressjs/response-time): @UlisesGascon
- [`expressjs/serve-favicon`](https://github.com/expressjs/serve-favicon): @ulisesGascon
- [`expressjs/serve-index`](https://github.com/expressjs/serve-index): @ulisesGascon
- [`expressjs/serve-static`](https://github.com/expressjs/serve-static): @ulisesGascon
- [`expressjs/session`](https://github.com/expressjs/session): @ulisesGascon
- [`expressjs/statusboard`](https://github.com/expressjs/statusboard): @wesleytodd
- [`expressjs/timeout`](https://github.com/expressjs/timeout): @ulisesGascon
- [`expressjs/vhost`](https://github.com/expressjs/vhost): @ulisesGascon
- [`jshttp/accepts`](https://github.com/jshttp/accepts): @blakeembrey
- [`jshttp/basic-auth`](https://github.com/jshttp/basic-auth): @blakeembrey
- [`jshttp/compressible`](https://github.com/jshttp/compressible): @blakeembrey
- [`jshttp/content-disposition`](https://github.com/jshttp/content-disposition): @blakeembrey
- [`jshttp/content-type`](https://github.com/jshttp/content-type): @blakeembrey
- [`jshttp/cookie`](https://github.com/jshttp/cookie): @blakeembrey
- [`jshttp/etag`](https://github.com/jshttp/etag): @blakeembrey
- [`jshttp/forwarded`](https://github.com/jshttp/forwarded): @blakeembrey
- [`jshttp/fresh`](https://github.com/jshttp/fresh): @blakeembrey
- [`jshttp/http-assert`](https://github.com/jshttp/http-assert): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/http-errors`](https://github.com/jshttp/http-errors): @wesleytodd, @jonchurch, @ulisesGascon
- [`jshttp/media-typer`](https://github.com/jshttp/media-typer): @blakeembrey
- [`jshttp/methods`](https://github.com/jshttp/methods): @blakeembrey
- [`jshttp/mime-db`](https://github.com/jshttp/mime-db): @blakeembrey, @UlisesGascon
- [`jshttp/mime-types`](https://github.com/jshttp/mime-types): @blakeembrey, @UlisesGascon
- [`jshttp/negotiator`](https://github.com/jshttp/negotiator): @blakeembrey
- [`jshttp/on-finished`](https://github.com/jshttp/on-finished): @wesleytodd, @ulisesGascon
- [`jshttp/on-headers`](https://github.com/jshttp/on-headers): @blakeembrey
- [`jshttp/proxy-addr`](https://github.com/jshttp/proxy-addr): @wesleytodd, @ulisesGascon
- [`jshttp/range-parser`](https://github.com/jshttp/range-parser): @blakeembrey
- [`jshttp/statuses`](https://github.com/jshttp/statuses): @blakeembrey
- [`jshttp/type-is`](https://github.com/jshttp/type-is): @blakeembrey
- [`jshttp/vary`](https://github.com/jshttp/vary): @blakeembrey
- [`pillarjs/cookies`](https://github.com/pillarjs/cookies): @blakeembrey
- [`pillarjs/csrf`](https://github.com/pillarjs/csrf): @ulisesGascon
- [`pillarjs/encodeurl`](https://github.com/pillarjs/encodeurl): @blakeembrey
- [`pillarjs/finalhandler`](https://github.com/pillarjs/finalhandler): @wesleytodd, @ulisesGascon
- [`pillarjs/hbs`](https://github.com/pillarjs/hbs): @ulisesGascon
- [`pillarjs/multiparty`](https://github.com/pillarjs/multiparty): @blakeembrey
- [`pillarjs/parseurl`](https://github.com/pillarjs/parseurl): @blakeembrey
- [`pillarjs/path-to-regexp`](https://github.com/pillarjs/path-to-regexp): @blakeembrey
- [`pillarjs/request`](https://github.com/pillarjs/request): @wesleytodd
- [`pillarjs/resolve-path`](https://github.com/pillarjs/resolve-path): @blakeembrey
- [`pillarjs/router`](https://github.com/pillarjs/router): @wesleytodd, @ulisesGascon
- [`pillarjs/send`](https://github.com/pillarjs/send): @blakeembrey
- [`pillarjs/understanding-csrf`](https://github.com/pillarjs/understanding-csrf): @ulisesGascon

#### Capitaine de l'initiative actuelle

- Équipe de triage [ref](https://github.com/expressjs/discussions/issues/227) : @UlisesGascon

### Certificat d'origine du développeur 1.1

```text
By making a contribution to this project, I certify that:

 (a) The contribution was created in whole or in part by me and I
     have the right to submit it under the open source license
     indicated in the file; or

 (b) The contribution is based upon previous work that, to the best
     of my knowledge, is covered under an appropriate open source
     license and I have the right under that license to submit that
     work with modifications, whether created in whole or in part
     by me, under the same open source license (unless I am
     permitted to submit under a different license), as indicated
     in the file; or

 (c) The contribution was provided directly to me by some other
     person who certified (a), (b) or (c) and I have not modified
     it.

 (d) I understand and agree that this project and the contribution
     are public and that a record of the contribution (including all
     personal information I submit with it, including my sign-off) is
     maintained indefinitely and may be redistributed consistent with
     this project or the open source license(s) involved.
```

## Guide du collaborateur

<!-- SRC: expressjs/express Collaborator-Guide.md -->

### Problèmes de site web

Problèmes ouverts pour le site expressjs.com sur https://github.com/expressjs/expressjs.com.

### Contributions RP et Code

- Les tests doivent réussir.
- Suivez [JavaScript Standard Style] (https://standardjs.com/) et `npm run lint`.
- Si vous corrigez un bug, ajoutez un test.

### Branches

Utilisez la branche `master` pour les corrections de bugs ou le travail mineur qui est prévu pour le flux de version actuelformat@@0 de
.

Utilisez la branche nommée correspondante, par exemple `5.0`, pour tout ce qui est destiné à
une future version d'Express.

### Étapes pour contribuer

1. [Créer un problème](https://github.com/expressjs/express/issues/new) pour le bogue
 que vous voulez corriger ou la fonctionnalité que vous voulez ajouter.
2. Créez votre propre [fork](https://github.com/expressjs/express) sur GitHub, puis
 passez en revue votre fork.
3. Écrivez votre code dans votre copie locale. Il est bon de créer une branche pour
 à chaque nouveau problème sur lequel vous travaillez, mais pas obligatoire.
4. Pour exécuter la suite de test, installez d'abord les dépendances en exécutant `npm install`,
 puis exécutez `npm test`.
5. Ensure your code is linted by running `npm run lint` -- fix any issue you
 see listed.
6. Si les tests réussissent, vous pouvez valider vos modifications sur votre fork et ensuite créer
 une pull request à partir de là. Assurez-vous de faire référence à votre problème depuis la requête pull
 en incluant le numéro du problème, par exemple `#123`.

### Problèmes qui sont des questions

Nous fermerons généralement tous les problèmes ou questions vagues qui sont spécifiques à certaines applications
que vous écrivez. Veuillez vérifier la documentation et les autres références avant qu'
ne se déclenche heureux avec la publication d'un problème de question.

Des choses qui vous aideront à examiner votre problème de question :

- Code JS complet et exécutable.
- Description claire du problème ou comportement inattendu.
- Effacer la description du résultat attendu.
- Des mesures que vous avez prises pour le déboguer vous-même.

If you post a question and do not outline the above items or make it easy for
us to understand and reproduce your issue, it will be closed.

## Politiques et procédures de sécurité

<!-- SRC: expressjs/express Security.md -->

Ce document décrit les procédures de sécurité et les politiques générales du projet Express
.

- [Signaler un bogue](#reporting-a-bug)
- [Politique de divulgation] (#disclosure-policy)
- (#comments-on-this-policy)

### Signaler un bug

L'équipe Express et la communauté prennent tous les bogues de sécurité dans Express au sérieux.
Merci pour l'amélioration de la sécurité de Express. We appreciate your efforts and
responsible disclosure and will make every effort to acknowledge your
contributions.

Signalez des bugs de sécurité en envoyant un email à `express-security@lists.openjsf.org`.

To ensure the timely response to your report, please ensure that the entirety
of the report is contained within the email body and not solely behind a web
link or an attachment.

Le responsable principal reconnaîtra votre courriel dans les 48 heures. et enverra une réponse
plus détaillée dans les 48 heures indiquant les prochaines étapes dans la gestion de
votre rapport. Après la réponse initiale à votre rapport, l'équipe en charge de la sécurité
s'efforcera de vous tenir informé de la progression vers une résolution et une annonce
complète, et peut demander des renseignements supplémentaires ou des conseils.

Signaler des bugs de sécurité dans des modules tiers à la personne ou à l'équipe gérant
le module.

### Versions de pré-version

Les versions Alpha et Beta sont instables et **ne conviennent pas à une utilisation en production**.
Les vulnérabilités trouvées dans les pré-versions devraient être signalées selon la section [Signaler un bogue](#reporting-a-bug).
En raison de la nature instable de la branche, il n'est pas garanti que des correctifs seront publiés dans la prochaine pré-version.

### Politique de divulgation

Quand l'équipe de sécurité reçoit un rapport de bogue de sécurité, elle l'assignera à un gestionnaire
principal. Cette personne coordonnera le processus de correction et de libération,
avec les étapes suivantes :

- Confirmez le problème et déterminez les versions affectées.
- Code d'audit pour trouver des problèmes similaires potentiels.
- Préparez des correctifs pour toutes les versions encore en maintenance. These fixes will be
 released as fast as possible to npm.

### Le modèle de menace Express

Nous travaillons actuellement sur une nouvelle version du modèle de sécurité, la version la plus mise à jour peut être trouvée [here](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md)

### Commentaires sur cette politique

Si vous avez des suggestions sur la façon dont ce processus pourrait être amélioré, veuillez soumettre une demande de tirage
.

----

# Contribution à Expressjs.com {#expressjs-website-contributing}

<!-- LOCAL: expressjs/expressjs.com ../../CONTRIBUTING.md -->

### La documentation officielle du framework JS Express

Ceci est la documentation de contribution pour le site [Expressjs.com](https://github.com/expressjs/expressjs.com).

#### Besoin d'idées ? Il s'agit là de questions typiques.

1. **Website issues**:
 If you see anything on the site that could use a tune-up, think about how to fix it.

 - Problèmes d'affichage ou de taille d'écran
 - Problèmes de réactivité des téléphones mobiles
 - Fonctionnalités d'accessibilité manquantes ou cassées
 - Pannes du site web
 - Liens cassés
 - Amélioration de la structure de la page ou de l'interface utilisateur

2. **Problèmes de contenu** :
 Corrige tout ce qui concerne le contenu du site ou les fautes de frappe.
 - Erreurs orthographiques
 - Documentation JS incorrecte/obsolète
 - Contenu manquant

3. **Problèmes de traduction**: Corrige les erreurs de traduction ou contribue au nouveau contenu.
 - Corriger les erreurs d'orthographe
 - Corriger les mots mal traduits ou incorrects
 - Traduire un nouveau contenu

> **IMPORTANT:**
> Toutes les soumissions de traduction sont actuellement en pause. Voir ceci [notice](#notice-we-have-paused-all-translation-contributions) pour plus d'informations.

- Consultez la section [Traductions contributives] (#contributing-translations) ci-dessous pour un guide de contribution.

#### Vous voulez travailler sur un problème de carnet de commandes ?

Nous avons souvent des bugs ou des améliorations qui nécessitent du travail. Vous pouvez les trouver sous l'onglet [Issues tab](https://github.com/expressjs/expressjs.com/issues). Découvrez les balises pour trouver quelque chose qui vous convient.

#### Vous avez une idée? Vous avez trouvé un bug ?

Si vous avez trouvé un bug ou une faute de frappe, ou si vous avez une idée pour une amélioration, vous pouvez:

- Soumettez un [nouveau numéro](https://github.com/expressjs/expressjs.com/issues/new/choose) sur notre dépôt. Faites ceci pour des propositions plus importantes, ou si vous voulez discuter ou obtenir des commentaires d'abord.
- Make a [Github pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). Si vous avez déjà fait du travail et qu'il est prêt à y aller, n'hésitez pas à nous le faire savoir.

## Mise en route

Les étapes ci-dessous vous guideront tout au long du processus de contribution Expressjs.com.

#### Étape 1 : (OPTIONAL) Ouvrir un nouveau problème

Vous avez donc trouvé un problème que vous voulez corriger, ou une amélioration du site que vous voulez faire.

1. Si vous voulez obtenir des commentaires ou discuter, ouvrez une discussion [issue](https://github.com/expressjs/expressjs.com/issues/new/choose) avant de commencer à travailler. Ce n'est pas nécessaire, mais encouragé pour des propositions plus larges.
 - Même si nous encourageons fortement cette étape, ce n’est que pour les soumissions qui proposent des changements significatifs. Il nous aide à clarifier et à cibler le travail et à nous assurer qu'il s'aligne sur les priorités générales du projet.
 - Pour les soumissions proposant des améliorations mineures ou des corrections, ce n'est pas nécessaire. Vous pouvez sauter cette étape.
 - Lors de l'ouverture d'un ticket, veuillez lui donner un titre et remplir la section description. Plus vous fournissez de détails, plus nous pouvons donner de commentaires.

2. Après avoir reçu votre numéro, l'équipe de documentation JS Express répondra avec vos commentaires. Nous lisons chaque soumission et essayons toujours de répondre rapidement par un commentaire.
 - Pour les soumissions proposant des changements importants, nous vous encourageons à suivre le processus d’examen avant de commencer à travailler.

#### Étape 2 : Obtenir la base du code d'application

Cloner le dépôt et obtenir le code :

```
git clone https://github.com/expressjs/expressjs.com.git
```

Après avoir reçu le code, vous êtes prêt à commencer à faire vos changements !

Mais juste au cas où vous auriez besoin d'une explication supplémentaire, cette section ci-dessous décrit les sections principales de la base de code, où la plupart des changements sont susceptibles d'être apportés.

**Fichiers de page Markdown**:

- Ces fichiers sont rendus en html et constituent les pages individuelles du site. La plupart du contenu de la documentation du site est écrit dans des fichiers `md`.
- Modifiez-les pour apporter des modifications au contenu/texte ou au balisage de chaque page.
- Chaque langue a son propre ensemble complet de pages, situés dans leurs répertoires linguistiques respectifs - tout le contenu du markdown espagnol se trouve dans le répertoire `es`, par exemple.

**Inclut les modèles de mise en page et partiels**

- `_includes` sont des partiels qui sont importés et réutilisés sur plusieurs pages.
 - Ils sont utilisés pour importer du contenu de texte à réutiliser entre les pages, comme la documentation de l'API, e. ., `_includes > api > fr > 5x`, qui est inclus dans chaque langue.
 - Ils sont utilisés pour inclure les composants de page qui composent l'interface utilisateur et la structure de périphérie du site, par exemple Header, Footer, etc.
- `_layouts` sont les modèles utilisés pour envelopper les pages individuelles du site.
 - Celles-ci sont utilisées pour afficher la structure de la périphérie du site, comme l'en-tête et le pied de page, et pour injecter et afficher des pages marqudown individuelles à l'intérieur de la balise `content`.

**Fichiers Markdown du blog**

- Ces fichiers composent les différents articles de blog. Si vous voulez contribuer à un article de blog, veuillez
 suivre les instructions spécifiques pour [Comment écrire un blog.](https://expressjs.com/en/blog/write-post.html)
- Situé dans le répertoire `_posts`.

**CSS or Javascript**

- Tous les fichiers css et js sont conservés dans les dossiers `css` et `js` à la racine du projet.

Le site Web Express JS est construit en utilisant [Jeykyll](https://jekyllrb.com/) et est hébergé sur [Github Pages](https://pages.github.com/).

#### Étape 3 : Exécution de l'application

Maintenant vous aurez besoin d'un moyen de voir vos modifications, ce qui signifie que vous aurez besoin d'une version en cours d'exécution de l'application. Vous avez deux options.

1. **Exécuter Locally**: Cela fait fonctionner la version locale de l'application sur votre machine. Suivez notre [Guide de configuration locale] (https://github.com/expressjs/expressjs.com?tab=readme-ov-file#local-setup) pour utiliser cette option.
 - C'est l'option recommandée pour les travaux modérés ou complexes.
2. **Exécuter en utilisant l'aperçu du déploie**: Utilisez cette option si vous ne voulez pas vous ennuyer avec une installation locale. Une partie de notre pipeline d'intégration continue comprend [Netlify Deploy Preview] (https://docs.netlify.com/site-deploys/deploy-previews/).
 1. Pour utiliser cela, vous aurez besoin de mettre vos modifications en ligne - une fois que vous aurez fait votre premier commit sur votre branche de fonctionnalités, faire une demande d'ajout de _brouillon_.
 2. Une fois les étapes de construction terminées, vous aurez accès à un onglet **Deploy Preview** qui exécutera vos modifications sur le web, la reconstruction après chaque commit est poussée.
 3. Une fois que vous avez terminé votre travail et qu'il est prêt à être revu, supprimez le statut de l'ébauche de votre pull request et soumettez votre travail.

## Contribuer aux traductions

#### Avis: Nous avons suspendu toutes les contributions à la traduction.

> **IMPORTANT:**
> Nous travaillons actuellement vers un flux de travail de traductions plus rationalisé. Tant que cet avis sera publié, nous n'accepterons _pas_ aucune soumission de traduction.

Nous encourageons vivement les traductions communautaires ! Nous n'avons plus de traductions professionnelles, et nous croyons en la puissance de notre communauté à fournir des traductions précises et utiles.

La documentation est traduite dans ces langues :

- Anglais (`en`)
- Espagnol (`es`)
- Français (`fr`)
- Italien (`it`)
- Indonésien (`id`)
- Japonais (`ja`)
- Coréen (`ko`)
- Portugais brésilien (`pt-br`)
- Russe (`ru`)
- Slovak (`sk`)
- Thaï (`th`)
- Turc (`tr`)
- Ukrainien (`uk`)
- Uzbek (`uz`)
- Chinois simplifié (`zh-cn`)
- Chinois traditionnel (`zh-tw`)

### Ajout de nouvelles traductions complètes du site

Si une traduction est manquante dans la liste, vous pouvez en créer une nouvelle.

Pour traduire Expressjs.com dans une nouvelle langue, suivez ces étapes:

1. Cloner le dépôt [`expressjs.com`](https://github.com/expressjs/expressjs.com).
2. Créez un répertoire pour la langue de votre choix en utilisant son [code ISO 639-1](https://www.loc.gov/standards/iso639-2/php/code_list.php) comme nom.
3. Copiez `index.md`, `api.md`, `starter/`, `guide/`, `advanced/`, `resources/`, `4x/`, et `3x/`, dans le répertoire de langue.
4. Retirez le lien vers la documentation 2.x du menu "Référence API".
5. Mettre à jour la variable `lang` dans les fichiers markdown copiés.
6. Mettre à jour la variable `title` dans les fichiers markdown copiés.
7. Créer le fichier d'en-tête, de pied de page, de notification et d'annonce pour la langue dans le répertoire `_includes/`, dans les répertoires respectifs, et faire les modifications nécessaires au contenu.
8. Crée le fichier d'annonce pour la langue dans le répertoire `_includes/`.
9. Assurez-vous d'ajouter `/{{ page.lang }}` à tous les liens du site.
10. Mettez à jour les fichiers [CONTRIBUTING.md](https://github.com/expressjs/expressjs.com/blob/gh-pages/CONTRIBUTING.md#contributing-translations) et `.github/workflows/translation.yml` avec la nouvelle langue.

### Ajout des traductions de page et de section

De nombreuses traductions de sites manquent encore de pages. Pour trouver ceux avec lesquels nous avons besoin d'aide, vous pouvez [filtrer pour les PR fusionnées] (https://github.com/expressjs/expressjs.com/pulls?q=is%3Apr+is%3Aclosed+label%3Arequires-translation-es) qui incluent le tag pour votre langue, comme `requires-translation-es` pour les besoins de traduction en espagnol.

Si vous contribuez à une page ou une traduction de section, veuillez consulter la RP originale. Cela aide la personne à fusionner votre traduction pour supprimer la balise de la PR originale.
