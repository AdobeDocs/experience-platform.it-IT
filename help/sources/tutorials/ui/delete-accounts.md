---
keywords: Experience Platform;home;argomenti popolari; eliminare gli account
description: I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per l'eliminazione degli account dall'area di lavoro Origini.
solution: Experience Platform
title: Eliminare gli account di connessione sorgente nell’interfaccia utente
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Elimina account di connessione di origine

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per eliminare account da **[!UICONTROL Origini]** workspace.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Eliminare gli account tramite l’interfaccia utente

>[!TIP]
>
>Prima di eliminare l&#39;account di origine, è necessario eliminare tutti i flussi di dati esistenti associati all&#39;account di origine. Per eliminare i flussi di dati esistenti, consulta l’esercitazione su [eliminazione dei flussi di dati di origini nell’interfaccia utente](./delete.md).

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse origini per le quali è possibile creare account e flussi di dati. Ciascuna origine mostra il numero di account e flussi di dati esistenti ad essi associati.

Seleziona **[!UICONTROL Account]** per accedere al **[!UICONTROL Account]** pagina.

![cataloghi](../../images/tutorials/delete-accounts/catalog.png)

Viene visualizzato un elenco di account esistenti. In questa pagina è riportato un elenco di informazioni ordinabili per account esistenti come origine, nome utente, flussi di dati associati e data di creazione. Seleziona la **icona funnel** in alto a sinistra per ordinare.

![elenco di dati](../../images/tutorials/delete-accounts/accounts.png)

Il pannello di ordinamento viene visualizzato sul lato sinistro dello schermo, contenente un elenco delle sorgenti disponibili. È possibile selezionare più sorgenti utilizzando la funzione di ordinamento.

Selezionare l&#39;origine a cui si desidera accedere e individuare l&#39;account che si desidera eliminare dall&#39;elenco degli account nell&#39;interfaccia principale. Nell’esempio, l’origine selezionata è **[!DNL Azure Blob Storage]** e il nome dell&#39;account è **[!UICONTROL blobTestConnector]**. Quando selezioni più sorgenti dal pannello di ordinamento, vengono visualizzati per primi gli account creati più di recente, perché l’elenco viene ordinato in base alla data di creazione.

Seleziona l’account da eliminare.

![ordinamento dei dati](../../images/tutorials/delete-accounts/sort.png)

La **[!UICONTROL Proprietà]** sul lato destro dello schermo viene visualizzato un pannello contenente informazioni relative all’account selezionato.

Seleziona i puntini di sospensione (`...`) accanto al nome dell’account da eliminare. Viene visualizzato un pannello a comparsa che fornisce le opzioni per **[!UICONTROL Aggiungi dati]**, **[!UICONTROL Modifica dettagli]** e **[!UICONTROL Elimina]**. Seleziona **[!UICONTROL Elimina]** per eliminare l’account.

![ordinamento dei dati](../../images/tutorials/delete-accounts/delete.png)

Viene visualizzata una finestra di dialogo di conferma finale, seleziona **[!UICONTROL Elimina]** per completare il processo.

![delete](../../images/tutorials/delete-accounts/confirm.png)

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente il **[!UICONTROL Origini]** area di lavoro per eliminare gli account esistenti.

Per i passaggi su come eseguire queste operazioni a livello di programmazione utilizzando il [!DNL Flow Service] API, consulta l’esercitazione su [eliminazione di connessioni tramite l’API del servizio di flusso](../../tutorials/api/delete.md)
