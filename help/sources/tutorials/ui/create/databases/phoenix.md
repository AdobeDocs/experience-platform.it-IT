---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Phoenix nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# Creare un connettore [!DNL Phoenix] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Phoenix] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Phoenix] sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una [!DNL Phoenix] connessione valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md)

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Phoenix] account su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Indirizzo IP o nome host del [!DNL Phoenix] server. |
| `port` | La porta TCP utilizzata dal [!DNL Phoenix] server per ascoltare le connessioni client. Se vi connettete a [!DNL Azure HDInsights], specificate la porta come 443. |
| `httpPath` | URL parziale corrispondente al [!DNL Phoenix] server. Specificate /hbasephoenix0 se utilizzate il [!DNL Azure HDInsights] cluster. |
| `username` | Il nome utente utilizzato per accedere al [!DNL Phoenix] server. |
| `password` | La password che corrisponde all&#39;utente. |
| `enableSsl` | Un interruttore che specifica se le connessioni al server sono crittografate utilizzando SSL. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)Phoenix.

## Collegamento dell&#39;account Phoenix

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per creare un nuovo [!DNL Phoenix] account a cui collegarvi [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. La *[!UICONTROL Catalog]* schermata mostra una varietà di origini per le quali è possibile creare un account in ingresso, e ogni origine mostra il numero di account esistenti e di flussi di dati ad essi associati.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionate **[!UICONTROL Phoenix]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione in entrata, selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/phoenix/catalog.png)

Viene *[!UICONTROL Connect to Phoenix]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Phoenix] le credenziali per la connessione. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Phoenix] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/phoenix/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Phoenix] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).