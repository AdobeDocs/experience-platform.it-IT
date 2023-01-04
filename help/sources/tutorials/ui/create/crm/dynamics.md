---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creare una connessione sorgente Microsoft Dynamics nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Microsoft Dynamics utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Crea un [!DNL Microsoft Dynamics] connessione sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Microsoft Dynamics] (in appresso denominato &quot;[!DNL Dynamics]&quot;) la connessione sorgente tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Dynamics] account, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati per un&#39;origine CRM](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL di servizio della [!DNL Dynamics] istanza. |
| `username` | Nome utente per il [!DNL Dynamics] account utente. |
| `password` | La password [!DNL Dynamics] conto. |
| `servicePrincipalId` | L&#39;ID cliente del tuo [!DNL Dynamics] conto. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Collega il tuo [!DNL Dynamics] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Dynamics] a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL CRM]** categoria, seleziona **[!UICONTROL Microsoft Dynamics]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Dynamics] connettore.

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

La **[!UICONTROL Connetti a Dynamics]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome e una descrizione facoltativa per il nuovo [!DNL Dynamics] conto.

La [!DNL Dynamics] connettore fornisce diversi tipi di autenticazione per l’accesso. Sotto [!UICONTROL Autenticazione account] select **[!UICONTROL Autenticazione di base]** per utilizzare le credenziali basate su password.

Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e poi lascia un po&#39; di tempo per stabilire il nuovo account.

![autenticazione di base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

In alternativa, è possibile selezionare **[!UICONTROL Autenticazione principale del servizio e chiave]** e collegare il [!DNL Dynamics] account utilizzando una combinazione di [!UICONTROL ID principale servizio] e [!UICONTROL Chiave principale servizio].

>[!IMPORTANT]
>
> Autenticazione di base in [!DNL Dynamics] possono essere bloccati dall’autenticazione a due fattori, attualmente non supportata da Platform. In questo caso, si consiglia di utilizzare l’autenticazione basata su chiave per creare un connettore di origine utilizzando [!DNL Dynamics].

![autenticazione basata su chiave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| [!UICONTROL ID principale servizio] | L&#39;ID cliente del tuo [!DNL Dynamics] conto. Questo ID è necessario quando si utilizzano l’entità del servizio e l’autenticazione basata sulle chiavi. |
| [!UICONTROL Chiave principale servizio] | Chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizza l’entità del servizio e l’autenticazione basata sulle chiavi. |

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Dynamics] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per proseguire.

![esistente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Dynamics] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati in Platform](../../dataflow/crm.md).
