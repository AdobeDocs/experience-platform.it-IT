---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;grafici XDM
title: Soluzioni di accessibilità personalizzate per Experience Platform
topic-legacy: guide
type: Documentation
description: Ulteriori informazioni sulle soluzioni di accessibilità personalizzate all'interno dell'interfaccia utente di Adobe Experience Platform.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 7f4202c9c4a132ed9d74c495f6608357eac8003f
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 0%

---

# Soluzioni di accessibilità personalizzate per Experience Platform

Adobe Experience Platform viene continuamente migliorato per soddisfare le esigenze di tutti i tipi di utenti e aderire agli standard mondiali che includono persone con disabilità visive, uditive, di mobilità o di altro tipo. Questo documento delinea soluzioni di accessibilità personalizzate all&#39;interno dell&#39;interfaccia utente di Experience Platform.

## Panoramica della pagina principale e dell’interfaccia utente

L’interfaccia utente di Experience Platform soddisfa i rapporti di contrasto richiesti per i normali componenti di testo, grafica e interfaccia utente. I colori dell’interfaccia utente sono stati scelti anche per supportare l’accessibilità per tutti gli utenti, compresi quelli con disabilità visive.

In Platform, è possibile utilizzare una tastiera anche per gli elementi dell’interfaccia utente cliccabili o utilizzabili con un puntatore. Questo include la navigazione a sinistra, lettori video, tabelle e altro ancora.

L’Experience Platform si impegna a soddisfare gli standard internazionali di accessibilità, inclusi gli standard web WAI-ARIA (Accessibility Guidelines) di livello 2.1 e A e AA (Livello A e Livello AA) e WAI (Web Accessibility Initiative - Accessible Rich Internet Applications).

![Pagina principale dell’interfaccia utente di Adobe Experience Platform.](images/homepage.png)

## Pannello di navigazione a sinistra

La navigazione a sinistra nell’interfaccia utente di Experience Platform è accessibile da tastiera e offre un contrasto del colore in stati di normale, passaggio del mouse e selezione che soddisfa gli standard di accessibilità.

Dalla schermata Home, gli utenti possono passare al menu di navigazione a sinistra. Selezione **Maiusc+Tab** restituisce l&#39;utente alla schermata iniziale.

![L&#39;Experience Platform ha lasciato la navigazione.](images/left-navigation-select.png)

Con la navigazione a sinistra in focus, **Scheda** consente agli utenti di espandere e comprimere l’interazione. La possibilità di espandere o comprimere la navigazione a sinistra viene attivata con **Invio (Invio)**.

![La navigazione a sinistra dell&#39;Experience Platform è compressa.](images/left-navigation-collapse.png)

Con la navigazione a sinistra in focus, i tasti freccia su e giù navigano su ogni elemento nella navigazione e circondano continuamente (in altre parole, lo stato attivo non si sposta via finché l&#39;utente non si sposta dalla navigazione a sinistra). Lo stato attivo viene visualizzato per gli elementi di navigazione quando selezionati. La selezione corrente viene visualizzata con un&#39;evidenziazione e un testo con grassetto. Quando si seleziona un elemento di navigazione a sinistra, **Invio (Invio)** apre l’elemento dell’interfaccia utente selezionato nel pannello di destra, tuttavia lo stato attivo rimane nella navigazione a sinistra fino a quando l’utente non si sposta.

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
| Riproduzione e pausa | Scheda<br/>Barra spaziatrice | Utilizzo **Scheda** per attivare il pulsante di riproduzione. **Barra spaziatrice** avvia la riproduzione del video e mette in pausa la riproduzione del video. |
| Scorrevole | Scheda<br/>Freccia sinistra<br/>Freccia destra | Durante la riproduzione del video, utilizza **Scheda** per attivare lo scorrimento. Con la gomma a fuoco, **tasti freccia sinistra e destra** saltare la riproduzione video rispettivamente avanti e indietro di 5 secondi. |
| Disattiva audio | Scheda<br/>Barra spaziatrice | Utilizzo **Scheda** per attivare l&#39;elemento volume muto. Utilizzo **barra spaziatrice** per disattivare o disattivare la riproduzione video. |
| Volume | Scheda<br/>Freccia sinistra<br/>Freccia destra | Utilizzo **Scheda** per concentrarsi sull&#39;elemento volume. **Tasti freccia sinistra e destra** spostare rispettivamente il volume in alto e in basso. |
| [!UICONTROL Sottotitoli] (&quot;cc&quot;) | Scheda<br/>Invio<br/>Freccia Su<br/>Freccia giù | **Scheda** a [!UICONTROL Sottotitoli] (&quot;cc&quot;). Utilizzo **Invio** per aprire il menu e **tasti freccia su e giù** per selezionare una lingua per le didascalie. **Invio** conferma la selezione. |
| [!UICONTROL Qualità] | Scheda<br/>Invio<br/>Freccia Su<br/>Freccia giù | Utilizzo **Scheda** per mettere a fuoco [!UICONTROL Qualità] elemento. Utilizzo **Invio** per aprire il menu e **tasti freccia su e giù** per selezionare la qualità video. **Invio** conferma la selezione. |
| Schermo intero | Scheda<br/>Barra spaziatrice o Invio<br/>Esc | Utilizzo **Scheda** per attivare l’elemento a schermo intero. Utilizzo **barra spaziatrice o ingresso** per attivare la visualizzazione a schermo intero. **Esc** (&quot;esc&quot;) esce dalla modalità a schermo intero. |
| Chiudi | Scheda<br/>Barra spaziatrice o Invio | Utilizzo **Scheda** per attivare il pulsante di chiusura. Utilizzo **barra spaziatrice o ingresso** per uscire dalla finestra di dialogo video. |

>[!NOTE]
>
>In qualsiasi momento durante la riproduzione, il tasto Esc (&quot;esc&quot;) può essere utilizzato per chiudere la finestra di dialogo video incorporata.

![La finestra di dialogo video incorporata con i numeri che identificano gli elementi di navigazione da tastiera.](images/video-dialog.png)

## Trascinamento file

Ad Experience Platform, tutte le zone di trascinamento e rilascio per la selezione dei file sono accessibili da tastiera. Utilizzo **Scheda** evidenziare **[!UICONTROL Scegliere i file]** e utilizzando **Entra o barra spaziatrice** per selezionarlo, richiama l&#39;interfaccia utente del sistema operativo per la selezione dei file.

Dopo il caricamento di un file, l’icona Elimina diventa accessibile da tastiera per rimuovere il file selezionato e caricarne uno nuovo. Gli utenti possono utilizzare **Scheda** per concentrarti sull’icona Elimina e **Entra o barra spaziatrice** per selezionarlo. Una volta rimosso il file, **[!UICONTROL Scegliere i file]** è automaticamente a fuoco e può essere selezionato.

In alternativa, se il file caricato non è nel formato corretto, viene visualizzata un&#39;icona di errore insieme a un messaggio di errore e alla **[!UICONTROL Scegliere i file]** pulsante attivo e selezionabile.

![Zona di trascinamento file con messaggio di errore e pulsante di selezione file attivo.](images/drag-and-drop.png)

Se si utilizza un mouse per selezionare la zona di trascinamento, viene richiamata anche l’interfaccia utente per la selezione dei file. In alternativa, l’utente può selezionare un file e trascinarlo nella zona per iniziare il caricamento.

![Zona di trascinamento e rilascio del file, quando un utente del mouse trascina un file nella zona.](images/drag-and-drop-mouse-over.png)

## Sfoglia tabella

Tutte le tabelle nell’interfaccia utente di Experience Platform sono accessibili da tastiera. È possibile navigare e interagire con righe e colonne di una tabella tramite una serie di scelte rapide da tastiera:

* Dall’intestazione della tabella, utilizza il **freccia giù** per sfogliare la tabella. Le intestazioni di tabella sono selezionabili quando si naviga tramite **Scheda** e puoi modificare l’ordinamento utilizzando **barra spaziatrice**.
* **Tasti freccia Su e Giù** si sposta in alto o in basso tra le righe della tabella.
* Quando una riga è selezionata o messa a fuoco, utilizzando **Invio** nella riga sono riportati i dettagli nella barra a destra.
* Quando una riga è selezionata o messa a fuoco, utilizza **tasti freccia** per spostarsi all&#39;interno di ogni elemento della riga.
* Utilizzo **Invio** per selezionare un elemento nella riga. Gli utenti con assistenti vocali ricevono un avviso se è necessario aprire una nuova finestra.
* Quando si esegue lo zoom al 200% o più, è possibile visualizzare la **ispettore ferroviario** mentre la barra a destra si espande per fornire più spazio di visualizzazione alla tabella.

![L’icona dell’ispettore della barra è attiva quando un utente raggiunge lo zoom del 200%.](images/rail-inspector.png)

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

* L’Editor di schema supporta la navigazione da tastiera, incluso l’utilizzo di **Scheda** per navigare tra gli elementi dell’interfaccia utente.
* **Scheda** entra nel campo di ricerca, quindi nella struttura dello schema.
* La struttura dello schema supporta l’utilizzo di tasti freccia per spostarsi all’interno dell’interfaccia utente della struttura dello schema
   * **Frecce Su e Giù** può essere utilizzato per attraversare l’albero.
   * **Frecce sinistra e destra** può essere utilizzato per espandere e comprimere i nodi o per spostarsi tra le azioni in linea nella struttura dello schema.
* **Invio (Invio)** attiva i dettagli dei singoli nodi nel pannello dei dettagli a destra.
* La **Pagina principale** viene ripristinata la parte superiore della struttura.
* La **Fine** passa alla parte inferiore della struttura.
* La struttura dello schema include anche le etichette ARIA per gli assistenti vocali.

## Interfaccia utente di Generatore di segmenti

Quando utilizzi l’interfaccia utente del Generatore di segmenti per creare, modificare e interagire con i segmenti all’interno di Experience Platform, le seguenti funzioni migliorano l’accessibilità:

* L’interfaccia utente del Generatore di segmenti è accessibile tramite la navigazione da tastiera.
* Gli assistenti vocali devono riconoscere i tag di markup per le intestazioni e possono annunciare l’intestazione insieme al relativo livello.
* Altre tecnologie per l’accessibilità possono modificare la visualizzazione di una pagina, utilizzando intestazioni codificate in modo da visualizzare una struttura o una visualizzazione alternativa.

È ora possibile comprimere o espandere le barre sinistra e destra dell’area di lavoro del generatore di segmenti per ottenere più spazio sullo schermo. Questa funzione è particolarmente utile in quanto offre funzionalità complete con zoom del 200%.

![Area di lavoro del generatore di segmenti con i widget di divulgazione della barra a sinistra e a destra evidenziati.](images/left-right-rail-expandables.png)

## Editor del servizio query

Nell’editor del servizio query sono disponibili le seguenti funzioni di accessibilità:

* Il contrasto del colore nell’interfaccia utente dell’editor del servizio query soddisfa la conformità in materia di accessibilità.
* La navigazione da tastiera è supportata all’esterno dell’interfaccia utente dell’editor. L’interfaccia utente dell’editor è un mirroring del codice incorporato.

## Scheda Vista sistema in Origini e Destinazioni

Quando esplori il **[!UICONTROL Vista di sistema]** in Origini e destinazioni, le seguenti funzionalità migliorano l’accessibilità:

* **Scheda** imposta lo stato attivo sulla prima scheda di connessione sorgente
   * **Scheda** di nuovo per mettere a fuoco il pulsante all&#39;interno della scheda
   * Seleziona **Invio** per attivare il pulsante di chiamata all&#39;azione all&#39;interno della scheda
* Selezione **Invio** sulla scheda di connessione vengono inoltre attivati ulteriori dettagli nella barra a destra
   * Quando la barra a destra è attivata, lo stato attivo è impostato su tale area. **Scheda** si concentra su **Chiudi** per il riquadro a destra. Selezione **Scheda** sposta di nuovo lo stato attivo nel pannello della barra a destra
   * Se sono presenti più schede di connessione sorgente, **Scheda** passa attraverso le connessioni
   * Utilizzo **tasti freccia (su, giù, sinistra e destra)** per spostarsi nell&#39;elenco delle origini
   * Seleziona **Scheda** per attivare il pannello a destra
