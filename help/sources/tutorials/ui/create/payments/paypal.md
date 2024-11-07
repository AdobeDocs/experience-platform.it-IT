---
keywords: Experience Platform;home;argomenti popolari;paypal;Paypal
solution: Experience Platform
title: Creare una connessione Source PayPal nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente PayPal utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL PayPal] nell&#39;interfaccia utente

>[!IMPORTANT]
>
>L&#39;origine [!DNL PayPal] diventerà obsoleta alla fine di maggio 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL PayPal].

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL PayPal] tramite l&#39;interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL PayPal] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli le credenziali richieste

Per accedere alla piattaforma dell&#39;account [!DNL PayPal], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | URL dell&#39;istanza [!DNL PayPal]. |
| `clientID` | L&#39;ID client associato all&#39;applicazione [!DNL PayPal]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL PayPal]. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connetti il tuo account [!DNL PayPal]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL PayPal] a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Pagamenti]**, seleziona **[!UICONTROL PayPal]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL PayPal].

![catalogo](../../../../images/tutorials/create/paypal/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a PayPal]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL PayPal]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/paypal/connect.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL PayPal] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/paypal/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL PayPal]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati di pagamento in Platform](../../dataflow/payments.md).
