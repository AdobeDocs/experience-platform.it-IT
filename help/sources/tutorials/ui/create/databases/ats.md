---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Table Storage nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Table Storage] sorgente nell’interfaccia utente

>[!NOTE]
>Il [!DNL Azure Table Storage] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Azure Table Storage] (in seguito denominato &quot;ATS&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione ATS valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account ATS su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione per la connessione all&#39; [!DNL Azure Table Storage] istanza. Stringa di connessione per la connessione all&#39;istanza ATS. Il pattern della stringa di connessione per ATS è `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Per ulteriori informazioni su come iniziare, consulta [ [!DNL Azure Table Storage] questo documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Collegamento dell&#39; [!DNL Azure Table Storage] account

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per collegare il tuo account ATS a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL Azure Table Storage]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore ATS.

![catalogo](../../../../images/tutorials/create/ats/catalog.png)

Viene **[!UICONTROL Connect to Azure Table Storage]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali ATS. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ats/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account ATS con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ats/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account ATS. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati in cui inserire i dati [!DNL Platform]](../../dataflow/databases.md).