---
keywords: Experience Platform;home;argomenti popolari;Azure Event Hubs;Event Hubs;azure event hub
solution: Experience Platform
title: Creare una connessione di origine degli hub eventi di Azure nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine Azure Event Hubs utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Creare un [!DNL Azure Event Hubs] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un [!DNL Azure Event Hubs] (in seguito denominati &quot;[!DNL Event Hubs]&quot;) connettore di origine utilizzando [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Event Hubs] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli le credenziali richieste

Per autenticare il tuo [!DNL Event Hubs] connettore di origine, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La chiave primaria della [!DNL Event Hubs] spazio dei nomi. Il `sasPolicy` che il `sasKey` corrisponde a deve avere `manage` diritti configurati per il [!DNL Event Hubs] elenco da compilare. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] si sta effettuando l&#39;accesso. |

Per ulteriori informazioni su questi valori, consulta [questo [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Connetti [!DNL Event Hubs] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Event Hubs] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella scheda sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Archiviazione cloud]** categoria, seleziona **[!UICONTROL Hub eventi di Azure]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore Hub eventi.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Il **[!UICONTROL Connetti a Azure Event Hubs]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Event Hubs] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Event Hubs] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai connesso [!DNL Event Hubs] account a [!DNL Platform]. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
