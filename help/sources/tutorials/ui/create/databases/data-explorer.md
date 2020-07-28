---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Data Explorer nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Data Explorer] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Azure Data Explorer] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Azure Data Explorer] (in seguito denominato &quot;[!DNL Data Explorer]&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una [!DNL Data Explorer] connessione valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Data Explorer] account su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | L&#39;endpoint del [!DNL Data Explorer] server. |
| `database` | Nome del [!DNL Data Explorer] database. |
| `tenant` | L&#39;ID tenant univoco utilizzato per connettersi al [!DNL Data Explorer] database. |
| `servicePrincipalId` | L&#39;ID entità servizio univoco utilizzato per connettersi al database di Esplora dati. |
| `servicePrincipalKey` | Chiave entità servizio univoca utilizzata per connettersi al database di Esplora dati. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)di Esplora dati.

## Collegamento dell&#39; [!DNL Azure Data Explorer] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per creare un nuovo [!DNL Data Explorer] account a cui collegarvi [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . La *[!UICONTROL Catalog]* schermata mostra una varietà di origini per le quali è possibile creare un account in ingresso, e ogni origine mostra il numero di account esistenti e di flussi di dati ad essi associati.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL Azure Data Explorer]** e fare clic **sull&#39;icona + (+)** per creare un nuovo connettore di Esplora dati.

![catalogo](../../../../images/tutorials/create/data-explorer/catalog.png)

Viene *[!UICONTROL Connect to Azure Data Explorer]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Data Explorer] le credenziali per la connessione. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Data Explorer] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/data-explorer/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Data Explorer] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati in Platform](../../dataflow/databases.md).