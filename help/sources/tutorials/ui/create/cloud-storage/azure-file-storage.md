---
keywords: Experience Platform;home;argomenti comuni;Azure File Storage;Azure File Storage connector
solution: Experience Platform
title: Creare una connessione Azure File Storage Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine Azure File Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Creare un [!DNL Azure File Storage] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per autenticare un [!DNL Azure File Storage] connettore di origine che utilizza [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Azure File Storage] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per autenticare il tuo [!DNL Azure File Storage] connettore di origine, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Endpoint del [!DNL Azure File Storage] istanza a cui si sta effettuando l’accesso. |
| `userId` | L’utente con un accesso sufficiente al [!DNL Azure File Storage] endpoint. |
| `password` | Il [!DNL Azure File Storage] chiave di accesso. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Azure File Storage] documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Connetti [!DNL Azure File Storage] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Azure File Storage] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Archiviazione file di Azure]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL Azure File Storage] connettore.

![catalogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Il **[!UICONTROL Connetti ad Azure File Storage]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Azure File Storage] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/azure-file-storage/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Azure File Storage] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Azure File Storage] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
