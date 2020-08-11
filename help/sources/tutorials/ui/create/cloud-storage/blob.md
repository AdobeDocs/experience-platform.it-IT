---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Blob nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Blob] sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un [!DNL Azure Blob] (in seguito denominato &quot;Blob&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base Blob, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

- Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
- JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
- Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere all&#39;archiviazione Blob su [!DNL Platform], è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione necessaria per accedere ai dati nell&#39;archivio Blob. Il pattern della stringa di connessione BLOB è: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Per ulteriori informazioni su come iniziare, visitare [questo documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)BLOB di Azure.

## Collegamento dell&#39;account Blob

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account Blob a cui connetterti [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL Azure Blob Storage]** seguita da **[!UICONTROL Add data]** per creare un nuovo [!DNL Blob]connettore.

![catalogo](../../../../images/tutorials/create/blob/catalog.png)

Viene *[!UICONTROL Connect to Azure Blob Storage]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Blob] le credenziali per la connessione. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/blob/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Blob] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/blob/existing.png)

## Passaggi successivi e risorse aggiuntive

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Blob] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/batch/cloud-storage.md).