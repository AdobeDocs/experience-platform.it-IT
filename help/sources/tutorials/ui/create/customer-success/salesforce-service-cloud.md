---
keywords: ' Experience Platform;home;argomenti popolari;Salesforce Service Cloud;salesforce service cloud'
solution: Experience Platform
title: Creare una connessione di origine Salesforce Service Cloud nell’interfaccia utente
topic: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Salesforce Service Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Salesforce Service Cloud] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Salesforce Service Cloud] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Salesforce Service Cloud] (in seguito denominato &quot;SSC&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione SSC valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli credenziali richieste

Per accedere al tuo account SSC su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Nome utente per l’account utente. |
| `password` | La password dell&#39;account utente. |
| `securityToken` | Token di sicurezza per l&#39;account utente. |

Per ulteriori informazioni su come iniziare, fare riferimento a [this [!DNL Salesforce Service Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Collegare l&#39;account [!DNL Salesforce Service Cloud]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account SSC a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Customer Success]**, selezionare **[!UICONTROL Salesforce Service Cloud]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore SSC.

![catalogo](../../../../images/tutorials/create/ssc/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Salesforce Service Cloud]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input che viene visualizzato, fornite un nome, una descrizione facoltativa e le credenziali SSC. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account SSC con cui connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ssc/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, si è stabilito un collegamento al proprio account SSC. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati di successo del cliente in [!DNL Platform]](../../dataflow/customer-success.md).