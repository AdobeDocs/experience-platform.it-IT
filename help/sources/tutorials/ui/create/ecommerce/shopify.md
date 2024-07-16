---
keywords: Experience Platform;home;argomenti popolari;shopify;Shopify
solution: Experience Platform
title: Creare una connessione Shopify Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Shopify utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Shopify] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Shopify] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Shopify], puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati per un connettore eCommerce](../../dataflow/ecommerce.md).

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL Shopify] in [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Punto finale del server [!DNL Shopify]. |
| `accessToken` | Il token di accesso per l&#39;account utente [!DNL Shopify]. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Connetti il tuo account [!DNL Shopify]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Shopify] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL eCommerce]**, seleziona **[!UICONTROL Shopify]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL Shopify].

![catalogo](../../../../images/tutorials/create/shopify/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Shopify]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL Shopify]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/shopify/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL Shopify] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/shopify/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Shopify]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati eCommerce in [!DNL Platform]](../../dataflow/ecommerce.md).
