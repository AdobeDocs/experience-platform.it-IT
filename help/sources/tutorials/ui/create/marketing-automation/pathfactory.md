---
title: Collegare l’account PathFactory all’Experience Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account PathFactory a Experience Platform tramite l’interfaccia utente.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---

# Connetti il tuo account [!DNL PathFactory] ad Experience Platform tramite l&#39;interfaccia utente

Questo tutorial descrive come collegare i dati di visitatori, sessioni e visualizzazioni di pagina di [!DNL PathFactory] a Adobe Experience Platform tramite l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL PathFactory], puoi saltare il resto di questo documento e passare all&#39;esercitazione su [come Experience Platform dei dati di automazione marketing tramite l&#39;interfaccia utente](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste {#gather-credentials}

Per accedere all’account PathFactory sulla piattaforma, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Nome utente | Nome utente dell&#39;account PathFactory. Questo è essenziale per identificare l’account nel sistema. |
| Password | La password associata al tuo account PathFactory. Assicurati che sia protetto per evitare accessi non autorizzati. |
| Dominio | Il dominio associato al tuo account PathFactory. In genere si riferisce all’identificatore univoco all’interno dell’URL PathFactory. |
| Token di accesso | Token univoco utilizzato per l’autenticazione API per garantire una comunicazione sicura tra i sistemi e PathFactory. |
| Endpoint API | Endpoint API specifici per l’accesso ai dati: visitatori, sessioni e visualizzazioni di pagina. Ogni endpoint corrisponde a set di dati diversi che è possibile recuperare. **Nota:** questi sono predefiniti da [!DNL PathFactory] e sono specifici per i dati a cui intendi accedere: <ul><li>**Endpoint visitatori**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Endpoint sessioni**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpoint visualizzazioni pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Per istruzioni dettagliate su come proteggere e utilizzare le credenziali e per informazioni su come ottenere e aggiornare il token di accesso, visitare il [Centro supporto PathFactory](https://support.pathfactory.com/categories/adobe/). Questa risorsa offre guide complete sulla gestione delle credenziali e sulla garanzia di un’integrazione API efficace e sicura.


## Connetti il tuo account [!DNL PathFactory]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Il [!UICONTROL catalogo] presenta diverse origini supportate da Experience Platform.

È possibile selezionare la categoria appropriata dall&#39;elenco delle categorie. Puoi anche utilizzare la barra di ricerca per filtrare in base a un’origine specifica.

Nella categoria [!UICONTROL Marketing automation], selezionare **[!UICONTROL PathFactory]**, quindi **[!UICONTROL Set up]**.

![Catalogo origini con origine PathFactory selezionata.](../../../../images/tutorials/create/pathfactory/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a PathFactory]**. In questa pagina è possibile creare un nuovo account o utilizzare un account esistente.

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome per il tuo account, una descrizione facoltativa e le credenziali di autenticazione corrispondenti al tuo account [!DNL PathFactory].

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account in cui è possibile autenticare un nuovo account per PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Account esistente

Se disponi già di un account, seleziona **[!UICONTROL Account esistente]**, quindi seleziona l&#39;account che desideri utilizzare dall&#39;elenco visualizzato.

![Interfaccia account esistente in cui è possibile effettuare la selezione da un elenco di account PathFactory esistenti.](../../../../images/tutorials/create/pathfactory/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione tra il tuo account [!DNL PathFactory] e l&#39;Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per inserire i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).
