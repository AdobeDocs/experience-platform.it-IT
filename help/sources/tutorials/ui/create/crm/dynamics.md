---
keywords: Experience Platform;home;argomenti comuni;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creare una connessione Microsoft Dynamics Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Microsoft Dynamics utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Microsoft Dynamics] nell&#39;interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare una connessione sorgente [!DNL Microsoft Dynamics] (in seguito denominata &quot;[!DNL Dynamics]&quot;) utilizzando l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Dynamics] valido, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati per un&#39;origine CRM](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente dell&#39;account utente [!DNL Dynamics]. |
| `password` | Password per il tuo account [!DNL Dynamics]. |
| `servicePrincipalId` | L&#39;ID client del tuo account [!DNL Dynamics]. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |

Per ulteriori informazioni su come iniziare, consulta [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connetti il tuo account [!DNL Dynamics]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Dynamics] a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL CRM]**, selezionare **[!UICONTROL Microsoft Dynamics]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Dynamics].

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Dynamics]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, fornisci un nome e una descrizione facoltativa per il nuovo account [!DNL Dynamics].

Il connettore [!DNL Dynamics] fornisce diversi tipi di autenticazione per l’accesso. In [!UICONTROL Account authentication] selezionare **[!UICONTROL Basic authentication]** per utilizzare le credenziali basate su password.

Al termine, seleziona **[!UICONTROL Connect to source]** e quindi consenti un po&#39; di tempo per la determinazione del nuovo account.

![autenticazione di base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

In alternativa, è possibile selezionare **[!UICONTROL Service-principal and key authentication]** e collegare il proprio account [!DNL Dynamics] utilizzando una combinazione di [!UICONTROL Service principal ID] e [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> L’autenticazione di base in [!DNL Dynamics] può essere bloccata dall’autenticazione a due fattori, attualmente non supportata da Platform. In questo caso, si consiglia di utilizzare l’autenticazione basata su chiave per creare un connettore di origine utilizzando [!DNL Dynamics].

![autenticazione basata su chiave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | L&#39;ID client del tuo account [!DNL Dynamics]. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| [!UICONTROL Service principal key] | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |

### Account esistente

Per collegare un account esistente, seleziona l&#39;account [!DNL Dynamics] con cui desideri connetterti, quindi seleziona **[!UICONTROL Next]** nell&#39;angolo in alto a destra per continuare.

![esistente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Dynamics] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).
