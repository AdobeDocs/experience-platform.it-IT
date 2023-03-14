---
keywords: Experience Platform;home;argomenti popolari;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Creare una connessione sorgente Salesforce Service Cloud nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Salesforce Service Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Creare un [!DNL Salesforce Service Cloud] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Salesforce Service Cloud] (di seguito &quot;SSC&quot;) che utilizza il connettore di origine [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione SSC valida, puoi saltare il resto del documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Per accedere al tuo account SSC su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Il nome utente dell’account utente. |
| `password` | Password dell&#39;account utente. |
| `securityToken` | Token di sicurezza per l’account utente. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Salesforce Service Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Connetti [!DNL Salesforce Service Cloud] account

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account SSC a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Customer Success]** categoria, seleziona **[!UICONTROL Salesforce Service Cloud]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore SSC.

![catalogo](../../../../images/tutorials/create/ssc/catalog.png)

Il **[!UICONTROL Connetti a Salesforce Service Cloud]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali SSC. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/ssc/connect.png)

### Account esistente

Per connettere un account esistente, seleziona l’account SSC con cui desideri connetterti, quindi fai clic su **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/ssc/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SSC. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di successo del cliente in [!DNL Platform]](../../dataflow/customer-success.md).
