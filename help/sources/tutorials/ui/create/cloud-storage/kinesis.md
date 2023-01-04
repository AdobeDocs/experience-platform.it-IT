---
keywords: Experience Platform;home;argomenti popolari;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: Creare una connessione sorgente Amazon Kinesis nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Amazon Kinesis utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Crea un [!DNL Amazon Kinesis] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un [!DNL Amazon Kinesis] (di seguito denominati [!DNL "Kinesis"]) connettore di origine utilizzando [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Kinesis] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli credenziali richieste

Per autenticare il [!DNL Kinesis] connettore di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per il tuo [!DNL Kinesis] conto. |
| `Secret access key` | Chiave di accesso segreto per il tuo [!DNL Kinesis] conto. |
| `region` | La regione del server AWS. |

Per ulteriori informazioni su questi valori, consulta [questo [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Collega il tuo [!DNL Kinesis] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Kinesis] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Archiviazione cloud]** categoria, seleziona **[!UICONTROL Amazon Kinesis]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Kinesis] connettore.

![](../../../../images/tutorials/create/kinesis/catalog.png)

La **[!UICONTROL Connettersi ad Amazon Kinesis]** viene visualizzata la finestra di dialogo . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Kinesis] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/kinesis/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Kinesis] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, ti sei connesso al tuo [!DNL Kinesis] account a [!DNL Platform]. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
