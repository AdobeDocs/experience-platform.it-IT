---
keywords: Experience Platform;home;argomenti popolari; eliminare gli account
description: I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per l'eliminazione degli account dall'area di lavoro Origini.
solution: Experience Platform
title: Eliminare gli account di connessione sorgente nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Elimina account di connessione di origine

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per eliminare gli account dall&#39;area di lavoro **[!UICONTROL Sources]**.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminare gli account tramite l’interfaccia utente

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. La schermata **[!UICONTROL Catalog]** visualizza una varietà di sorgenti con cui è possibile creare account e flussi di dati. Ciascuna origine mostra il numero di account e flussi di dati esistenti ad essi associati.

Seleziona **[!UICONTROL Accounts]** per accedere alla pagina **[!UICONTROL Accounts]**.

![cataloghi](../../images/tutorials/delete-accounts/catalog.png)

Viene visualizzato un elenco di account esistenti. In questa pagina è riportato un elenco di informazioni ordinabili per account esistenti come origine, nome utente, flussi di dati associati e data di creazione. Seleziona l&#39;icona **funnel** in alto a sinistra per ordinare.

![elenco di dati](../../images/tutorials/delete-accounts/accounts.png)

Il pannello di ordinamento viene visualizzato sul lato sinistro dello schermo, contenente un elenco delle sorgenti disponibili. È possibile selezionare più sorgenti utilizzando la funzione di ordinamento.

Selezionare l&#39;origine a cui si desidera accedere e individuare l&#39;account che si desidera eliminare dall&#39;elenco degli account nell&#39;interfaccia principale. Nell’esempio, l’origine selezionata è **[!DNL Azure Blob Storage]** e il nome dell’account è **[!UICONTROL blobTestConnector]**. Quando selezioni più sorgenti dal pannello di ordinamento, vengono visualizzati per primi gli account creati più di recente, perché l’elenco viene ordinato in base alla data di creazione.

Seleziona l’account da eliminare.

![ordinamento dei dati](../../images/tutorials/delete-accounts/sort.png)

Il pannello **[!UICONTROL Properties]** viene visualizzato sul lato destro dello schermo, contenente informazioni relative all’account selezionato.

Selezionare i puntini di sospensione (`...`) accanto al nome dell&#39;account che si desidera eliminare. Viene visualizzato un pannello a comparsa che fornisce opzioni per **[!UICONTROL Add data]**, **[!UICONTROL Edit details]** e **[!UICONTROL Delete]**. Seleziona **[!UICONTROL Delete]** per eliminare l’account.

![ordinamento dei dati](../../images/tutorials/delete-accounts/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale, selezionare **[!UICONTROL Delete]** per completare il processo.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l’area di lavoro **[!UICONTROL Sources]** per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando l&#39;API [!DNL Flow Service], fai riferimento all&#39;esercitazione su [eliminazione di connessioni utilizzando l&#39;API del servizio di flusso](../../tutorials/api/delete.md)
