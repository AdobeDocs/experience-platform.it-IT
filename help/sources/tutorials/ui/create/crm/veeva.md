---
keywords: Experience Platform;home;argomenti popolari;Veeva CRM;veeva
solution: Experience Platform
title: Creare una connessione veeva CRM Source nell'interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Veeva CRM utilizzando l’interfaccia utente Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Veeva CRM] nell&#39;interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Veeva CRM] utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Veeva CRM] valido, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | URL dell&#39;istanza sorgente [!DNL Veeva CRM]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Veeva CRM]. |
| `password` | Password dell&#39;account utente [!DNL Veeva CRM]. |
| `securityToken` | Token di sicurezza per l&#39;account utente [!DNL Veeva CRM]. |

Per ulteriori informazioni su come iniziare, consulta [questo documento Veeva CRM]

## Connetti il tuo account [!DNL Veeva CRM]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Veeva CRM] a [!DNL Platform].

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Origini]. La schermata [!UICONTROL Catalogo] visualizza una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria [!UICONTROL CRM], selezionare **[!UICONTROL Veeva CRM]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/veeva/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account CRM Veeva]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Veeva CRM] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/veeva/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali [!DNL Veeva CRM]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**, quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/veeva/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Veeva CRM] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).
