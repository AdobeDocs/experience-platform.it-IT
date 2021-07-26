---
keywords: Experience Platform;home;argomenti popolari;paypal;Paypal
solution: Experience Platform
title: Creare una connessione PayPal all’origine nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente PayPal utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: 6b6bd67e70267e81c144c37549b0dcba20534eb6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL PayPal] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL PayPal] utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL PayPal] valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere alla piattaforma account [!DNL PayPal], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | URL dell&#39;istanza [!DNL PayPal]. |
| `clientID` | L&#39;ID client associato all&#39;applicazione [!DNL PayPal]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL PayPal]. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL PayPal] documento](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connetti il tuo account [!DNL PayPal]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL PayPal] a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. La schermata **[!UICONTROL Catalogo]** visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Pagamenti]**, selezionare **[!UICONTROL PayPal]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL PayPal].

![catalogo](../../../../images/tutorials/create/paypal/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a PayPal]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL PayPal]. Al termine, selezionare **[!UICONTROL Connetti]**, quindi lasciare che sia necessario un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL PayPal] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/paypal/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL PayPal] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di pagamento in Platform](../../dataflow/payments.md).
