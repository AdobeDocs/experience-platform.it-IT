---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;grafici XDM
title: Soluzioni di accessibilità personalizzate per Experience Platform
topic-legacy: guide
type: Documentation
description: Ulteriori informazioni sulle soluzioni di accessibilità personalizzate all'interno dell'interfaccia utente di Adobe Experience Platform.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---


# Soluzioni di accessibilità personalizzate per Experience Platform

Adobe Experience Platform viene continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e aderire agli standard mondiali che includono persone con disabilità visive, uditive, di mobilità o di altro tipo. Questo documento delinea soluzioni di accessibilità personalizzate all&#39;interno dell&#39;interfaccia utente di Experience Platform.

## Panoramica della pagina principale e dell’interfaccia utente

L’interfaccia utente di Experience Platform soddisfa i rapporti di contrasto richiesti per i normali componenti di testo, grafica e interfaccia utente. I colori dell’interfaccia utente sono stati scelti anche per supportare l’accessibilità per tutti gli utenti, inclusi quelli con disabilità visive.

In Platform, è possibile utilizzare una tastiera anche per gli elementi dell’interfaccia utente cliccabili o utilizzabili con un puntatore. Questo include la navigazione a sinistra, lettori video, tabelle e altro ancora.

L’Experience Platform si impegna a soddisfare gli standard internazionali di accessibilità, inclusi gli standard web WAI-ARIA (Accessibility Guidelines) di livello 2.1 e A e AA (Livello A e Livello AA) e WAI (Web Accessibility Initiative - Accessible Rich Internet Applications).

![Pagina principale dell’interfaccia utente di Adobe Experience Platform.](images/homepage.png)

## Navigazione a sinistra

La navigazione a sinistra nell’interfaccia utente di Experience Platform è accessibile da tastiera e offre un contrasto del colore in stati di normale, passaggio del mouse e selezione che soddisfa gli standard di accessibilità.

Dalla schermata Home, gli utenti possono passare al menu di navigazione a sinistra. Selezionando **Maiusc + Tab** l&#39;utente torna alla schermata iniziale.

![L&#39;Experience Platform ha lasciato la navigazione.](images/left-navigation-select.png)

Quando la navigazione a sinistra è attiva, **Tab** consente agli utenti di espandere e comprimere l&#39;interazione. La possibilità di espandere o comprimere la navigazione a sinistra viene attivata con **Invio (Invio)**.

![La navigazione a sinistra dell&#39;Experience Platform è compressa.](images/left-navigation-collapse.png)

Con la navigazione a sinistra in focus, i tasti freccia su e giù navigano su ogni elemento nella navigazione e circondano continuamente (in altre parole, lo stato attivo non si sposta via finché l&#39;utente non si sposta dalla navigazione a sinistra). Lo stato attivo viene visualizzato per gli elementi di navigazione quando selezionati. La selezione corrente viene visualizzata con un&#39;evidenziazione e un testo con grassetto. Quando si seleziona un elemento di navigazione a sinistra, **Invio (Invio)** apre l&#39;elemento di interfaccia selezionato nel pannello a destra, tuttavia lo stato attivo rimane nella navigazione a sinistra finché l&#39;utente non si sposta.

![Nell&#39;Experience Platform è stato selezionato il menu di navigazione a sinistra con Origini.](images/left-navigation-sources.png)

Alcune funzioni di Platform non sono abilitate per tutti gli utenti. Questi elementi vengono visualizzati nella navigazione ma non possono essere selezionati. Quando si naviga con una tastiera, questi elementi vengono ignorati durante la navigazione a freccia e non possono essere selezionati utilizzando **Invio (Invio)**.

![Impossibile selezionare le sezioni della navigazione a sinistra dell’Experience Platform non abilitate per l’utente.](images/left-navigation-sections-disabled.png)

## Finestra di dialogo video incorporato

I video possono essere visualizzati in Experience Platform utilizzando la navigazione da tastiera per evidenziare e selezionare un collegamento video disponibile. Viene visualizzata una finestra di dialogo video incorporata nell’interfaccia utente di Platform.

![Bordo blu intorno a un elemento selezionato per indicare che è stato applicato lo stato attivo.](images/profile-overview-tab.png)

## Accessibilità da tastiera della finestra di dialogo video

La finestra di dialogo video incorporata può anche essere navigata utilizzando la tastiera. La tabella seguente illustra la navigazione da tastiera completa disponibile per la finestra di dialogo video incorporata.

| Elemento finestra di dialogo | Accessibilità da tastiera | Descrizione |
|---|---|---|
| Riproduzione e pausa | Tab<br/>Barra spaziatrice | Utilizzare **Tab** per impostare lo stato attivo sul pulsante di riproduzione. **** La barra spaziatrice avvia la riproduzione del video e ne mette in pausa la riproduzione. |
| Scorrevole | Tab<br/>Freccia sinistra<br/>Freccia destra | Durante la riproduzione del video, utilizza **Tab** per attivare lo scorrimento. Con lo scorrimento in focus, **tasti freccia sinistra e destra** salta la riproduzione video rispettivamente avanti e indietro di 5 secondi. |
| Disattiva | Tab<br/>Barra spaziatrice | Utilizza **Tab** per attivare l&#39;elemento volume muto. Utilizzare la **barra spaziatrice** per disattivare o disattivare la riproduzione video. |
| Volume | Tab<br/>Freccia sinistra<br/>Freccia destra | Utilizza **Tab** per attivare l&#39;elemento del volume. **I** tasti freccia sinistra e destra spostano rispettivamente il volume verso l&#39;alto o verso il basso. |
| [!UICONTROL Sottotitoli]  chiusi (&quot;cc&quot;) | Tab<br/>Invio<br/>Freccia su<br/>Freccia giù | **Elemento** Tabto  [!UICONTROL Closed Captions] (&quot;cc&quot;). Utilizzare **Invio** per aprire il menu e **tasti freccia su e giù** per selezionare una lingua per le didascalie. **** Conferma la selezione. |
| [!UICONTROL Qualità] | Tab<br/>Invio<br/>Freccia su<br/>Freccia giù | Utilizza **Tab** per attivare l&#39;elemento [!UICONTROL Quality]. Utilizza **Invio** per aprire il menu e i **tasti freccia su e giù** per selezionare la qualità video. **** Conferma la selezione. |
| Schermo intero | Tab<br/>Barra spaziatrice o Invio<br/>Esc | Utilizza **Tab** per attivare l&#39;elemento a schermo intero. Utilizza la **barra spaziatrice o Invio** per attivare la visualizzazione a schermo intero. **Escape** (&quot;esc&quot;) esce dalla modalità a schermo intero. |
| Chiudi | Tab<br/>Barra spaziatrice o Invio | Usare **Tab** per attivare il pulsante di chiusura. Utilizza la **barra spaziatrice o il tasto Enter** per uscire dalla finestra di dialogo video. |

>[!NOTE]
>
>In qualsiasi momento durante la riproduzione, il tasto Esc (&quot;esc&quot;) può essere utilizzato per chiudere la finestra di dialogo video incorporata.

![La finestra di dialogo video incorporata con i numeri che identificano gli elementi di navigazione da tastiera.](images/video-dialog.png)

## Trascinamento file

Ad Experience Platform, tutte le zone di trascinamento e rilascio per la selezione dei file sono accessibili da tastiera. Utilizzando **Tab** per evidenziare **[!UICONTROL Scegli file]** e utilizzando **Invio o barra spaziatrice** per selezionarlo, viene richiamata l&#39;interfaccia utente del sistema operativo per la selezione dei file.

Dopo il caricamento di un file, l’icona Elimina diventa accessibile da tastiera per rimuovere il file selezionato e caricarne uno nuovo. Gli utenti possono utilizzare **Tab** per attivare l&#39;icona di eliminazione e **Invio o barra spaziatrice** per selezionarla. Una volta rimosso il file, **[!UICONTROL Scegli file]** viene automaticamente messo a fuoco e può essere selezionato.

In alternativa, se il file caricato non è nel formato corretto, viene visualizzata un&#39;icona di errore insieme a un messaggio di errore e il pulsante **[!UICONTROL Choose files]** è attivo e selezionabile.

![Zona di trascinamento file con messaggio di errore e pulsante di selezione file attivo.](images/drag-and-drop.png)

Se si utilizza un mouse per selezionare la zona di trascinamento, viene richiamata anche l’interfaccia utente per la selezione dei file. In alternativa, l’utente può selezionare un file e trascinarlo nella zona per iniziare il caricamento.

![Zona di trascinamento e rilascio del file, quando un utente del mouse trascina un file nella zona.](images/drag-and-drop-mouse-over.png)

## Sfoglia tabella

Tutte le tabelle nell’interfaccia utente di Experience Platform sono accessibili da tastiera. È possibile navigare e interagire con righe e colonne di una tabella tramite una serie di scelte rapide da tastiera:

* Dall’intestazione della tabella, utilizza la **freccia giù** per sfogliare la tabella. Le intestazioni di tabella sono selezionabili quando si naviga tramite **Tab** e è possibile modificare l&#39;ordine di ordinamento utilizzando **barra spaziatrice**.
* **I** tasti freccia Su e Giù si spostano in alto e in basso tra le righe della tabella.
* Quando una riga è selezionata o nello stato attivo, utilizzando **Invio** sulla riga sono riportati i dettagli nella barra a destra.
* Quando una riga è selezionata o nello stato attivo, utilizzare i tasti **freccia** per spostarsi all&#39;interno di ogni elemento della riga.
* Utilizza **Invio** per selezionare un elemento nella riga. Gli utenti con assistenti vocali ricevono un avviso se è necessario aprire una nuova finestra.

### Accessibilità della tastiera della tabella

| Accessibilità da tastiera | Descrizione |
|---|---|
| HOME (Funzione + freccia sinistra) | Quando la riga è attiva, porta gli utenti al primo elemento della riga |
| END (Funzione + freccia destra) | Quando la riga è attiva, porta gli utenti all’ultimo elemento della riga |
| Pagina in alto | Passa 10 righe verso l’alto nella tabella (per pagina) |
| Pagina giù | Passa 10 righe verso il basso nella tabella (per pagina) |
| Controllo + HOME | Passa alla prima riga della tabella |
| Controllo + FINE | Passa alla prima attività nella tabella per pagina |

## Interfaccia utente dell’Editor schema

L’interfaccia utente dell’Editor di schema è resa accessibile dalle seguenti funzionalità:

* L’Editor di schema supporta la navigazione da tastiera, incluso l’utilizzo di **Tab** per la navigazione tra gli elementi dell’interfaccia utente.
* **** Nella struttura dello schema, il campo di ricerca viene inserito nella scheda.
* La struttura dello schema supporta l’utilizzo di tasti freccia per spostarsi all’interno dell’interfaccia utente della struttura dello schema
   * **Per scorrere l&#39;albero, utilizzare** la freccia su e giù.
   * **La** freccia sinistra e destra possono essere utilizzate per espandere e comprimere i nodi o per spostarsi tra le azioni in linea nella struttura dello schema.
* **Invio (Invio)** attiva i dettagli dei singoli nodi nel pannello dei dettagli a destra.
* Il tasto **Home** torna nella parte superiore della struttura.
* Il tasto **Fine** si sposta nella parte inferiore della struttura.
* La struttura dello schema include anche le etichette ARIA per gli assistenti vocali.

## Interfaccia utente di Generatore di segmenti

Quando utilizzi l’interfaccia utente del Generatore di segmenti per creare, modificare e interagire con i segmenti all’interno di Experience Platform, le seguenti funzioni migliorano l’accessibilità:

* L’interfaccia utente del Generatore di segmenti è accessibile tramite la navigazione da tastiera.
* Gli assistenti vocali devono riconoscere i tag di markup per le intestazioni e possono annunciare l’intestazione insieme al relativo livello.
* Altre tecnologie per l’accessibilità possono modificare la visualizzazione di una pagina, utilizzando intestazioni codificate in modo da visualizzare una struttura o una visualizzazione alternativa.

## Editor del servizio query

Nell’editor del servizio query sono disponibili le seguenti funzioni di accessibilità:

* Il contrasto del colore nell’interfaccia utente dell’editor del servizio query soddisfa la conformità in materia di accessibilità.
* La navigazione da tastiera è supportata all’esterno dell’interfaccia utente dell’editor. L’interfaccia utente dell’editor è un mirroring del codice incorporato.

## Scheda Vista sistema in Origini e Destinazioni

Quando esplori la **[!UICONTROL Vista di sistema]** in Origini e Destinazioni, le seguenti funzionalità migliorano l&#39;accessibilità:

* **** Le schede si concentrano sulla prima scheda di connessione sorgente
   * **** Tabella per attivare il pulsante all’interno della scheda
   * Seleziona **Invio** per attivare il pulsante di chiamata all&#39;azione all&#39;interno della scheda
* Selezionando **Invio** sulla scheda di connessione vengono attivati anche altri dettagli nella barra a destra
   * Quando la barra a destra è attivata, lo stato attivo è impostato su tale area. **** La scheda si concentra su  **** Chiudi per il riquadro a barre di destra. Quando si seleziona **Tab**, lo stato attivo viene nuovamente spostato nel pannello della barra a destra
   * Se è presente più di una scheda di connessione sorgente, **Tab** passa attraverso le connessioni
   * Utilizzare i tasti freccia **su, giù, sinistra e destra)** per spostarsi all&#39;interno dell&#39;elenco delle origini
   * Seleziona **Tab** per impostare lo stato attivo sul pannello della barra a destra