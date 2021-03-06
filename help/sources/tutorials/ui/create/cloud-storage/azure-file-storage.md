---
keywords: Experience Platform;home;argomenti comuni;Azure File Storage;Connettore di archiviazione file di Azure
solution: Experience Platform
title: Creare una connessione di Azure File Storage Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Azure File Storage utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 25d483b6-3975-4e80-9dbe-28b7b91cb063
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Azure File Storage] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce passaggi per l&#39;autenticazione di un connettore di origine [!DNL Azure File Storage] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Azure File Storage] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine [!DNL Azure File Storage], è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Endpoint dell&#39;istanza [!DNL Azure File Storage] a cui si accede. |
| `userId` | L’utente con accesso sufficiente all’endpoint [!DNL Azure File Storage]. |
| `password` | Chiave di accesso [!DNL Azure File Storage]. |

Per ulteriori informazioni su come iniziare, consulta [this [!DNL Azure File Storage] document](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

## Connetti il tuo account [!DNL Azure File Storage]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Azure File Storage] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. La schermata **[!UICONTROL Catalogo]** visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Database]**, selezionare **[!UICONTROL Archiviazione file di Azure]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL Azure File Storage].

![catalogo](../../../../images/tutorials/create/azure-file-storage/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Azure File Storage]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Azure File Storage]. Al termine, selezionare **[!UICONTROL Connetti]**, quindi lasciare che sia necessario un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/azure-file-storage/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Azure File Storage] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/azure-file-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Azure File Storage] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
