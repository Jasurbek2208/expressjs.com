---
layout: page
title: Contribuire a Express
description: Scopri come contribuire a Express.js, comprese le linee guida per i problemi di segnalazione, l'invio di richieste di pull, il diventare un collaboratore e la comprensione delle politiche di sicurezza.
menu: resources
lang: it
redirect_from: ""
---

# Contribuire a Express

### Stai cercando di contribuire a Expressjs.com? Click [here](#expressjs-website-contributing).

Express e gli altri progetti dell'organizzazione [expressjs su GitHub](https://github.com/expressjs) sono progetti della [OpenJs Foundation](https://openjsf.org/).
Questi progetti sono disciplinati dalle politiche generali e dalle linee guida della Fondazione Node.js insieme alle linee guida aggiuntive che seguono.

- [Comitato tecnico](#technical-committee)
- [Guida al contributo della comunità](#community-contributing-guide)
- [Guida del collaboratore](#collaborators-guide)
- [Politiche e procedure di sicurezza](#security-policies-and-procedures)

## Comitato tecnico

Il comitato tecnico espresso è composto da membri attivi del progetto e guida lo sviluppo e la manutenzione del progetto Express. Per ulteriori informazioni, vedere [Express Community - Technical committee](community.html#technical-committee).

## Guida al contributo comunitario

<!-- SRC: expressjs/express Contributing.md -->

L'obiettivo del presente documento è quello di creare un processo di contributo che:

- Incoraggia nuovi contributi.
- Incoraggia i contributori a rimanere coinvolti.
- Evitare i processi e la burocrazia inutili ogniqualvolta possibile.
- Creates a transparent decision making process that makes it clear how
 contributors can be involved in decision making.

### Vocabolario

- Un **contributore** è qualsiasi individuo che crea o commenta su un problema o su una richiesta di pull.
- Un **Committer** è un sottoinsieme di contributori a cui è stato dato accesso in scrittura al repository.
- Un **Capitano del Progetto** è il responsabile principale di un repository.
- Un **TC (Comitato Tecnico)** è un gruppo di committenti che rappresentano le competenze tecniche
 necessarie per risolvere controversie rare.
- Un **Triager** è un sottoinsieme di contributori a cui è stato dato l'accesso di triage al repository.

### Problemi Di Registrazione

Registra un problema per qualsiasi domanda o problema che potresti avere. In caso di dubbio, registrare un problema e
qualsiasi criterio aggiuntivo su cosa includere sarà fornito nelle risposte. L'unica eccezione
è la comunicazione di informazioni sulla sicurezza che dovrebbe essere inviata in privato.

I committenti possono indirizzare l'utente verso un altro repository, chiedere chiarimenti aggiuntivi e
aggiungere metadati appropriati prima che il problema venga affrontato.

Per favore, siate cortesi e rispettosi. Ogni partecipante dovrebbe seguire il Codice di condotta del progetto
.

### Contributi

Qualsiasi modifica delle risorse in questo repository deve avvenire tramite pull requests. Questo vale per tutte le modifiche
alla documentazione, al codice, ai file binari, ecc. Anche i committenti a lungo termine e i membri TC devono utilizzare le richieste di pull
.

Nessuna pull request può essere unita senza essere revisionata.

Per i contributi non banali, le richieste di pull dovrebbero sedersi per almeno 36 ore per garantire che i contributori di
in altri fusi orari abbiano il tempo di rivedere. Dovrebbero essere presi in considerazione anche i fine settimana
e altri periodi di ferie per garantire che gli impegni attivi abbiano tutti un tempo ragionevole per
essere coinvolti nel processo di discussione e di revisione, se lo desiderano.

Il valore predefinito per ogni contributo è che è accettato una volta che nessun committer ha un'obiezione.
Durante una recensione, gli impegni possono anche chiedere che un contributore specifico che è più esperto in una determinata area
fornisca una "LGTM" prima che la PR possa essere fusa. Non esiste un processo aggiuntivo "sign off"
per i contributi alla terra. Una volta risolte tutte le questioni sollevate dagli impegnatori,
può essere sbarcata da qualsiasi impegno.

In caso di obiezione sollevata in una richiesta di richiamo da parte di un altro committente, tutti gli impegni
interessati dovrebbero cercare di raggiungere un consenso per rispondere alle preoccupazioni espresse
mediante discussione, compromesso sulla modifica proposta o sul ritiro della modifica proposta.

Se un contributo è controverso e gli impegni non possono concordare su come farlo atterrare
o se dovrebbe atterrare allora dovrebbe essere aumentato al TC. I membri del TC dovrebbero discutere regolarmente di
i contributi in sospeso per trovare una risoluzione. Si prevede che solo una piccola minoranza di questioni
sia portata al TC per la risoluzione e che la discussione e il compromesso
tra gli impegni costituiscano il meccanismo di risoluzione di default.

### Diventare un Triager

Chiunque può diventare un triangolo! Per saperne di più sul processo di essere un triager in
[il documento di processo di triage](https://github.com/expressjs/express/blob/master/Triager-Guide.md).

Attualmente, qualsiasi [membro dell'organizzazione](https://github.com/orgs/expressjs/people) può nominare
un nuovo triager. Se siete interessati a diventare un triager, il nostro miglior consiglio è quello di partecipare attivamente a
nella comunità aiutando a risolvere i problemi e le richieste di richiamo. Raccomandiamo inoltre a
di impegnarsi in altre attività della comunità come partecipare alle riunioni TC e partecipare alle discussioni Slack
. If you feel ready and have been helping triage some issues, reach out to an active member of the organization to ask if they'd
be willing to support you. Se sono d'accordo, possono creare una richiesta pull per formalizzare la vostra nomina. Nel caso di un'obiezione alla nomina, la squadra di triage è responsabile di lavorare con le persone coinvolte e di trovare una risoluzione.

Puoi anche contattare uno qualsiasi dei [membri dell'organizzazione](https://github.com/orgs/expressjs/people)
se hai domande o hai bisogno di guida.

### Diventare un Committer

Tutti i contributori che hanno apportato contributi significativi e preziosi dovrebbero essere imbarcati in modo tempestivo,
e aggiunto come committente, ed è dato l'accesso in scrittura al repository.

Si prevede che i committenti seguano questa politica e continuino a inviare richieste di pull, passare attraverso la corretta revisione
e hanno altri committenti unire le loro richieste di pull.

### Processo TC

Il TC utilizza un processo di "ricerca del consenso" per le questioni che sono escalated al TC.
Il gruppo cerca di trovare una risoluzione che non abbia obiezioni aperte tra i membri del TC.
Se non è possibile raggiungere un consenso che non ha obiezioni, viene chiamata una maggioranza che vince il voto
. Si prevede inoltre che la maggior parte delle decisioni prese dal TC siano tramite
un processo di ricerca del consenso e che il voto sia utilizzato solo come ultima risorsa.

La risoluzione può comportare il ritorno della questione ai capitani di progetto con suggerimenti su
come procedere verso un consenso. Non si prevede che una riunione del TC
risolverà tutte le questioni all'ordine del giorno durante tale riunione e potrebbe preferire continuare
la discussione che sta accadendo tra i capitani del progetto.

I membri possono essere aggiunti al TC in qualsiasi momento. Ogni membro del TC può nominare un altro committer
per il TC e il TC utilizza il suo processo di ricerca di consenso standard per valutare se o
per aggiungere questo nuovo membro. Il TC sarà composto da un minimo di 3 membri attivi e un massimo di 10 membri
. Se il TC dovrebbe scendere al di sotto di 5 membri, i membri del TC attivi dovrebbero nominare
qualcuno nuovo. Se un membro del TC sta scendendo, sono incoraggiati (ma non richiesto) a
nominare qualcuno per prendere il loro posto.

I membri del TC saranno aggiunti come admin sugli organi di Github, npm orgs, e altre risorse come
necessario per essere efficaci nel ruolo.

Per rimanere "attivo" un membro del TC dovrebbe partecipare negli ultimi 12 mesi e mancare di
non più di sei riunioni consecutive del TC. Il nostro obiettivo è aumentare la partecipazione, non punire le persone
per qualsiasi mancanza di partecipazione, questa linea guida dovrebbe essere utilizzata solo come tale
(sostituire un membro inattivo con un nuovo attivo, per esempio). I membri che non soddisfano questa
sono tenuti a dimettersi. Se un membro del TC non si allontana, un problema può essere aperto nelle discussioni di
repo per spostarli in stato inattivo. I membri del TC che si abbassano o vengono rimossi a causa di
per inattività verranno spostati in stato inattivo.

I membri dello status inattivi possono diventare membri attivi per autogoverno se il TC non è già
superiore al massimo di 10. Verrà anche data la preferenza se, mentre alla dimensione massima, un membro attivo
scenderà.

### Capitano Del Progetto

L'Express TC può designare capitani per singoli progetti/repos nelle organizzazioni
. Questi capitani sono responsabili di essere i principali
manutentori quotidiani del repo su un fronte tecnico e comunitario.
I capitani di Repo sono abilitati con la proprietà di repo e i diritti di pubblicazione pacchetto.
Quando ci sono conflitti, soprattutto su argomenti che influenzano il progetto Express
in generale, i capitani hanno la responsabilità di sollevare fino al TC e guidare
quei conflitti alla risoluzione. I capitani sono anche responsabili di assicurarsi che i membri della comunità
seguano le linee guida della comunità, mantenere il repo
e il pacchetto pubblicato, nonché fornire supporto agli utenti.

Come i membri di TC, i capitani di Repo sono un sottoinsieme di committenti.

Per diventare capitano di un progetto si prevede che il candidato partecipi al progetto
per almeno 6 mesi come committer prima della richiesta. Dovrebbero avere
aiutato con contributi di codice e problemi di triaging. Essi sono anche tenuti a
avere 2FA abilitato su entrambi i loro account GitHub e npm.

Qualsiasi membro del TC o un capitano esistente sul \*\*stesso repo \*\* può nominare un altro committer
al ruolo del capitano. A tal fine, essi dovrebbero presentare una PR al presente documento, aggiornamento della sezione
**Captains** del Progetto Attivo (mantenendo l'ordine di ordine) con il nome del progetto
, la maniglia GitHub del candidato e il loro nome utente npm (se diverso).

- Repos può avere tanti capitani come hanno senso per la portata del lavoro.
- Un membro di TC o un capitano di repo esistente **sullo stesso progetto** può nominare un nuovo capitano.
 I capitani di Repo di altri progetti non dovrebbero nominare capitani per un progetto diverso.

La PR richiederà almeno 2 approvazioni da parte dei membri TC e 2 settimane di tempo per consentire ad
di commentare e/o dissentire.  Quando la PR è unita, un membro di TC li aggiungerà ai gruppi di GitHub/npm di
.

#### Progetti attivi e capitani

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
- [`jshttp/negoziator`](https://github.com/jshttp/negotiator): @blakeembrey
- [`jshttp/on-finished`](https://github.com/jshttp/on-finished): @wesleytodd, @ulisesGascon
- [`jshttp/on-headers`](https://github.com/jshttp/on-headers): @blakeembrey
- [`jshttp/proxy-addr`](https://github.com/jshttp/proxy-addr): @wesleytodd, @ulisesGascon
- [`jshttp/range-parser`](https://github.com/jshttp/range-parser): @blakeembrey
- [`jshttp/statuses`](https://github.com/jshttp/statuses): @blakeembrey
- [`jshttp/typeis`](https://github.com/jshttp/type-is): @blakeembrey
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

#### Iniziativa Attuale Capitani

- Triage team [ref](https://github.com/expressjs/discussions/issues/227): @UlisesGascon

### Certificato di origine dello sviluppatore 1.1

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

## Guida del collaboratore

<!-- SRC: expressjs/express Collaborator-Guide.md -->

### Problemi Sul Sito

Open issues for the expressjs.com website in https://github.com/expressjs/expressjs.com.

### PRs e contributi del codice

- Le prove devono essere superate.
- Segui [JavaScript Standard Style](https://standardjs.com/) e `npm run lint`.
- Se correggi un bug, aggiungi un test.

### Rami

Usa il ramo `master` per le correzioni di bug o il lavoro minore che è destinato al flusso di rilascio corrente
.

Usa il ramo di nome corrispondente, ad esempio `5.0`, per tutto ciò che è destinato ad
una futura versione di Express.

### Passi per il contributo

1. [Creare un problema](https://github.com/expressjs/express/issues/new) per il bug
 che si desidera correggere o la funzione che si desidera aggiungere.
2. Crea il tuo [fork](https://github.com/expressjs/express) su GitHub, poi
 checkout il fork.
3. Scrivi il tuo codice nella tua copia locale. È buona pratica creare un ramo per
 ogni nuovo problema su cui lavori, anche se non obbligatorio.
4. Per eseguire la suite di prova, prima installare le dipendenze eseguendo `npm install`,
 quindi eseguire `npm test`.
5. Assicurati che il tuo codice sia lintato eseguendo `npm run lint` -- correggi qualsiasi problema che
 vedi elencato.
6. Se i test passano, è possibile inviare le modifiche al fork e quindi creare
 una pull request da lì. Assicurati di fare riferimento al tuo problema dai commenti della richiesta pull
 includendo il numero di problema, ad esempio `#123`.

### Questioni che sono domande

In genere chiuderemo eventuali problemi vaghi o domande che sono specifici per alcune app
che stai scrivendo. Si prega di controllare due volte i documenti e altri riferimenti prima di
essere attivati con successo con la pubblicazione di un problema di domanda.

Cose che aiuteranno a ottenere il problema della domanda ha esaminato:

- Codice JS completo ed eseguibile.
- Cancella la descrizione del problema o il comportamento imprevisto.
- Cancella la descrizione del risultato atteso.
- I passi che hai preso per debug te stesso.

Se si pubblica una domanda e non delineare gli elementi di cui sopra o rendere facile per
noi di capire e riprodurre il vostro problema, sarà chiuso.

## Politiche e procedure di sicurezza

<!-- SRC: expressjs/express Security.md -->

Il presente documento delinea le procedure di sicurezza e le politiche generali per il progetto Express
.

- [Segnalare un errore](#reporting-a-bug)
- [Politica Di Trasparenza](#disclosure-policy)
- [Commenti su questa Politica](#comments-on-this-policy)

### Segnala un bug

Il team e la comunità Express prendono sul serio tutti i bug di sicurezza in Express.
Grazie per aver migliorato la sicurezza di Express. Apprezziamo i tuoi sforzi e la divulgazione responsabile di
e faremo ogni sforzo per riconoscere i tuoi contributi
.

Segnala bug di sicurezza inviando un'email a `express-security@lists.openjsf.org`.

Per garantire la risposta tempestiva al tuo rapporto, si prega di assicurarsi che la totalità
del rapporto sia contenuta all'interno del corpo e-mail e non solo dietro un link web
o un allegato.

Il responsabile principale riconoscerà la tua email entro 48 ore, e invierà una risposta
più dettagliata entro 48 ore indicando i prossimi passi nella gestione
il tuo report. Dopo la prima risposta al tuo rapporto, il team di sicurezza cercherà
di tenerti informato dei progressi verso un annuncio completo e completo
, e può chiedere ulteriori informazioni o orientamenti.

Segnala bug di sicurezza nei moduli di terze parti alla persona o al team che mantiene
il modulo.

### Versioni Pre-release

Le versioni Alpha e Beta sono instabili e **non adatte all'uso in produzione**.
Le vulnerabilità trovate nelle pre-release devono essere segnalate secondo la sezione [Segnalazione di un Bug](#reporting-a-bug).
A causa della natura instabile del ramo non è garantito che eventuali correzioni saranno rilasciate nella prossima pre-rilascio.

### Politica Di Divulgazione

Quando il team di sicurezza riceve una segnalazione di bug di sicurezza, la assegnerà a un gestore primario
. Questa persona coordinerà il processo di correzione e rilascio,
che comporta i seguenti passaggi:

- Confermare il problema e determinare le versioni interessate.
- Codice di controllo per trovare eventuali problemi simili.
- Preparare correzioni per tutte le versioni ancora in manutenzione. Queste correzioni saranno
 rilasciate il più velocemente possibile a npm.

### Il Modello Espresso Di Minaccia

Attualmente stiamo lavorando su una nuova versione del modello di sicurezza, la versione più aggiornata può essere trovata [here](https://github.com/expressjs/security-wg/blob/main/docs/ThreatModel.md)

### Osservazioni su questa politica

Se avete suggerimenti su come questo processo potrebbe essere migliorato si prega di inviare una richiesta di pull
.

----

# Contribuire a Expressjs.com {#expressjs-website-contributing}

<!-- LOCAL: expressjs/expressjs.com ../../CONTRIBUTING.md -->

### Documentazione ufficiale del quadro JS espresso

Questa è la documentazione di contributo per il sito web [Expressjs.com](https://github.com/expressjs/expressjs.com).

#### Hai bisogno di idee? Questi sono alcuni problemi tipici.

1. **Problemi del sito web**:
 Se vedi qualcosa sul sito che potrebbe usare un tune-up, pensa a come risolverlo.

 - Problemi di visualizzazione o dimensionamento dello schermo
 - Problemi di reattività mobile
 - Funzioni di accessibilità mancanti o rotte
 - Interruzioni del sito
 - Collegamenti interrotti
 - Miglioramenti della struttura della pagina o dell'interfaccia utente

2. **Problemi di contenuti**:
 Risolvi tutto ciò che riguarda il contenuto del sito o gli errori di battitura.
 - Errori ortografici
 - Documentazione JS non corretta/obsoleta
 - Contenuto mancante

3. **Problemi di traduzione**: risolvere eventuali errori di traduzione o contribuire con nuovi contenuti.
 - Correggi errori di ortografia
 - Correggi parole non corrette/mal tradotte
 - Traduci nuovi contenuti

> **IMPORTANTE:**
> Tutti i messaggi di traduzione sono attualmente in pausa. Vedi questa [notice](#notice-we-have-paused-all-translation-contributions) per maggiori informazioni.

- Scopri la sezione [Contribuire alle traduzioni](#contributing-translations) qui sotto per una guida contribuente.

#### Vuoi lavorare su un problema di backlog?

Abbiamo spesso bug o miglioramenti che hanno bisogno di lavoro. Puoi trovarli sotto la [scheda Problemi del nostro repo](https://github.com/expressjs/expressjs.com/issues). Dai un'occhiata ai tag per trovare qualcosa che sia una buona partita per te.

#### Hai un'idea? Trovato un bug?

Se hai trovato un bug o un typo, o se hai un'idea per un miglioramento, puoi:

- Invia un [nuovo problema](https://github.com/expressjs/expressjs.com/issues/new/choose) sul nostro repo. Fare questo per le proposte più grandi, o se si desidera discutere o ottenere il feedback prima.
- Make a [Github pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request). Se avete già fatto il lavoro ed è pronto ad andare, sentitevi liberi di inviare la nostra strada.

## Introduzione

I passaggi seguenti ti guideranno attraverso il processo di contribuzione di Expressjs.com.

#### Passo 1: (OPZIONALE) Aprire un nuovo problema

Così hai trovato un problema che si desidera risolvere, o avere un miglioramento del sito che si desidera fare.

1. Se vuoi ottenere un feedback o discutere, apri una discussione [issue](https://github.com/expressjs/expressjs.com/issues/new/choose) prima di iniziare a lavorare. Ciò non è necessario, ma è incoraggiato a presentare proposte più ampie.
 - Pur incoraggiando vivamente questo passo, è solo per le proposte che propongono cambiamenti significativi. Ci aiuta a chiarire e concentrare il lavoro e a garantire che esso si allinei con le priorità generali del progetto.
 - Per le presentazioni che propongono miglioramenti o correzioni di lieve entità, ciò non è necessario. Puoi saltare questo passaggio.
 - Quando si apre un problema si prega di dare un titolo e compilare la sezione descrizione. Più dettagli fornisci, più feedback possiamo dare.

2. Dopo aver ricevuto il tuo problema il team di documentazione Express JS risponderà con un feedback. Leggiamo ogni invio e cerchiamo sempre di rispondere rapidamente con un feedback.
 - Per le presentazioni che propongono cambiamenti significativi, vi invitiamo a seguire il processo di revisione prima di iniziare a lavorare.

#### Passo 2: Ottieni la base del codice di applicazione

Clona il repo e ottieni il codice:

```
git clone https://github.com/expressjs/expressjs.com.git
```

Dopo aver ricevuto il codice sei pronto per iniziare a fare le tue modifiche!

Ma nel caso in cui avete bisogno di una piccola spiegazione in più, questa sezione seguente delinea le sezioni principali della base di codici, in cui è probabile che la maggior parte delle modifiche siano apportate.

**File Della Pagina Markdown**:

- Questi file rendono in html e compongono le singole pagine del sito. La maggior parte del contenuto del testo della documentazione del sito è scritta in file `md`.
- Modificali per apportare modifiche al contenuto/testo o al markup delle singole pagine.
- Ogni lingua ha il suo set completo di pagine, localizzato sotto le rispettive directory linguistiche - tutti i contenuti di markdown spagnoli si trovano nella directory `es`, per esempio.

**Include Partials e Modelli di Layout**

- `_includes` sono parziali importati e riutilizzati su più pagine.
 - Questi sono utilizzati per importare contenuti di testo per il riutilizzo su tutte le pagine, come la documentazione API, e. ., `_include > api > it > 5x`, che è incluso in ogni lingua.
 - Questi sono utilizzati per includere i componenti della pagina che compongono l'interfaccia utente di tutto il sito e la struttura periferica, ad esempio, intestazione, piè di pagina, ecc.
- `_layouts` sono i modelli utilizzati per avvolgere le singole pagine del sito.
 - Questi sono utilizzati per visualizzare la struttura della periferia del sito, come l'intestazione e il piè di pagina, e per iniettare e visualizzare singole pagine di markdown all'interno del tag `content`.

**Blog Markdown Files**

- Questi file compongono i singoli post del blog. Se vuoi contribuire a un post sul blog, per favore
 segui le istruzioni specifiche per [Come scrivere un post sul blog.](https://expressjs.com/en/blog/write-post.html)
- Situato sotto la directory `_posts`.

**CSS or Javascript**

- Tutti i file css e js sono conservati nelle cartelle `css` e `js` nella radice del progetto.

Il sito di Express JS è costruito utilizzando [Jeykyll](https://jekyllrb.com/) ed è ospitato su [Github Pages](https://pages.github.com/).

#### Passo 3: Esecuzione dell'applicazione

Ora avrai bisogno di un modo per vedere le tue modifiche, il che significa che avrai bisogno di una versione in esecuzione dell'applicazione. Avete due opzioni.

1. **Esegui localmente**: Questo fa funzionare la versione locale dell'applicazione sulla tua macchina. Segui la nostra [Guida alle Impostazioni Locali](https://github.com/expressjs/expressjs.com?tab=readme-ov-file#local-setup) per utilizzare questa opzione.
 - Questa è l'opzione consigliata per lavori da moderati a complessi.
2. **Esegui usando Deploy Preview**: Usa questa opzione se non vuoi preoccuparti con un'installazione locale. Parte della nostra pipeline di integrazione continua include [Anteprima Deploy Netlify](https://docs.netlify.com/site-deploys/deploy-previews/).
 1. Per utilizzare questo dovrai ottenere le modifiche online - dopo aver effettuato il tuo primo commit sul tuo ramo di funzionalità, fai una richiesta di pull _bozza_.
 2. Dopo che i passaggi di costruzione saranno completati, avrai accesso a una scheda **Deploy Preview** che eseguirà le tue modifiche sul web, ricostruire dopo che ogni commit è stato spinto.
 3. Dopo aver fatto completamente il tuo lavoro ed è pronto per la revisione, rimuovi lo stato della bozza sulla tua pull request e invia il tuo lavoro.

## Contribuire alle traduzioni

#### Avviso: Abbiamo messo in pausa tutti i contributi di traduzione.

> **IMPORTANTE:**
> Attualmente stiamo lavorando verso un flusso di lavoro più semplificato per le traduzioni. Fintanto che questo avviso è pubblicato, _non_ accetteremo qualsiasi presentazione di traduzione.

Incoraggiamo vivamente le traduzioni della comunità! Non abbiamo più traduzioni professionali e crediamo nel potere della nostra comunità di fornire traduzioni accurate e utili.

La documentazione è tradotta in queste lingue:

- Inglese (`en`)
- Spagnolo (`es`)
- Francese (`fr`)
- Italiano (`it`)
- Indonesiano (`id`)
- Giapponese (`ja`)
- Coreano (`ko`)
- Portoghese Brasiliano (`pt-br`)
- Russo (`ru`)
- Slovak (`sk`)
- Tailandese (`th`)
- Turco (`tr`)
- Ucraino (`uk`)
- Uzbek (`uz`)
- Cinese Semplificato (`zh-cn`)
- Cinese Tradizionale (`zh-tw`)

### Aggiunta Di Nuove Traduzioni Completa Del Sito

Se si trova una traduzione mancante dalla lista è possibile crearne una nuova.

Per tradurre Expressjs.com in una nuova lingua, segui questi passaggi:

1. Clona il repository [`expressjs.com`](https://github.com/expressjs/expressjs.com).
2. Crea una directory per la lingua di tua scelta usando il suo [codice ISO 639-1](https://www.loc.gov/standards/iso639-2/php/code_list.php) come suo nome.
3. Copia `index.md`, `api.md`, `starter/`, `guide/`, `advanced/`, `resources/`, `4x/`, e `3x/`, nella directory della lingua.
4. Rimuovere il collegamento ai documenti 2.x dal menu "API Reference".
5. Aggiorna la variabile `lang` nei file di markdown copiati.
6. Aggiorna la variabile `title` nei file di markdown copiati.
7. Crea l'intestazione, il piè di pagina, l'avviso e il file di annuncio per la lingua nella directory `_includes/`, nelle rispettive directory, e rendere necessarie modifiche al contenuto.
8. Crea il file di annuncio per la lingua nella directory `_includes/`.
9. Assicurati di aggiungere `/{{ page.lang }}` a tutti i link all'interno del sito.
10. Aggiorna i file [CONTRIBUTING.md](https://github.com/expressjs/expressjs.com/blob/gh-pages/CONTRIBUTING.md#contributing-translations) e `.github/workflows/translation.yml` con la nuova lingua.

### Aggiunta di traduzioni di Pagina e Sezione

Molte traduzioni del sito sono ancora pagine mancanti. Per trovare quelli con cui abbiamo bisogno di aiuto, puoi [filtrare per i PRs uniti](https://github.com/expressjs/expressjs.com/pulls?q=is%3Apr+is%3Aclosed+label%3Arequires-translation-es) che includono il tag per la tua lingua, come `requires-translation-es` per richiedere la traduzione in spagnolo.

Se si contribuisce a una traduzione di una pagina o di una sezione, si prega di fare riferimento al PR. Questo aiuta la persona che unisce la tua traduzione per rimuovere il tag dal PR. originale
