---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Salesforce marketing cloud
solution: Experience Platform
title: Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del Marketing Cloud Salesforce utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Creare un [!DNL Salesforce Marketing Cloud] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
> Il [!DNL Salesforce Marketing Cloud] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Salesforce Marketing Cloud] connettore di origine che utilizza l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di un [!DNL Salesforce Marketing Cloud] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Salesforce Marketing Cloud] su Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando si immette il `host` , è necessario specificare solo il sottodominio e non l’intero URL. Ad esempio, se l’URL host è `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, è sufficiente inserire `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` come valore host. |
| `clientId` | L’ID client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |

Per ulteriori informazioni su come iniziare, consulta questa [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connetti [!DNL Salesforce Marketing Cloud] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Salesforce Marketing Cloud] da un account a Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. È inoltre possibile utilizzare la barra di ricerca per limitare i connettori visualizzati.

Sotto [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Marketing Cloud Salesforce]** e quindi seleziona **[!UICONTROL Configurazione]**.

![catalogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Il **[!UICONTROL Connetti al Marketing Cloud Salesforce]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Salesforce Marketing Cloud] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Salesforce Marketing Cloud] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Salesforce Marketing Cloud] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di marketing automation system in Platform](../../dataflow/marketing-automation.md).
