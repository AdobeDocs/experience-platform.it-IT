---
keywords: Experience Platform;home;argomenti comuni;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;connettore adls
solution: Experience Platform
title: Creare una connessione di origine di Azure Data Lake Storage Gen2 nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine di Azure Data Lake Storage Gen2 utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Creare un [!DNL Azure Data Lake Storage Gen2] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un [!DNL Azure Data Lake Storage Gen2] (in seguito denominati &quot;[!DNL ADLS Gen2]&quot;) connettore di origine utilizzando [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione ADLS Gen2 valida, puoi saltare il resto del documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per autenticare il tuo [!DNL ADLS Gen2] connettore di origine, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | Endpoint per [!DNL ADLS Gen2]. |
| `servicePrincipalId` | ID client dell’applicazione. |
| `servicePrincipalKey` | Chiave dell&#39;applicazione. |
| `tenant` | Informazioni tenant contenenti l&#39;applicazione. |

Per ulteriori informazioni su questi valori, consulta [questo [!DNL ADLS Gen2] documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Connetti [!DNL ADLS Gen2] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL ADLS Gen2] account a cui connettersi [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Azure Data Lake Gen2]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Il **[!UICONTROL Connessione ad Azure Data Lake Gen2]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL ADLS Gen2] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL ADLS Gen2] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL ADLS Gen2] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
