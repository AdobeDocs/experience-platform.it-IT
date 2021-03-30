---
keywords: Experience Platform;home;argomenti popolari;shopify;Shopify
solution: Experience Platform
title: Creare una connessione sorgente casuale nell’interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scopri come creare una connessione Shopify sorgente utilizzando l’interfaccia utente Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Creare una connessione sorgente [!DNL Shopify] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Shopify] utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md) Experience Data Model (XDM): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Shopify], puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati per un connettore eCommerce](../../dataflow/ecommerce.md).

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Shopify] su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Punto finale del server [!DNL Shopify]. |
| `accessToken` | Token di accesso per l’account utente [!DNL Shopify]. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Connetti il tuo account [!DNL Shopify]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Shopify] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL eCommerce]**, selezionare **[!UICONTROL Shopify]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Shopify].

![catalogo](../../../../images/tutorials/create/shopify/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Shopify]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Shopify]. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Shopify] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/shopify/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Shopify] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di eCommerce in [!DNL Platform]](../../dataflow/ecommerce.md).