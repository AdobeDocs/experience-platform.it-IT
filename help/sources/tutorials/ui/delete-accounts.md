---
keywords: Experience Platform;home;popular topics; delete accounts
description: I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per eliminare gli account dall'area di lavoro Origini.
solution: Experience Platform
title: Elimina account
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Elimina account

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per eliminare gli account dall&#39; **[!UICONTROL Sources]** area di lavoro.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminazione di account tramite l&#39;interfaccia utente

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse origini per le quali è possibile creare account e flussi di dati. Ogni origine mostra il numero di account e di flussi di dati esistenti ad essi associati.

Selezionate **[!UICONTROL Accounts]** per accedere alla **[!UICONTROL Accounts]** pagina.

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

Viene visualizzato un elenco di account esistenti. In questa pagina è presente un elenco di informazioni ordinabili per gli account esistenti, quali origine, nome utente, flussi di dati associati e data di creazione. Selezionate l’icona **** funnel in alto a sinistra per ordinare i dati.

![elenco dei flussi di dati](../../images/tutorials/delete-accounts/accounts.png)

Il pannello di ordinamento viene visualizzato sul lato sinistro dello schermo, contenente un elenco delle sorgenti disponibili. È possibile selezionare più origini utilizzando la funzione di ordinamento.

Selezionare l&#39;origine a cui si desidera accedere e individuare l&#39;account che si desidera eliminare dall&#39;elenco degli account nell&#39;interfaccia principale. Nell&#39;esempio, l&#39;origine selezionata è **[!DNL Azure Blob Storage]** e il nome dell&#39;account è **[!UICONTROL blobTestConnector]**. Quando si selezionano più origini dal pannello di ordinamento, gli account creati più di recente vengono visualizzati per primi, perché l&#39;elenco è ordinato in base alla data di creazione.

Selezionate l’account da eliminare.

![ordinamento dei dati](../../images/tutorials/delete-accounts/sort.png)

Il **[!UICONTROL Properties]** pannello viene visualizzato sul lato destro dello schermo, contenente le informazioni relative all’account selezionato.

Selezionate le ellissi (`...`) accanto al nome dell’account che intendete eliminare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** e **[!UICONTROL Delete]**. Selezionate **[!UICONTROL Delete]** per eliminare l’account.

![ordinamento dei dati](../../images/tutorials/delete-accounts/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale; selezionate **[!UICONTROL Delete]** per completare il processo.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, l&#39;area di lavoro **[!UICONTROL Sources]** è stata utilizzata per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39; [!DNL Flow Service] API, fare riferimento all&#39;esercitazione sull&#39; [eliminazione delle connessioni tramite l&#39;API del servizio di flusso](../../tutorials/api/delete.md)