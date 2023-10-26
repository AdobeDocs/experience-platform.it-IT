---
title: Creare una connessione di origine degli hub eventi di Azure nell’interfaccia utente
description: Scopri come creare una connessione di origine Azure Event Hubs utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1680cc4e1d5c1576767053a74e560bc2eb8c24cb
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# Creare un [!DNL Azure Event Hubs] connessione sorgente nell’interfaccia utente

>[!IMPORTANT]
>
>Il [!DNL Azure Event Hubs] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive come creare un [!DNL Azure Event Hubs] tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Event Hubs] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli le credenziali richieste

Per autenticare il tuo [!DNL Event Hubs] connettore di origine, è necessario fornire i valori per le seguenti proprietà di connessione:

>[!BEGINTABS]

>[!TAB Autenticazione standard]

| Credenziali | Descrizione |
| --- | --- |
| Nome chiave SAS | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| Chiave SAS | La chiave primaria della [!DNL Event Hubs] spazio dei nomi. Il `sasPolicy` che il `sasKey` corrisponde a deve avere `manage` diritti configurati per il [!DNL Event Hubs] elenco da compilare. |
| Namespace | Lo spazio dei nomi del [!DNL Event Hubs] si sta effettuando l&#39;accesso. Un [!DNL Event Hubs] namespace fornisce un contenitore di ambito univoco, nel quale è possibile creare uno o più [!DNL Event Hubs]. |

>[!TAB Autenticazione SAS]

| Credenziali | Descrizione |
| --- | --- |
| Nome chiave SAS | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| Chiave SAS | La chiave primaria della [!DNL Event Hubs] spazio dei nomi. Il `sasPolicy` che il `sasKey` corrisponde a deve avere `manage` diritti configurati per il [!DNL Event Hubs] elenco da compilare. |
| Namespace | Lo spazio dei nomi del [!DNL Event Hubs] si sta effettuando l&#39;accesso. Un [!DNL Event Hubs] namespace fornisce un contenitore di ambito univoco, nel quale è possibile creare uno o più [!DNL Event Hubs]. |
| Nome hub eventi | Il nome per il [!DNL Event Hubs] sorgente. |

>[!ENDTABS]

Per ulteriori informazioni su questi valori, consulta [questo documento Hub eventi](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Event Hubs] da Experience Platform.

## Connetti [!DNL Event Hubs] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Hub eventi di Azure]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con Azure Event Hub selezionato.](../../../../images/tutorials/create/eventhub/catalog.png)

Il **[!UICONTROL Connetti a Azure Event Hubs]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Event Hubs] account che desideri utilizzare, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Elenco degli account di origine di Azure Event Hubs esistenti.](../../../../images/tutorials/create/eventhub/existing.png)

### Nuovo account

>[!TIP]
>
>Una volta creato, non è possibile modificare il tipo di autenticazione di un [!DNL Event Hubs] connessione di base. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Event Hubs] account.

![La nuova interfaccia per la creazione di account per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Autenticazione standard]

Per creare un [!DNL Event Hubs] account con autenticazione standard, seleziona **[!UICONTROL Autenticazione standard]** e quindi fornisci i valori per [!UICONTROL Nome chiave SAS], [!UICONTROL Chiave SAS], e [!UICONTROL Namespace].

Dopo aver immesso le credenziali di autenticazione, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione standard per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Autenticazione SAS]

Per creare un [!DNL Event Hubs] account con autenticazione SAS, selezionare **[!UICONTROL Autenticazione SAS]** e quindi fornisci i valori per [!UICONTROL Nome chiave SAS], [!UICONTROL Chiave SAS], [!UICONTROL Namespace], e [!UICONTROL Nome hub eventi].

Dopo aver immesso le credenziali di autenticazione, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione SAS per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/sas.png)

>[!ENDTABS]


## Passaggi successivi

Seguendo questa esercitazione, hai connesso [!DNL Event Hubs] da Experience Platform. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare in Experience Platform i dati dall’archiviazione cloud](../../dataflow/streaming/cloud-storage-streaming.md).
