---
title: Collegare l’account PathFactory all’Experience Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account PathFactory a Experienci Platform tramite l’interfaccia utente.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# Connetti [!DNL PathFactory] da Experience Platform tramite l’interfaccia utente

Questo tutorial descrive come collegare [!DNL PathFactory] I dati di visitatori, sessioni e visualizzazioni di pagina vengono inviati a Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di un [!DNL PathFactory] account, puoi saltare il resto di questo documento e passare all’esercitazione su [Experience Platform dei dati di automazione marketing tramite l’interfaccia utente di](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste {#gather-credentials}

Per accedere all’account PathFactory sulla piattaforma, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Nome utente | Nome utente dell&#39;account PathFactory. Questo è essenziale per identificare l’account nel sistema. |
| Password | La password associata al tuo account PathFactory. Assicurati che sia protetto per evitare accessi non autorizzati. |
| Dominio | Il dominio associato al tuo account PathFactory. In genere si riferisce all’identificatore univoco all’interno dell’URL PathFactory. |
| Token di accesso | Token univoco utilizzato per l’autenticazione API per garantire una comunicazione sicura tra i sistemi e PathFactory. |
| Endpoint API | Endpoint API specifici per l’accesso ai dati: visitatori, sessioni e visualizzazioni di pagina. Ogni endpoint corrisponde a set di dati diversi che è possibile recuperare. **Nota:** Questi sono predefiniti da [!DNL PathFactory] e sono specifici per i dati a cui intendi accedere: <ul><li>**Endpoint visitatori**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Endpoint sessioni**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpoint visualizzazioni pagina**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Per istruzioni dettagliate su come proteggere e utilizzare le credenziali e per informazioni su come ottenere e aggiornare il token di accesso, visita [Centro assistenza PathFactory](https://support.pathfactory.com/categories/adobe/). Questa risorsa offre guide complete sulla gestione delle credenziali e sulla garanzia di un’integrazione API efficace e sicura.


## Connetti [!DNL PathFactory] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] In vengono visualizzate diverse origini supportate da Experienci Platform.

È possibile selezionare la categoria appropriata dall&#39;elenco delle categorie. Puoi anche utilizzare la barra di ricerca per filtrare in base a un’origine specifica.

Sotto [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL PathFactory]** e quindi seleziona **[!UICONTROL Configurazione]**.

![Catalogo delle origini con l&#39;origine PathFactory selezionata.](../../../../images/tutorials/create/pathfactory/catalog.png)

Il **[!UICONTROL Connetti a PathFactory]** viene visualizzata. In questa pagina è possibile creare un nuovo account o utilizzare un account esistente.

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome per l&#39;account, una descrizione facoltativa e le credenziali di autenticazione corrispondenti al tuo [!DNL PathFactory] account.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account in cui è possibile autenticare un nuovo account per PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Account esistente

Se disponi già di un account, seleziona **[!UICONTROL Account esistente]** quindi seleziona l’account che desideri utilizzare dall’elenco visualizzato.

![L&#39;interfaccia account esistente in cui è possibile effettuare la selezione da un elenco di account PathFactory esistenti.](../../../../images/tutorials/create/pathfactory/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione tra [!DNL PathFactory] account e Experience Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per portare in Experience Platform i dati di automazione marketing](../../dataflow/marketing-automation.md).
