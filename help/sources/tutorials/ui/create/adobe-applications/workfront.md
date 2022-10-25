---
keywords: Experience Platform;home;argomenti popolari;
title: (Beta) Creare una connessione sorgente Adobe Workfront nell’interfaccia utente
description: Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente Adobe Workfront per trasferire i dati di Workfront a Adobe Experience Platform tramite l’interfaccia utente di .
source-git-commit: 1af0863766e29c599e02f2a553d237bc62f455d2
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# (Beta) Creare una connessione sorgente Adobe Workfront nell’interfaccia utente

>[!NOTE]
>
>La sorgente Adobe Workfront è in versione beta. Consulta la sezione [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente Adobe Workfront per trasferire i dati di Workfront a Adobe Experience Platform tramite l’interfaccia utente di .

## Introduzione

>[!IMPORTANT]
>
>Devi essere configurato come amministratore in Adobe Admin Console per accedere all’origine Workfront.

Questa esercitazione richiede una comprensione approfondita dei seguenti componenti dell&#39;Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
* [Profilo cliente in tempo reale](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

## Creare una connessione sorgente Workfront nell’interfaccia utente

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] visualizza una varietà di sorgenti che possono essere utilizzate per creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. Puoi anche usare la barra di ricerca per limitare le sorgenti visualizzate.

Sotto la **[!UICONTROL Applicazioni di Adobe]** categoria, seleziona **[!UICONTROL Adobe Workfront]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle sorgenti con la sorgente Adobe Workfront evidenziata.](../../../../images/tutorials/create/workfront/catalog.png)

## Seleziona dati

La [!UICONTROL Seleziona dati] viene visualizzato il passaggio . In questo caso, devi fornire valori per il sottodominio Workfront e per il Datalane. Il sottodominio Workfront è lo stesso URL utilizzato per accedere all’istanza Workfront, ad esempio `https://acme.workfront.com/`, mentre il datalane rappresenta l’ambiente principale da utilizzare.

Dopo aver aggiunto il sottodominio e il datalane, seleziona **[!UICONTROL Successivo]**.

![La pagina di selezione dei dati con i valori segnaposto per il sottodominio e il datalane.](../../../../images/tutorials/create/workfront/select-data.png)

## Fornire i dettagli del flusso di dati

Il passaggio dei dettagli del flusso di dati ti consente di fornire un nome e una descrizione facoltativa per il flusso di dati. Durante questo passaggio, puoi anche effettuare la sottoscrizione a avvisi per ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, visita l’esercitazione su [iscrizione agli avvisi nell’interfaccia utente delle sorgenti](../../alerts.md).

Dopo aver fornito i dettagli del flusso di dati e configurato le impostazioni di avviso desiderate, seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli del flusso di dati con informazioni su nome, descrizione e notifiche di avviso del flusso di dati](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Revisione

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno del file di origine.
* **[!UICONTROL Assegna set di dati e campi mappa]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![Pagina di revisione che riepiloga le informazioni sulla connessione.](../../../../images/tutorials/create/workfront/review.png)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sull’origine Workfront.

### Schema eventi di modifica Workfront

I dati Workfront in Platform sono rappresentati come dati di record relativi alle serie temporali, in cui ogni riga nei dati presenta una marca temporale che viene visualizzata quando si è verificato l’evento e gli attributi correlati a tale evento.

Durante la configurazione, viene creato uno schema denominato Workfront Change Events from Flow.

| Campo schema | Descrizione |
| --- | --- |
| `timestamp` | L&#39;ora in cui si è verificato l&#39;evento selezionato. La marca temporale è rappresentata nel fuso orario GTM. |
| `_workfront.objectType` | Tipo di oggetto. I valori disponibili possono includere `project`, `task`, `portfolio`, e altri, a seconda dell’oggetto modificato o creato. |
| `_workfront.objectID` | L&#39;ID che corrisponde al tipo di oggetto. |
| `_workfront.created` | Questo valore è impostato su `1` se l&#39;evento rappresenta una creazione di oggetti. |
| `_workfront.deleted` | Questo valore è impostato su `1` se l’oggetto viene eliminato. |
| `_worfkront.updated` | Questo valore è impostato su `1` se l’oggetto viene aggiornato. |
| `_workfront.completed` | Questo valore è impostato su `1` se l’oggetto è contrassegnato come completato. |
| `_workfront.parentObjectType` | (Facoltativo) Il tipo di oggetto che corrisponde al padre dell&#39;oggetto. |
| `_workfront.parentID` | ID dell&#39;oggetto principale. |
| `_workfront.customData` | Una mappa di tutti i campi modulo personalizzati e dei valori compilati durante l’evento. |

>[!IMPORTANT]
>
>Vengono compilati solo gli attributi modificati o creati come parte di un evento. Ad esempio, se si modifica solo il nome dell’oggetto, gli unici campi da compilare sono:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Passaggi successivi

Seguendo questa esercitazione, ora hai creato un flusso di dati per riportare in Experience Platform i tuoi dati da Workfront. Ora puoi utilizzare servizi come [Servizio query](../../../../../query-service/home.md) per eseguire ulteriori analisi sui dati. Per ulteriori informazioni su Workfront, consulta la sezione [Panoramica di Workfront](../../../../connectors/adobe-applications/workfront.md).