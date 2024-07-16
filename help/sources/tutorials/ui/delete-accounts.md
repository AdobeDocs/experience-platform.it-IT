---
keywords: Experience Platform;home;argomenti popolari; eliminare gli account
description: I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questa esercitazione fornisce i passaggi per eliminare gli account dall’area di lavoro Origini.
solution: Experience Platform
title: Eliminare gli account di connessione Source nell’interfaccia utente
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Elimina account di connessione di origine

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questa esercitazione fornisce i passaggi per eliminare gli account dall&#39;area di lavoro **[!UICONTROL Sources]**.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminare gli account tramite l’interfaccia utente

>[!TIP]
>
>Prima di eliminare l’account di origine, devi eliminare tutti i flussi di dati esistenti associati all’account di origine. Per eliminare i flussi di dati esistenti, fare riferimento all&#39;esercitazione su [eliminazione dei flussi di dati di origine nell&#39;interfaccia utente](./delete.md).

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare account e flussi di dati con. Ogni origine mostra il numero di account e flussi di dati esistenti ad essi associati.

Selezionare **[!UICONTROL Account]** per accedere alla pagina **[!UICONTROL Account]**.

![account-catalogo](../../images/tutorials/delete-accounts/catalog.png)

Viene visualizzato un elenco degli account esistenti. In questa pagina è disponibile un elenco di informazioni ordinabili per gli account esistenti, ad esempio origine, nome utente, flussi di dati associati e data di creazione. Seleziona l&#39;icona **funnel** in alto a sinistra per ordinare.

![elenco di flussi di dati](../../images/tutorials/delete-accounts/accounts.png)

Il pannello di ordinamento viene visualizzato sul lato sinistro dello schermo e contiene un elenco delle sorgenti disponibili. È possibile selezionare più origini utilizzando la funzione di ordinamento.

Seleziona l’origine a cui desideri accedere e individua l’account da eliminare dall’elenco degli account nell’interfaccia principale. Nell&#39;esempio, l&#39;origine selezionata è **[!DNL Azure Blob Storage]** e il nome account è **[!UICONTROL blobTestConnector]**. Quando si selezionano più origini dal pannello di ordinamento, vengono visualizzati per primi gli account creati più di recente, poiché l’elenco è ordinato in base alla data di creazione.

Selezionare l&#39;account che si desidera eliminare.

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

Il pannello **[!UICONTROL Proprietà]** viene visualizzato sul lato destro dello schermo e contiene informazioni relative all&#39;account selezionato.

Selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account che si desidera eliminare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL Aggiungere dati]**, **[!UICONTROL Modificare dettagli]** e **[!UICONTROL Eliminare]**. Seleziona **[!UICONTROL Elimina]** per eliminare l&#39;account.

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale. Selezionare **[!UICONTROL Elimina]** per completare il processo.

![elimina](../../images/tutorials/delete-accounts/confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro **[!UICONTROL Sources]** per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fare riferimento al tutorial sull&#39;eliminazione di connessioni con l&#39;API del servizio Flusso](../../tutorials/api/delete.md)[
