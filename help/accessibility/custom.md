---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;Profilo unificato;unificato;Profilo;rtcp;XDM
title: Soluzioni personalizzate per l’accessibilità, ad Experience Platform
type: Documentation
description: Ulteriori informazioni sulle soluzioni di accessibilità personalizzate nell’interfaccia utente di Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Soluzioni di accessibilità personalizzate, ad Experience Platform

Adobe Experience Platform viene continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e aderire agli standard mondiali che includono le persone con disabilità visive, uditive, di mobilità o di altro tipo. Questo documento illustra le soluzioni di accessibilità personalizzate all’interno dell’interfaccia utente di Experience Platform.

## Panoramica della pagina principale e dell’interfaccia utente

L’interfaccia utente di Experience Platform soddisfa le proporzioni di contrasto richieste per i componenti normali di testo, grafica e interfaccia utente. I colori dell’interfaccia utente sono stati scelti anche per supportare l’accessibilità per tutti gli utenti, inclusi quelli con disabilità visive.

In Platform, gli elementi dell’interfaccia utente cliccabili o utilizzabili con un puntatore possono essere attivati anche utilizzando una tastiera. Ciò include la navigazione a sinistra, lettori video, tabelle e altro ancora.

Experience Platform si impegna a soddisfare gli standard internazionali di accessibilità, tra cui le linee guida per l’accessibilità dei contenuti web 2.1, di livello A e AA, e gli standard web WAI-ARIA (Accessible Rich Internet Applications) dell’iniziativa per l’accessibilità dei contenuti web.

![Pagina principale dell’interfaccia utente di Adobe Experience Platform.](images/homepage.png)

## Pannello di navigazione a sinistra

La barra di navigazione a sinistra nell’interfaccia utente di Experience Platform è accessibile da tastiera e fornisce un contrasto del colore negli stati normale, al passaggio del mouse e di selezione che soddisfano gli standard di accessibilità.

Dalla schermata Home, gli utenti possono passare alla navigazione a sinistra. Selezione **Maiusc+Tab** riporta l’utente alla schermata iniziale.

![L’Experience Platform ha lasciato la navigazione.](images/left-navigation-select.png)

Con la barra di navigazione a sinistra attivata, **Linguetta** porta gli utenti all’interazione di espansione e compressione. La possibilità di espandere o comprimere il pannello di navigazione a sinistra è attivata con **Invio (ritorno)**.

![La navigazione a sinistra dell’Experience Platform è stata compressa.](images/left-navigation-collapse.png)

Attivando la barra di navigazione a sinistra, i tasti freccia su e freccia giù consentono di passare a ciascun elemento della barra di navigazione e di scorrere continuamente (in altre parole, lo stato attivo non si sposta finché l&#39;utente non si sposta dalla barra di navigazione a sinistra). Se questa opzione è selezionata, lo stato attivo viene visualizzato per gli elementi di navigazione. La selezione corrente viene visualizzata con un testo evidenziato e in grassetto. Quando si seleziona un elemento di navigazione sinistro, **Invio (ritorno)** apre la voce di interfaccia utente selezionata nel pannello di destra, tuttavia lo stato attivo rimane nella navigazione a sinistra fino a quando l’utente non si sposta.

![L’Experience Platform mostra la navigazione a sinistra con Origini selezionate.](images/left-navigation-sources.png)

Alcune funzioni di Platform non sono abilitate per tutti gli utenti. Questi elementi vengono visualizzati nella navigazione ma non possono essere selezionati. Quando si naviga con una tastiera, questi elementi vengono ignorati durante la navigazione con le frecce e non possono essere selezionati utilizzando **Invio (ritorno)**.

![Le sezioni del pannello di navigazione a sinistra dell’Experience Platform non abilitate per l’utente non possono essere selezionate.](images/left-navigation-sections-disabled.png)

## Finestra di dialogo del video incorporato

I video possono essere visualizzati in Experience Platform utilizzando la navigazione da tastiera per evidenziare e selezionare un collegamento video disponibile. Viene aperta una finestra di dialogo con video incorporato nell’interfaccia utente di Platform.

![Un bordo blu che appare intorno a un elemento selezionato per indicare che è applicato lo stato attivo.](images/profile-overview-tab.png)

## Accessibilità da tastiera della finestra di dialogo per video

La finestra di dialogo del video incorporato può essere visualizzata anche utilizzando la tastiera. La tabella seguente illustra la navigazione completa da tastiera disponibile per la finestra di dialogo del video incorporato.

| Elemento finestra di dialogo | Accessibilità da tastiera | Descrizione |
|---|---|---|
| Riproduci e Pausa | Linguetta<br/>Barra spaziatrice | Utilizzare **Linguetta** per impostare lo stato attivo sul pulsante di riproduzione. **Barra spaziatrice** avvia la riproduzione del video e la mette in pausa. |
| Scrubber | Linguetta<br/>Freccia sinistra<br/>Freccia destra | Durante la riproduzione del video, utilizza **Linguetta** per mettere a fuoco lo scorrimento. Con lo scorrimento a fuoco, **tasti freccia sinistra e destra** salta la riproduzione video avanti e indietro di 5 secondi, rispettivamente. |
| Disattiva audio | Linguetta<br/>Barra spaziatrice | Utilizzare **Linguetta** per attivare l&#39;elemento volume disattivato. Utilizzare **barra spaziatrice** per disattivare o disattivare la riproduzione video. |
| Volume | Linguetta<br/>Freccia sinistra<br/>Freccia destra | Utilizzare **Linguetta** per concentrarsi sull&#39;elemento volume. **Freccia sinistra e freccia destra** spostare il volume verso l&#39;alto o verso il basso, rispettivamente. |
| [!UICONTROL Sottotitoli] (&quot;cc&quot;) | Linguetta<br/>Invio<br/>Freccia su<br/>Freccia giù | **Linguetta** a [!UICONTROL Sottotitoli] (cc). Utilizzare **Invio** per aprire il menu e **tasti freccia su e giù** per selezionare una lingua per i sottotitoli. **Invio** conferma la selezione. |
| [!UICONTROL Qualità] | Linguetta<br/>Invio<br/>Freccia su<br/>Freccia giù | Utilizzare **Linguetta** per concentrare [!UICONTROL Qualità] elemento. Utilizzare **Invio** per aprire il menu e **tasti freccia su e giù** per selezionare la qualità video. **Invio** conferma la selezione. |
| Schermo intero | Linguetta<br/>Barra spaziatrice o Invio<br/>Escape | Utilizzare **Linguetta** per mettere a fuoco l’elemento a schermo intero. Utilizzare **barra spaziatrice o Invio** per attivare la visualizzazione a schermo intero. **Escape** (&quot;esc&quot;) esce dalla modalità a schermo intero. |
| Chiudi | Linguetta<br/>Barra spaziatrice o Invio | Utilizzare **Linguetta** per attivare il pulsante chiudi. Utilizzare **barra spaziatrice o Invio** per uscire dalla finestra di dialogo del video. |

>[!NOTE]
>
>In qualsiasi momento durante la riproduzione, è possibile utilizzare il tasto Esc per chiudere la finestra di dialogo del video incorporato.

![Finestra di dialogo del video incorporato con numeri che identificano gli elementi di navigazione della tastiera.](images/video-dialog.png)

## Trascinamento file

Ad Experience Platform, tutte le zone di trascinamento della selezione dei file sono accessibili da tastiera. Utilizzo di **Linguetta** da evidenziare **[!UICONTROL Scegli i file]** e utilizzando **Invio o barra spaziatrice** per selezionarla, viene richiamata l&#39;interfaccia utente di selezione file del sistema operativo.

Dopo il caricamento di un file, l’icona Elimina diventa navigabile da tastiera per rimuovere il file selezionato e caricarne uno nuovo. Gli utenti possono **Linguetta** per concentrarsi sull’icona elimina e **Invio o barra spaziatrice** per selezionarlo. Una volta rimosso il file, **[!UICONTROL Scegli i file]** è automaticamente attivo e può essere selezionato.

In alternativa, se il file caricato non è nel formato corretto, viene visualizzata un’icona di errore insieme a un messaggio di errore e alla **[!UICONTROL Scegli i file]** è attivo e selezionabile.

![Zona di trascinamento file con un messaggio di errore e pulsante Scegli file attivo.](images/drag-and-drop.png)

L’utilizzo del mouse per selezionare la zona di trascinamento attiva anche l’interfaccia utente per la selezione dei file, in modo che un utente del mouse possa selezionare un file e trascinarlo nella zona per iniziare il caricamento.

![Una zona di trascinamento dei file attiva quando un utente del mouse trascina un file nella zona.](images/drag-and-drop-mouse-over.png)

## Sfoglia tabella

Tutte le tabelle all’interno dell’interfaccia utente di Experience Platform sono accessibili da tastiera. È possibile navigare e interagire con le righe e le colonne della tabella tramite una serie di scelte rapide da tastiera:

* Dall’intestazione della tabella, utilizza **freccia giù** per sfogliare la tabella. Le intestazioni della tabella sono selezionabili quando si naviga tramite **Linguetta** e puoi modificare l’ordinamento utilizzando **barra spaziatrice**.
* **Tasti freccia su e freccia giù** si sposta verso l&#39;alto o il basso nelle righe della tabella.
* Quando una riga è selezionata o attivata, utilizzando **Invio** nella riga fornisce i dettagli nella barra a destra.
* Quando una riga è selezionata o attivata, utilizza **tasti freccia** per spostarsi tra gli elementi della riga.
* Utilizzare **Invio** per selezionare un elemento nella riga. Gli utenti con utilità per la lettura dello schermo vengono avvisati se è necessario aprire una nuova finestra.
* Quando si esegue lo zoom al 200% o più, è possibile visualizzare **ispettore della rotaia** mentre la barra a destra si comprime per fornire più spazio di visualizzazione per la tabella.

![L’icona del pannello di ispezione è visibile quando un utente ingrandisce la visualizzazione al 200%.](images/rail-inspector.png)

### Accesso facilitato alla tastiera per la navigazione in tabella

| Accessibilità da tastiera | Descrizione |
|---|---|
| HOME (Funzione + freccia sinistra) | Quando si attiva la riga, porta gli utenti al primo elemento della riga |
| END (Funzione + freccia destra) | Quando si attiva la riga, porta gli utenti all&#39;ultimo elemento della riga |
| Pagina su | Attraversa 10 righe verso l’alto nella tabella (per pagina) |
| Pagina successiva | Attraversa 10 righe verso il basso nella tabella (per pagina) |
| Ctrl + HOME | Passa alla prima riga della tabella |
| Ctrl + FINE | Passa alla prima funzione nella tabella per pagina |

## Interfaccia utente dell’editor schema

L’interfaccia utente dell’Editor schema è resa accessibile dalle seguenti funzionalità:

* L’Editor di schema supporta la navigazione da tastiera, incluso l’utilizzo di **Linguetta** alla navigazione attraverso gli elementi dell’interfaccia utente.
* **Linguetta** immette il campo di ricerca, quindi nella struttura dello schema.
* La struttura dello schema supporta l&#39;utilizzo dei tasti freccia per spostarsi nell&#39;interfaccia utente della struttura dello schema
   * **Frecce su e giù** può essere utilizzato per scorrere l’albero.
   * **Frecce sinistra e destra** può essere utilizzato per espandere e comprimere i nodi o per spostarsi tra le azioni in linea nella struttura dello schema.
* **Invio (ritorno)** attiva i dettagli dei singoli nodi nel pannello dettaglio a destra.
* Il **Home** ritorna alla parte superiore della struttura.
* Il **Fine** tasto consente di spostarsi nella parte inferiore della struttura.
* La struttura dello schema include anche etichette ARIA per gli assistenti vocali.

## Interfaccia utente di Segment Builder

Quando utilizzi l’interfaccia utente del Generatore di segmenti per creare, modificare e interagire con i segmenti all’interno di Experience Platform, le seguenti funzioni migliorano l’accessibilità:

* L’interfaccia utente del Generatore di segmenti è accessibile tramite navigazione da tastiera.
* Gli assistenti vocali devono riconoscere i tag di markup per i titoli e possono annunciare l’intestazione e il relativo livello.
* Altre tecnologie per l’accessibilità possono modificare la visualizzazione visiva di una pagina utilizzando intestazioni codificate in modo appropriato per visualizzare una struttura o una vista alternativa.

Ora puoi comprimere o espandere le barre sinistra e destra dell’area di lavoro del generatore di segmenti per aumentare lo spazio disponibile sullo schermo. Questa funzione è particolarmente utile in quanto offre una funzionalità completa con uno zoom del 200%.

![L’area di lavoro del generatore di segmenti con i widget di divulgazione della barra a sinistra e a destra sono evidenziati.](images/left-right-rail-expandables.png)

## Editor servizio query

Nell’editor di Query Service sono disponibili le seguenti funzioni di accessibilità:

* Il contrasto cromatico nell’interfaccia utente dell’editor di Query Service è conforme all’accessibilità.
* La navigazione tramite tastiera è supportata al di fuori dell’interfaccia utente dell’editor. L’interfaccia utente dell’editor è un Code Mirror incorporato.

## Scheda Vista sistema in Origini e destinazioni

Durante la navigazione in **[!UICONTROL Vista sistema]** in Origini e destinazioni, le seguenti funzionalità migliorano l’accessibilità:

* **Linguetta** imposta lo stato attivo sulla prima scheda di connessione sorgente
   * **Linguetta** di nuovo per concentrarti sul pulsante all’interno della scheda
   * Seleziona **Invio** per attivare il pulsante di invito all’azione all’interno della scheda
* Selezione **Invio** sulla scheda di connessione attiva anche ulteriori dettagli nella barra a destra
   * Quando la barra a destra è attivata, lo stato attivo è impostato su tale area. **Linguetta** si concentra su **Chiudi** per il riquadro della barra a destra. Selezione **Linguetta** sposta di nuovo lo stato attivo attraverso la barra a destra
   * Se sono presenti più schede di connessione sorgente, **Linguetta** si sposta tra le connessioni
   * Utilizzare **tasti freccia (su, giù, sinistra e destra)** per spostarsi nell&#39;elenco delle origini
   * Seleziona **Linguetta** per mettere a fuoco il pannello nella barra a destra
