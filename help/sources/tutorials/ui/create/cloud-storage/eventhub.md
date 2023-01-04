---
keywords: Experience Platform;home;argomenti popolari;hub eventi di Azure;hub eventi;hub eventi di Azure
solution: Experience Platform
title: Creare una connessione di origine degli hub eventi di Azure nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Azure Event Hubs utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# Crea un [!DNL Azure Event Hubs] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un [!DNL Azure Event Hubs] (in appresso denominato &quot;[!DNL Event Hubs]&quot;) connettore di origine con [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Event Hubs] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli credenziali richieste

Per autenticare il [!DNL Event Hubs] connettore di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La chiave primaria del [!DNL Event Hubs] spazio dei nomi. La `sasPolicy` che `sasKey` corrisponde a `manage` diritti configurati per [!DNL Event Hubs] elenco da compilare. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] stai accedendo. |

Per ulteriori informazioni su questi valori, consulta [questo [!DNL Event Hubs] documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Collega il tuo [!DNL Event Hubs] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Event Hubs] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** In viene visualizzata una varietà di origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Archiviazione cloud]** categoria, seleziona **[!UICONTROL Hub eventi di Azure]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore Event Hubs.

![](../../../../images/tutorials/create/eventhub/catalog.png)

La **[!UICONTROL Connetti agli hub eventi di Azure]** viene visualizzata la finestra di dialogo . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Event Hubs] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Event Hubs] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai collegato il tuo [!DNL Event Hubs] account a [!DNL Platform]. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
