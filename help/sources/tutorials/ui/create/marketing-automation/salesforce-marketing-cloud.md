---
title: Connetti il tuo account di Marketing Cloud Salesforce a Experienci Platform tramite l’interfaccia utente
description: Scopri come collegare il tuo account di Marketing Cloud Salesforce a Experienci Platform tramite l’interfaccia utente.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 30f1e8a0424ee0f81d8e98fb24886ad1480b270c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---

# Connetti [!DNL Salesforce Marketing Cloud] da Experience Platform tramite l’interfaccia utente

>[!IMPORTANT]
>
>L’acquisizione di oggetti personalizzati non è attualmente supportata da [!DNL Salesforce Marketing Cloud] integrazione sorgente.

Questo tutorial descrive come collegare [!DNL Salesforce Marketing Cloud] a Adobe Experience Platform tramite l’interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di un [!DNL Salesforce Marketing Cloud] account, puoi saltare il resto di questo documento e passare all’esercitazione su [Experience Platform dei dati di automazione marketing tramite l’interfaccia utente di](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Salesforce Marketing Cloud] su Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Host | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il `host` valore, è necessario specificare il valore `{subdomain}.rest.marketingcloudapis.com`. Ad esempio, se l’URL host è `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è necessario immettere `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` come valore host. |
| ID client | L’ID client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| Segreto client | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |

Per ulteriori informazioni sull&#39;autenticazione per [!DNL Salesforce Marketing Cloud], visita il [[!DNL Salesforce] documentazione di autenticazione](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connetti [!DNL Salesforce Marketing Cloud] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] In vengono visualizzate diverse origini supportate da Experienci Platform.

È possibile selezionare la categoria appropriata dall&#39;elenco delle categorie. Puoi anche utilizzare la barra di ricerca per filtrare in base a un’origine specifica.

Sotto [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Marketing Cloud Salesforce]** e quindi seleziona **[!UICONTROL Configurazione]**.

![Catalogo delle origini con l’origine del Marketing Cloud Salesforce selezionata.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Il **[!UICONTROL Connetti al Marketing Cloud Salesforce]** viene visualizzata. In questa pagina è possibile creare un nuovo account o utilizzare un account esistente.

### Nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome per l&#39;account, una descrizione facoltativa e le credenziali di autenticazione corrispondenti al tuo [!DNL Salesforce Marketing Cloud] account.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell’account in cui puoi autenticare un nuovo account per il Marketing Cloud Salesforce.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Account esistente

Se disponi già di un account, seleziona **[!UICONTROL Account esistente]** quindi seleziona l’account che desideri utilizzare dall’elenco visualizzato.

![L’interfaccia account esistente, in cui puoi effettuare la selezione da un elenco di account di Marketing Cloud Salesforce esistenti.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione tra [!DNL Salesforce Marketing Cloud] account e Experience Platform. Ora puoi continuare con l’esercitazione successiva e [creare un flusso di dati per portare in Experience Platform i dati di automazione marketing](../../dataflow/marketing-automation.md).
