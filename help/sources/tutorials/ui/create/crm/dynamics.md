---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics;home;popular topic;Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Creare una connessione Microsoft Dynamics Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine Microsoft Dynamics utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---

# Crea una connessione sorgente [!DNL Microsoft Dynamics] nell&#39;interfaccia utente

Questo tutorial illustra i passaggi necessari per creare una connessione di origine [!DNL Microsoft Dynamics] (di seguito &quot;[!DNL Dynamics]&quot;) tramite l&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Dynamics] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati per un&#39;origine CRM](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per autenticare l&#39;origine [!DNL Dynamics], è necessario fornire i valori per le proprietà di connessione seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione di base]

| Credenziali | Descrizione |
| --- | --- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Dynamics]. |
| `password` | Password per l&#39;account [!DNL Dynamics]. |

>[!TAB Autenticazione Service-principal e chiave]

| Credenziali | Descrizione |
| --- | --- |
| `servicePrincipalId` | ID client dell&#39;account [!DNL Dynamics]. Questo ID è necessario quando si utilizza l’entità servizio e l’autenticazione basata su chiave. |
| `servicePrincipalKey` | Chiave segreta dell&#39;entità servizio. Questa credenziale è necessaria quando si utilizza l&#39;entità servizio e l&#39;autenticazione basata su chiave. |

>[!ENDTABS]

Per ulteriori informazioni, consulta [questo [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Connetti il tuo account [!DNL Dynamics]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL CRM], selezionare **[!UICONTROL Microsoft Dynamics]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con Microsoft Dynamics selezionato.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account Microsoft Dynamics]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Dynamics] che desideri utilizzare, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per procedere.

![Interfaccia account esistente.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Nuovo account

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Dynamics]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]**, quindi specificare un nome e una descrizione facoltativa per il nuovo account [!DNL Dynamics].

![Nuova interfaccia per la creazione dell&#39;account.](../../../../images/tutorials/create/ms-dynamics/new.png)

Durante la creazione di un account [!DNL Dynamics] è possibile utilizzare l&#39;autenticazione di base o l&#39;autenticazione con chiave e entità servizio.

>[!BEGINTABS]

>[!TAB Autenticazione di base]

Per creare un account [!DNL Dynamics] con autenticazione di base, selezionare [!UICONTROL Autenticazione di base], quindi specificare i valori per l&#39;[!UICONTROL URI servizio], [!UICONTROL Nome utente] e [!UICONTROL Password]. **Nota**: l&#39;autenticazione di base in [!DNL Dynamics] potrebbe essere bloccata da un&#39;autenticazione a due fattori, attualmente non supportata da Platform. In questo caso, si consiglia di utilizzare l&#39;autenticazione basata su chiave per creare un connettore di origine utilizzando [!DNL Dynamics].

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per l&#39;impostazione del nuovo account.

![Interfaccia di autenticazione di base.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Autenticazione Service-principal e chiave]

Per creare un account [!DNL Dynamics] con autenticazione service-principal e chiave, selezionare **[!UICONTROL Autenticazione service-principal e chiave]**, quindi specificare i valori per l&#39;[!UICONTROL ID service principal] e la [!UICONTROL chiave service principal].

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per l&#39;impostazione del nuovo account.

![Interfaccia di autenticazione della chiave service-principal.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Dynamics]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/crm.md).
