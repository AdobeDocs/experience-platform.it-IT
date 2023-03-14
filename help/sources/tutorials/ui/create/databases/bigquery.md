---
keywords: Experience Platform;home;argomenti popolari;Google Big Query;google big query;GBQ;gbq
solution: Experience Platform
title: Creare una connessione Google Big Query Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Google Big Query utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Creare un [!DNL Google Big Query] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Google Big Query] tramite l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Google BigQuery] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Google BigQuery] su Platform, è necessario fornire i seguenti valori di autenticazione OAuth 2.0:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | ID progetto predefinito [!DNL Google BigQuery] progetto su cui eseguire la query. |
| `clientID` | Valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l’accesso a [!DNL Google BigQuery]. |

Per ulteriori informazioni su questi valori, consulta [questo [!DNL Google BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Connetti il tuo account Google BigQuery

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Database] categoria, seleziona **[!UICONTROL BigQuery Google]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Il **[!UICONTROL Connetti a Google Big Query]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Google BigQuery] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Google BigQuery] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/google-big-query/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Google BigQuery] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/databases.md).
