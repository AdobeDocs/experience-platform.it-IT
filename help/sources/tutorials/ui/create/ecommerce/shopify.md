---
keywords: Experience Platform;home;argomenti popolari;shopify;Shopify
solution: Experience Platform
title: Creare una connessione sorgente Shopify nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Shopify utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Creare un [!DNL Shopify] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Shopify] connettore di origine che utilizza [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di un [!DNL Shopify] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati per un connettore eCommerce](../../dataflow/ecommerce.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Shopify] account su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Punto finale del [!DNL Shopify] server. |
| `accessToken` | Il token di accesso per [!DNL Shopify] account utente. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Connetti [!DNL Shopify] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Shopify] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL eCommerce]** categoria, seleziona **[!UICONTROL Shopify]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL Shopify] connettore.

![catalogo](../../../../images/tutorials/create/shopify/catalog.png)

Il **[!UICONTROL Connetti a Shopify]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Shopify] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/shopify/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Shopify] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/shopify/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Shopify] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati eCommerce in [!DNL Platform]](../../dataflow/ecommerce.md).
