---
keywords: Experience Platform;home;argomenti popolari;Veeva CRM;veeva
solution: Experience Platform
title: Creare una connessione Source a Veeva CRM nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del sistema CRM Veeva utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Veeva CRM] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Veeva CRM] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Veeva CRM] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | URL dell&#39;istanza di origine [!DNL Veeva CRM]. |
| `username` | Nome utente per l&#39;account utente [!DNL Veeva CRM]. |
| `password` | Password per l&#39;account utente [!DNL Veeva CRM]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Veeva CRM]. |

Per ulteriori informazioni, consulta questo [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Connetti il tuo account [!DNL Veeva CRM]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Veeva CRM] a [!DNL Platform].

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL CRM] selezionare **[!UICONTROL Veeva CRM]**, quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/veeva/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account CRM Veeva]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Veeva CRM] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/veeva/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali di [!DNL Veeva CRM]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/veeva/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Veeva CRM]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/crm.md).
