---
keywords: Experience Platform;home;argomenti popolari;Google Big Query;Google big query;GBQ;gbq
solution: Experience Platform
title: Creare una connessione Google Big Query Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Google Big Query utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Google Big Query] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Google BigQuery] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce passaggi per la creazione di un connettore di origine [!DNL Google Big Query] (in seguito denominato &quot;BigQuery&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione BigQuery valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account BigQuery su [!DNL Platform], devi fornire i seguenti valori di autenticazione OAuth 2.0:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | ID del progetto [!DNL BigQuery] predefinito su cui eseguire la query. |
| `clientID` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Il valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |

Per ulteriori informazioni su questi valori, consulta [questo documento BigQuery](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Connetti il tuo account Google BigQuery

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account BigQuery a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Google Big Query]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore BigQuery.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google Big Query]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali BigQuery. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account BigQuery con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account GBQ. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
