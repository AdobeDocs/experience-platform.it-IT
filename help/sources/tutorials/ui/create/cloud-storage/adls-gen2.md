---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Data Lake Storage Gen2 nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Data Lake Storage Gen2] sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore [!DNL Azure Data Lake Storage Gen2] (in seguito denominato &quot;[!DNL ADLS Gen2]&quot;) sorgente mediante l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione ADLS Gen2 valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore [!DNL ADLS Gen2] di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L&#39;endpoint per [!DNL ADLS Gen2]. |
| `servicePrincipalId` | L&#39;ID client dell&#39;applicazione. |
| `servicePrincipalKey` | La chiave dell&#39;applicazione. |
| `tenant` | Le informazioni sul tenant che contengono l&#39;applicazione. |

Per ulteriori informazioni su questi valori, fare riferimento a [ [!DNL ADLS Gen2] questo documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

## Collegamento dell&#39; [!DNL ADLS Gen2] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare l&#39; [!DNL ADLS Gen2] account a cui effettuare la connessione [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL Azure Data Lake Gen2]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore ADLS Gen2.

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

Viene visualizzata **[!UICONTROL Connect to Azure Data Lake Gen2]** la finestra di dialogo. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New Account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL ADLS Gen2] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL ADLS Gen2] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL ADLS Gen2] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud [!DNL Platform]](../../dataflow/batch/cloud-storage.md).