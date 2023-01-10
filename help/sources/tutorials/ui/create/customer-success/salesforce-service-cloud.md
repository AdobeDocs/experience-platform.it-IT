---
keywords: Experience Platform;home;argomenti popolari;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: Creare una connessione Salesforce Service Cloud Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Salesforce Service Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Crea un [!DNL Salesforce Service Cloud] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Salesforce Service Cloud] (in seguito denominato &quot;SSC&quot;) connettore di sorgente che utilizza [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione SSC valida, è possibile saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli credenziali richieste

Per accedere al tuo account SSC su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `username` | Nome utente dell&#39;account utente. |
| `password` | Password dell&#39;account utente. |
| `securityToken` | Token di sicurezza per l’account utente. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Salesforce Service Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Collega il tuo [!DNL Salesforce Service Cloud] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account SSC a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Successo del cliente]** categoria, seleziona **[!UICONTROL Cloud di servizi Salesforce]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore SSC.

![catalogo](../../../../images/tutorials/create/ssc/catalog.png)

La **[!UICONTROL Connessione a Salesforce Service Cloud]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le tue credenziali SSC. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account SSC con cui si desidera connettersi, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/ssc/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account SSC. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati di successo del cliente in [!DNL Platform]](../../dataflow/customer-success.md).
