---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics;home;popular topic;Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creare una connessione sorgente Microsoft Dynamics nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine Microsoft Dynamics utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# Creare un [!DNL Microsoft Dynamics] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Microsoft Dynamics] (in seguito denominati &quot;[!DNL Dynamics]&quot;) tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Dynamics] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati per un’origine CRM](../../dataflow/crm.md).

### Raccogli le credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL del servizio del tuo [!DNL Dynamics] dell&#39;istanza. |
| `username` | Il nome utente per il [!DNL Dynamics] account utente. |
| `password` | La password per [!DNL Dynamics] account. |
| `servicePrincipalId` | L’ID client del tuo [!DNL Dynamics] account. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connetti [!DNL Dynamics] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Dynamics] da un account a Platform.

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL CRM]** categoria, seleziona **[!UICONTROL Microsoft Dynamics]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL Dynamics] connettore.

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Il **[!UICONTROL Connetti a Dynamics]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Dynamics] account.

Il [!DNL Dynamics] Il connettore offre diversi tipi di autenticazione per l’accesso. Sotto [!UICONTROL Autenticazione account] seleziona **[!UICONTROL Autenticazione di base]** per utilizzare credenziali basate su password.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** quindi lascia un po’ di tempo per l’istituzione del nuovo account.

![autenticazione di base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

In alternativa, è possibile selezionare **[!UICONTROL Autenticazione Service-principal e chiave]** e collegare [!DNL Dynamics] account utilizzando una combinazione di [!UICONTROL ID entità servizio] e [!UICONTROL Chiave principale servizio].

>[!IMPORTANT]
>
> Autenticazione di base in [!DNL Dynamics] potrebbe essere bloccata dall’autenticazione a due fattori, attualmente non supportata da Platform. In questo caso, si consiglia di utilizzare l’autenticazione basata su chiave per creare un connettore di origine utilizzando [!DNL Dynamics].

![autenticazione basata su chiave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| [!UICONTROL ID entità servizio] | L’ID client del tuo [!DNL Dynamics] account. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| [!UICONTROL Chiave principale servizio] | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Dynamics] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** nell’angolo in alto a destra per procedere.

![esistente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Dynamics] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).
