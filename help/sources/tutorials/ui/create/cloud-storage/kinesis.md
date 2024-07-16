---
title: Creare una connessione Amazon Kinesis Source nell’interfaccia utente
description: Scopri come creare una connessione sorgente Amazon Kinesis utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Amazon Kinesis] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL Amazon Kinesis] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un connettore di origine [!DNL Amazon Kinesis] (di seguito [!DNL "Kinesis"]) tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Kinesis] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine [!DNL Kinesis], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID della chiave di accesso per l&#39;account [!DNL Kinesis]. |
| `Secret access key` | Chiave di accesso segreta per l&#39;account [!DNL Kinesis]. |
| `region` | L’area geografica del server AWS. |

Per ulteriori informazioni su questi valori, fare riferimento a [questo [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Connetti il tuo account [!DNL Kinesis]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Kinesis] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Archiviazione cloud]**, seleziona **[!UICONTROL Amazon Kinesis]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL Kinesis].

![](../../../../images/tutorials/create/kinesis/catalog.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Connetti ad Amazon Kinesis]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Kinesis]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/kinesis/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Kinesis] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, ti sei connesso al tuo account [!DNL Kinesis] a [!DNL Platform]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
