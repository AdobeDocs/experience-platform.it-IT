---
keywords: ' Experience Platform;home;argomenti popolari;shopify;Shopify'
solution: Experience Platform
title: Creare una connessione di origine casuale nell’interfaccia utente
topic: overview
type: Tutorial
description: Scoprite come creare una connessione Shopify source utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Shopify] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore [!DNL Shopify] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore di origine [!DNL Shopify] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) XDM (Experience Data Model): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione [!DNL Shopify], potete ignorare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati per un connettore eCommerce](../../dataflow/ecommerce.md).

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Shopify] su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Punto finale del server [!DNL Shopify]. |
| `accessToken` | Token di accesso per l&#39;account utente [!DNL Shopify]. |

Per ulteriori informazioni su come iniziare, fare riferimento a questo [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Collegare l&#39;account [!DNL Shopify]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Shopify] a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL eCommerce]**, selezionare **[!UICONTROL Shopify]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Shopify].

![catalogo](../../../../images/tutorials/create/shopify/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Shopify]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Shopify]. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Shopify] con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/shopify/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Shopify]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati di eCommerce in [!DNL Platform]](../../dataflow/ecommerce.md).