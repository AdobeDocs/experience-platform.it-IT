---
keywords: Experience Platform;home;argomenti popolari;ServiceNow;servicenow
solution: Experience Platform
title: Creare una connessione Source ServiceNow nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente ServiceNow utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL ServiceNow] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL ServiceNow] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL ServiceNow] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL ServiceNow] in [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | Endpoint del server [!DNL ServiceNow]. |
| `username` | Nome utente utilizzato per connettersi al server [!DNL ServiceNow] per l&#39;autenticazione. |
| `password` | Password per la connessione al server [!DNL ServiceNow] per l&#39;autenticazione. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL ServiceNow] documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Connetti il tuo account [!DNL ServiceNow]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL ServiceNow] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Customer Success]**, seleziona **[!UICONTROL ServiceNow]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Connetti origine]** per creare un nuovo connettore [!DNL ServiceNow].

![](../../../../images/tutorials/create/servicenow/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a ServiceNow]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali [!DNL ServiceNow]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/servicenow/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL ServiceNow] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL ServiceNow]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/customer-success.md).
