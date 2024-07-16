---
keywords: Experience Platform;home;argomenti comuni;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;connettore adls
solution: Experience Platform
title: Creare una connessione Source di Azure Data Lake Storage Gen2 nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine di Azure Data Lake Storage Gen2 utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Crea una connessione di origine [!DNL Azure Data Lake Storage Gen2] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questa esercitazione fornisce i passaggi per autenticare un connettore di origine [!DNL Azure Data Lake Storage Gen2] (di seguito denominato &quot;[!DNL ADLS Gen2]&quot;) tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione ADLS Gen2 valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per autenticare il connettore di origine [!DNL ADLS Gen2], è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | Endpoint per [!DNL ADLS Gen2]. |
| `servicePrincipalId` | ID client dell’applicazione. |
| `servicePrincipalKey` | Chiave dell&#39;applicazione. |
| `tenant` | Informazioni tenant contenenti l&#39;applicazione. |

Per ulteriori informazioni su questi valori, fare riferimento a [questo [!DNL ADLS Gen2] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Connetti il tuo account [!DNL ADLS Gen2]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL ADLS Gen2] per connettersi a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Database]**, selezionare **[!UICONTROL Azure Data Lake Gen2]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Connetti ad Azure Data Lake Gen2]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL ADLS Gen2]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL ADLS Gen2] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL ADLS Gen2]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
