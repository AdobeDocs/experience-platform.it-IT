---
keywords: Experience Platform;home;argomenti popolari;shopify;Shopify
solution: Experience Platform
title: Creare una connessione sorgente casuale nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione Shopify sorgente utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 527cac95-3d9a-4089-98e4-66d746641b85
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# Crea un [!DNL Shopify] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Shopify] connettore di origine con [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Sistema Experience Data Model (XDM)](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se hai già un [!DNL Shopify] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati per un connettore eCommerce](../../dataflow/ecommerce.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Shopify] conto su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Il punto finale del tuo [!DNL Shopify] server. |
| `accessToken` | Token di accesso per il tuo [!DNL Shopify] account utente. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [[!DNL Shopify] documento](https://shopify.dev/concepts/about-apis/authentication).

## Collega il tuo [!DNL Shopify] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Shopify] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL eCommerce]** categoria, seleziona **[!UICONTROL Shopificante]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Shopify] connettore.

![catalogo](../../../../images/tutorials/create/shopify/catalog.png)

La **[!UICONTROL Connetti a Shopify]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Shopify] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/shopify/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Shopify] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/shopify/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Shopify] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati eCommerce in [!DNL Platform]](../../dataflow/ecommerce.md).
