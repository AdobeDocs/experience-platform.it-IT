---
keywords: Experience Platform;home;argomenti popolari;
title: (Beta) Creare una connessione sorgente Adobe Workfront nell’interfaccia utente
description: Questo tutorial illustra i passaggi necessari per creare una connessione di origine Adobe Workfront che consenta di trasferire i dati Workfront a Adobe Experience Platform tramite l’interfaccia utente.
exl-id: f82e852a-c9d1-4ecc-bc54-2b39d3b4cc1e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 1%

---

# (Beta) Creare una connessione sorgente Adobe Workfront nell’interfaccia utente

>[!NOTE]
>
>Il codice sorgente di Adobe Workfront è in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial illustra i passaggi necessari per creare una connessione di origine Adobe Workfront che consenta di trasferire i dati Workfront a Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

>[!IMPORTANT]
>
>Devi essere configurato come amministratore in Adobe Admin Console per accedere all’origine Workfront.

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
* [Profilo cliente in tempo reale](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Creare una connessione sorgente Workfront nell’interfaccia utente

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini che possono essere utilizzate per creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. È inoltre possibile utilizzare la barra di ricerca per limitare le origini visualizzate.

Sotto **[!UICONTROL applicazioni Adobe]** categoria, seleziona **[!UICONTROL Adobe Workfront]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con l’origine Adobe Workfront evidenziata.](../../../../images/tutorials/create/workfront/catalog.png)

## Selezionare i dati

Il [!UICONTROL Seleziona dati] viene visualizzato il passaggio. In questo caso, devi fornire i valori per il sottodominio Workfront e Datalane. Il sottodominio Workfront è lo stesso URL utilizzato per accedere all’istanza di Workfront, ad esempio `https://acme.workfront.com/`, mentre il datalane rappresenta l’ambiente workfront che desideri utilizzare.

Dopo aver aggiunto il sottodominio e il datalane, seleziona **[!UICONTROL Successivo]**.

![La pagina seleziona dati con valori segnaposto per sottodominio e datalane.](../../../../images/tutorials/create/workfront/select-data.png)

## Fornisci i dettagli del flusso di dati

Il passaggio dei dettagli del flusso di dati consente di fornire un nome e una descrizione facoltativa per il flusso di dati. Durante questo passaggio, puoi anche abbonarti agli avvisi per ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta il tutorial su [abbonamento agli avvisi nell’interfaccia utente delle sorgenti](../../alerts.md).

Dopo aver fornito i dettagli del flusso di dati e configurato le impostazioni di avviso desiderate, seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli del flusso di dati con informazioni su nome del flusso di dati, descrizione e notifiche di avviso](../../../../images/tutorials/create/workfront/dataflow-detail.png)

## Revisione

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Pagina di revisione che riepiloga le informazioni sulla connessione.](../../../../images/tutorials/create/workfront/review.png)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive sull’origine di Workfront.

### Schema evento di modifica Workfront

In Platform, i dati di Workfront sono rappresentati come dati di record di serie temporali, dove ogni riga dei dati presenta una marca temporale che indica quando si è verificato l’evento e gli attributi correlati a tale evento.

Durante l’installazione, viene creato uno schema denominato Workfront Change Events from Flow (Eventi di modifica dal flusso).

| Campo schema | Descrizione |
| --- | --- |
| `timestamp` | Ora in cui si è verificato l&#39;evento selezionato. Il timestamp è rappresentato nel fuso orario GTM. |
| `_workfront.objectType` | Il tipo di oggetto. I valori disponibili possono includere `project`, `task`, `portfolio`e altri, a seconda dell’oggetto modificato o creato. |
| `_workfront.objectID` | ID corrispondente al tipo di oggetto. |
| `_workfront.created` | Questo valore è impostato su `1` se l’evento rappresenta la creazione di un oggetto. |
| `_workfront.deleted` | Questo valore è impostato su `1` se l’oggetto viene eliminato. |
| `_worfkront.updated` | Questo valore è impostato su `1` se l’oggetto viene aggiornato. |
| `_workfront.completed` | Questo valore è impostato su `1` se l’oggetto è contrassegnato come completato. |
| `_workfront.parentObjectType` | (Facoltativo) Il tipo di oggetto che corrisponde all&#39;elemento padre dell&#39;oggetto. |
| `_workfront.parentID` | ID dell&#39;oggetto padre. |
| `_workfront.customData` | Mappa di tutti i campi modulo personalizzato e dei relativi valori compilata durante l’evento. |

>[!IMPORTANT]
>
>Vengono compilati solo gli attributi modificati o creati come parte di un evento. Ad esempio, se modifichi solo il nome dell’oggetto, gli unici campi che verranno compilati sono:<ul><li>`timestamp`</li><li>`_workfront.update (=1)`</li><li>`_workfront.objectType`</li><li>`_workfront.objectID`</li><li>`_workfront.objectName`</li></ul>

## Passaggi successivi

Seguendo questa esercitazione, ora hai creato un flusso di dati per portare i tuoi dati da Workfront a Experience Platform. Ora puoi utilizzare servizi come [Servizio query](../../../../../query-service/home.md) per eseguire ulteriori analisi sui dati. Per ulteriori informazioni su Workfront, consulta [Panoramica di Workfront](../../../../connectors/adobe-applications/workfront.md).
