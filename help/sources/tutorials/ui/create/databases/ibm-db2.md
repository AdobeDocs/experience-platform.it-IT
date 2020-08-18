---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente IBM DB2 nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---



# Creare un connettore sorgente IBM DB2 nell&#39;interfaccia utente

>[!NOTE]
> Il connettore IBM DB2 è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente IBM DB2 (in seguito denominato &quot;DB2&quot;) tramite l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione DB2 valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi correttamente a DB2 utilizzando l&#39; [!DNL Flow Service] API.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `server` | Nome del server DB2. Potete specificare il numero di porta dopo il nome del server delimitato da due punti. Ad esempio: server:port. |
| `database` | Nome del database DB2. |
| `username` | Nome utente utilizzato per connettersi al database DB2. |
| `password` | La password per l’account utente specificato per il nome utente. |

Per ulteriori informazioni su come iniziare, consultare [questo documento](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)DB2.

## Collegamento dell&#39;account IBM DB2

Dopo aver raccolto le credenziali richieste, è possibile seguire i passaggi descritti di seguito per collegare l&#39;account DB2 a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL IBM DB2]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore DB2.

![catalogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

Viene **[!UICONTROL Connect to IBM DB2]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali DB2. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account DB2 con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ibm-db2/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account DB2. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati in cui inserire i dati [!DNL Platform]](../../dataflow/databases.md).