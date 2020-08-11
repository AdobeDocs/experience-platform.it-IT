---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Microsoft Dynamics nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Creare un connettore [!DNL Microsoft Dynamics] sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati CRM di origine esterna su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Microsoft Dynamics] (in seguito denominato &quot;[!DNL Dynamics]&quot;) sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un [!DNL Dynamics] account valido, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL del servizio dell’ [!DNL Dynamics] istanza. |
| `username` | Nome utente per l’account [!DNL Dynamics] utente. |
| `password` | La password per il tuo account Dynamics. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)di Dynamics.

## Collegamento dell&#39; [!DNL Dynamics] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per creare un nuovo [!DNL Dynamics] account a cui collegarvi [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL Dynamics]** seguito **[!UICONTROL Add data]** da per creare un nuovo [!DNL Dynamics] connettore.

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Viene *[!UICONTROL Connect to Dynamics]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Dynamics] le credenziali per la connessione. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Dynamics] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo superiore destro per proseguire.

![esistenti](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Dynamics] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/crm.md).