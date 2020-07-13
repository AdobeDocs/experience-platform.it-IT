---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Blob o Amazon S3 nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---


# Creare un connettore sorgente [!DNL Azure Blob] o [!DNL Amazon] S3 nell’interfaccia utente

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce passaggi per la creazione di un connettore sorgente [!DNL Azure Blob] (in seguito denominato &quot;Blob&quot;) o [!DNL Amazon] S3 (in seguito denominato &quot;S3&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di base Blob o S3, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

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

Allo stesso modo, l&#39;accesso al bucket S3 [!DNL Platform] richiede di fornire i valori validi per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `s3AccessKey` | ID chiave di accesso per l&#39;archiviazione S3. |
| `s3SecretKey` | ID chiave segreta per l&#39;archiviazione S3. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)AWS.

## Collegamento dell&#39;account Blob o S3

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare un nuovo account Blob o S3 a cui connetterti [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL Azure Blob Storage]** o **[!UICONTROL Amazon S3]** fare clic **sull&#39;icona + (+)** per creare un nuovo connettore [!DNL Blob] o S3.

![catalogo](../../../../images/tutorials/create/blob/catalog.png)

Viene *[!UICONTROL Connect to Azure Blob Storage]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input che viene visualizzato, fornire alla connessione un nome, una descrizione facoltativa e le credenziali [!DNL Blob] o S3. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/blob/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Blob] o S3 con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/blob/existing.png)

## Passaggi successivi e risorse aggiuntive

Seguendo questa esercitazione, è stata stabilita una connessione al proprio account [!DNL Blob] o S3. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud ad Platform](../../dataflow/batch/cloud-storage.md).