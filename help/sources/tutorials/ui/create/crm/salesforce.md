---
keywords: ' Experience Platform;home;argomenti popolari;Salesforce;salesforce'
solution: Experience Platform
title: Creare una connessione sorgente Salesforce nell’interfaccia utente
topic: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Salesforce utilizzando l’interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Salesforce] nell&#39;interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati CRM di origine esterna su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore di origine [!DNL Salesforce] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di un account [!DNL Salesforce] valido, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | L&#39;URL dell&#39;istanza di origine [!DNL Salesforce]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Salesforce]. |
| `password` | La password per l&#39;account utente [!DNL Salesforce]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Salesforce]. |

Per ulteriori informazioni su come iniziare, consultare [questo documento Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

## Collegare l&#39;account [!DNL Salesforce]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Salesforce] a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Salesforce]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore Salesforce.

![catalogo](../../../../images/tutorials/create/salesforce/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Salesforce]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Salesforce]. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Salesforce] con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo superiore destro per continuare.

![esistenti](../../../../images/tutorials/create/salesforce/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Salesforce]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;inserimento di dati in [!DNL Platform]](../../dataflow/crm.md).