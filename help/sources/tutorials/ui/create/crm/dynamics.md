---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics;home;popular topic;Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creare una connessione sorgente Microsoft Dynamics nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine Microsoft Dynamics utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Creare un [!DNL Microsoft Dynamics] connessione sorgente nell’interfaccia utente

Questo tutorial descrive come creare un [!DNL Microsoft Dynamics] (in seguito denominati &quot;[!DNL Dynamics]&quot;) tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Dynamics] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati per un’origine CRM](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per autenticare il tuo [!DNL Dynamics] origine, è necessario fornire valori per le proprietà di connessione seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

| Credenziali | Descrizione |
| --- | --- |
| `serviceUri` | L’URL del servizio del tuo [!DNL Dynamics] dell&#39;istanza. |
| `username` | Il nome utente per il [!DNL Dynamics] account utente. |
| `password` | La password per [!DNL Dynamics] account. |

>[!TAB Autenticazione Service-principal e chiave]

| Credenziali | Descrizione |
| --- | --- |
| `servicePrincipalId` | L’ID client del tuo [!DNL Dynamics] account. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

>[!ENDTABS]

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connetti [!DNL Dynamics] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL CRM] categoria, seleziona **[!UICONTROL Microsoft Dynamics]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con Microsoft Dynamics selezionato.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Il **[!UICONTROL Connetti account Microsoft Dynamics]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Dynamics] account che desideri utilizzare, quindi seleziona **[!UICONTROL Successivo]** nell’angolo in alto a destra per procedere.

![Interfaccia account esistente.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nuovo account

>[!TIP]
>
>Una volta creato, non è possibile modificare il tipo di autenticazione di un [!DNL Dynamics] connessione di base. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Dynamics] account.

![La nuova interfaccia per la creazione di account.](../../../../images/tutorials/create/ms-dynamics/new.png)

È possibile utilizzare l’autenticazione di base o l’autenticazione service-principal e chiave durante la creazione di un [!DNL Dynamics] account.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per creare un [!DNL Dynamics] account con autenticazione di base, seleziona [!UICONTROL Autenticazione di base] e quindi fornisci i valori per [!UICONTROL URI servizio], [!UICONTROL Nome utente], e [!UICONTROL Password]. **Nota**: autenticazione di base in [!DNL Dynamics] potrebbe essere bloccata dall’autenticazione a due fattori, attualmente non supportata da Platform. In questo caso, si consiglia di utilizzare l’autenticazione basata su chiave per creare un connettore di origine utilizzando [!DNL Dynamics].

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** quindi lascia un po’ di tempo per l’istituzione del nuovo account.

![Interfaccia di autenticazione di base.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Autenticazione Service-principal e chiave]

Per creare un [!DNL Dynamics] account con autenticazione service-principal e chiave, selezionare **[!UICONTROL Autenticazione Service-principal e chiave]** e quindi fornisci i valori per [!UICONTROL ID entità servizio] e [!UICONTROL Chiave principale servizio].

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** quindi lascia un po’ di tempo per l’istituzione del nuovo account.

![Interfaccia di autenticazione della chiave service-principal.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Dynamics] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).
