---
title: Collegare l’account Marketing Cloud di Salesforce ad Experience Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account Marketing Cloud di Salesforce ad Experience Platform tramite l’interfaccia utente.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 2%

---

# Connetti il tuo account [!DNL Salesforce Marketing Cloud] ad Experience Platform tramite l&#39;interfaccia utente

>[!WARNING]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] diventerà obsoleta a gennaio 2026. Una nuova fonte verrà rilasciata nel corso di quest&#39;anno come alternativa. Una volta rilasciata la nuova origine, è necessario pianificare la migrazione alla nuova origine creando nuove connessioni account e flussi di dati prima della fine di gennaio 2026.

Questo tutorial illustra i passaggi necessari per collegare l&#39;account [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform tramite l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Salesforce Marketing Cloud], puoi saltare il resto di questo documento e passare all&#39;esercitazione su [portare dati di automazione marketing in Experience Platform utilizzando l&#39;interfaccia utente](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per accedere al tuo account [!DNL Salesforce Marketing Cloud] su Experience Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Host | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il valore `host`, è necessario specificare `{subdomain}.rest.marketingcloudapis.com`. Ad esempio, se l&#39;URL host è `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è necessario immettere `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` come valore host. |
| ID client | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| Segreto client | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |

Per ulteriori informazioni sull&#39;autenticazione per [!DNL Salesforce Marketing Cloud], visitare la [[!DNL Salesforce] documentazione sull&#39;autenticazione](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connetti il tuo account [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Il [!UICONTROL catalogo] visualizza diverse origini supportate da Experience Platform.

È possibile selezionare la categoria appropriata dall&#39;elenco delle categorie. Puoi anche utilizzare la barra di ricerca per filtrare in base a un’origine specifica.

Nella categoria [!UICONTROL Automazione marketing], selezionare **[!UICONTROL Salesforce Marketing Cloud]**, quindi **[!UICONTROL Configurazione]**.

![Catalogo delle origini con l&#39;origine Marketing Cloud di Salesforce selezionata.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Salesforce Marketing Cloud]**. In questa pagina è possibile creare un nuovo account o utilizzare un account esistente.

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome per il tuo account, una descrizione facoltativa e le credenziali di autenticazione corrispondenti al tuo account [!DNL Salesforce Marketing Cloud].

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell&#39;account in cui è possibile autenticare un nuovo account per Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Account esistente

Se disponi già di un account, seleziona **[!UICONTROL Account esistente]**, quindi seleziona l&#39;account che desideri utilizzare dall&#39;elenco visualizzato.

![Interfaccia account esistente in cui è possibile effettuare la selezione da un elenco di account Salesforce Marketing Cloud esistenti.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione tra il tuo account [!DNL Salesforce Marketing Cloud] e Experience Platform. Ora puoi continuare con l&#39;esercitazione successiva e [creare un flusso di dati per inserire i dati di automazione marketing in Experience Platform](../../dataflow/marketing-automation.md).
