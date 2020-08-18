---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un Apache Hive sul connettore di origine Azure HDInsights nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---


# Creare un connettore [!DNL Apache Hive] on- [!DNL Azure HDInsights] source nell&#39;interfaccia utente

>[!NOTE]
> Il [!DNL Apache Hive] connettore on [!DNL Azure HDInsights] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Apache Hive] on [!DNL Azure HDInsights] source utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una [!DNL Hive] connessione valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md)

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Hive] account su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Hive] server. |
| `username` | Il nome utente utilizzato per accedere al [!DNL Hive] server. |
| `password` | La password che corrisponde all&#39;utente. |

Per ulteriori informazioni su come iniziare, consulta [ [!DNL Hive] questo documento](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Collegamento dell&#39; [!DNL Hive] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL Hive] account a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL Hive]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo [!DNL Hive] connettore.

![catalogo](../../../../images/tutorials/create/hive/catalog.png)

Viene **[!UICONTROL Connect to Hive]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Hive] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/hive/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Hive] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/hive/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Hive] account. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati in cui inserire i dati [!DNL Platform]](../../dataflow/databases.md).