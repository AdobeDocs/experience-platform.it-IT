---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente del Marketing Cloud Salesforce utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Salesforce Marketing Cloud] nell&#39;interfaccia utente

>[!NOTE]
>
> L&#39;origine [!DNL Salesforce Marketing Cloud] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo delle sorgenti con etichetta beta, consulta la [panoramica sulle sorgenti](../../../../home.md#terms-and-conditions) .

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Salesforce Marketing Cloud] utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Salesforce Marketing Cloud], puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Salesforce Marketing Cloud] su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. |
| `clientId` | L&#39;ID client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | Il segreto client associato all&#39;applicazione [!DNL Salesforce Marketing Cloud]. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Connetti il tuo account [!DNL Salesforce Marketing Cloud]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Salesforce Marketing Cloud] a Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. Puoi anche usare la barra di ricerca per restringere i connettori visualizzati.

Sotto la categoria [!UICONTROL Automazione marketing], seleziona **[!UICONTROL Marketing Cloud Salesforce]**, quindi seleziona **[!UICONTROL Imposta]**.

![catalogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a Marketing Cloud Salesforce]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Salesforce Marketing Cloud]. Al termine, selezionare **[!UICONTROL Connetti]**, quindi lasciare che sia necessario un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Salesforce Marketing Cloud] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Salesforce Marketing Cloud] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati del sistema di automazione del marketing in Platform](../../dataflow/marketing-automation.md).
