---
keywords: Experience Platform;home;argomenti popolari;paypal;Paypal
solution: Experience Platform
title: Creare una connessione sorgente PayPal nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente PayPal utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Creare un [!DNL PayPal] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL PayPal] connettore di origine che utilizza l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL PayPal] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL PayPal] piattaforma dell’account, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | L’URL del [!DNL PayPal] dell&#39;istanza. |
| `clientID` | L’ID client associato al tuo [!DNL PayPal] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL PayPal] applicazione. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connetti [!DNL PayPal] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL PayPal] da un account a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Pagamenti]** categoria, seleziona **[!UICONTROL PayPal]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL PayPal] connettore.

![catalogo](../../../../images/tutorials/create/paypal/catalog.png)

Il **[!UICONTROL Connetti a PayPal]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL PayPal] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/paypal/connect.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL PayPal] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/paypal/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL PayPal] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di pagamento in Platform](../../dataflow/payments.md).
