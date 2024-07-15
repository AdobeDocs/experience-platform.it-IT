---
title: Creare una connessione Source Azure Event Hubs nell’interfaccia utente
description: Scopri come creare una connessione di origine Azure Event Hubs utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: 1256f0c76b29edad4808fc4be1d61399bfbae8fa
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Azure Event Hubs] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Azure Event Hubs] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Leggere questo tutorial per scoprire come creare un account [!DNL Azure Event Hubs] utilizzando l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Event Hubs] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine [!DNL Event Hubs], è necessario fornire i valori per le proprietà di connessione seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione standard]

| Credenziali | Descrizione |
| --- | --- |
| Nome chiave SAS | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| Chiave SAS | Chiave primaria dello spazio dei nomi [!DNL Event Hubs]. I `sasPolicy` a cui corrisponde `sasKey` devono avere `manage` diritti configurati affinché l&#39;elenco [!DNL Event Hubs] possa essere popolato. |
| Namespace | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |

>[!TAB Autenticazione SAS]

| Credenziali | Descrizione |
| --- | --- |
| Nome chiave SAS | Il nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| Chiave SAS | Chiave primaria dello spazio dei nomi [!DNL Event Hub]. I `sasPolicy` a cui corrisponde `sasKey` devono avere `manage` diritti configurati affinché l&#39;elenco [!DNL Event Hubs] possa essere popolato. |
| Namespace | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| Nome hub eventi | Inserisci il nome [!DNL Azure Event Hub]. Per ulteriori informazioni sui nomi di [!DNL Event Hub], leggere la [documentazione di Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub). |

>[!TAB Hub eventi Azure Active Directory Auth]

| Credenziali | Descrizione |
| --- | --- |
| ID tenant | ID tenant a cui desideri richiedere l’autorizzazione. L’ID tenant può essere formattato come GUID o come nome descrittivo. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| ID client | L&#39;ID applicazione assegnato alla tua app. Puoi recuperare questo ID dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| Valore segreto client | Segreto client utilizzato insieme all’ID client per autenticare l’app. Puoi recuperare il segreto client dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| Namespace | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |

Per ulteriori informazioni su [!DNL Azure Active Directory], leggere la [Guida di Azure sull&#39;utilizzo di Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!TAB Autenticazione Azure Active Directory con ambito hub eventi]

| Credenziali | Descrizione |
| --- | --- |
| ID tenant | ID tenant a cui desideri richiedere l’autorizzazione. L’ID tenant può essere formattato come GUID o come nome descrittivo. **Nota**: nell&#39;interfaccia [!DNL Microsoft Azure] l&#39;ID tenant viene indicato come &quot;ID directory&quot;. |
| ID client | L&#39;ID applicazione assegnato alla tua app. Puoi recuperare questo ID dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| Valore segreto client | Segreto client utilizzato insieme all’ID client per autenticare l’app. Puoi recuperare il segreto client dal portale [!DNL Microsoft Entra ID] in cui hai registrato [!DNL Azure Active Directory]. |
| Namespace | Spazio dei nomi di [!DNL Event Hub] a cui si sta effettuando l&#39;accesso. Uno spazio dei nomi [!DNL Event Hub] fornisce un contenitore di ambito univoco, in cui è possibile creare uno o più [!DNL Event Hubs]. |
| Nome hub eventi | Inserisci il nome [!DNL Azure Event Hub]. Per ulteriori informazioni sui nomi di [!DNL Event Hub], leggere la [documentazione di Microsoft](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub). |

Per ulteriori informazioni su [!DNL Azure Active Directory], leggere la [Guida di Azure sull&#39;utilizzo di Microsoft Entra ID](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application).

>[!ENDTABS]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Event Hubs] all&#39;Experience Platform.

## Connetti il tuo account [!DNL Event Hubs]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL Hub eventi di Azure]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con gli hub eventi di Azure selezionati.](../../../../images/tutorials/create/eventhub/catalog.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Connetti a Azure Event Hubs]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Event Hubs] che si desidera utilizzare, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![Elenco degli account di origine di Azure Event Hubs esistenti.](../../../../images/tutorials/create/eventhub/existing.png)

### Nuovo account

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Event Hubs]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]**, quindi specificare un nome e una descrizione facoltativa per il nuovo account [!DNL Event Hubs].

![Nuova interfaccia di creazione account per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/new.png)

>[!BEGINTABS]

>[!TAB Autenticazione standard]

Per creare un account [!DNL Event Hubs] con autenticazione standard, utilizzare il menu a discesa [!UICONTROL Autenticazione account], quindi selezionare **[!UICONTROL Autenticazione standard]**. Fornire quindi i valori per [!UICONTROL Nome chiave SAS], [!UICONTROL Chiave SAS] e [!UICONTROL Spazio dei nomi].

Dopo aver immesso le credenziali di autenticazione, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione standard per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/standard.png)

>[!TAB Autenticazione SAS]

Per creare un account [!DNL Event Hubs] con autenticazione SAS, utilizzare il menu a discesa [!UICONTROL Autenticazione account], quindi selezionare **[!UICONTROL Autenticazione SAS]**. Quindi, fornisci i valori per [!UICONTROL nome chiave SAS], [!UICONTROL chiave SAS], [!UICONTROL spazio dei nomi] e [!UICONTROL nome hub eventi].

Dopo aver immesso le credenziali di autenticazione, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![Interfaccia di autenticazione SAS per gli hub eventi di Azure.](../../../../images/tutorials/create/eventhub/sas.png)

>[!TAB Hub eventi Azure Active Directory Auth]

Per creare un account [!DNL Event Hubs] con l&#39;autenticazione di Azure Active Directory dell&#39;hub eventi, utilizzare il menu a discesa [!UICONTROL Autenticazione account], quindi selezionare **[!UICONTROL Azure Active Directory dell&#39;hub eventi]**. Quindi, fornisci i valori per [!UICONTROL ID tenant], [!UICONTROL ID client], [!UICONTROL Valore segreto client] e [!UICONTROL Spazio dei nomi].

![Autenticazione Azure Active Directory per l&#39;hub eventi Azure](../../../../images/tutorials/create/eventhub/active-directory.png)

>[!TAB Autenticazione Azure Active Directory con ambito hub eventi]

Per creare un account [!DNL Event Hubs] con autenticazione Azure Active Directory con ambito hub eventi, utilizzare il menu a discesa [!UICONTROL Autenticazione account], quindi selezionare **[!UICONTROL Azure Active Directory con ambito hub eventi]**. Quindi, fornisci i valori per [!UICONTROL ID tenant], [!UICONTROL ID client], [!UICONTROL Valore segreto client], [!UICONTROL Spazio dei nomi] e [!UICONTROL Nome hub eventi].

![Autenticazione di Azure Activity Directory con ambito hub eventi Azure](../../../../images/tutorials/create/eventhub/scoped.png)

>[!ENDTABS]


## Passaggi successivi

Seguendo questa esercitazione, hai connesso il tuo account [!DNL Event Hubs] a Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati dall&#39;archiviazione cloud in Experience Platform](../../dataflow/streaming/cloud-storage-streaming.md).
