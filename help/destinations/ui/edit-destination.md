---
title: Modificare le destinazioni
type: Tutorial
description: Scopri come modificare e aggiornare gli account di destinazioni esistenti nell’interfaccia utente di Adobe Experience Platform
badgeBeta: label="Beta" type="Informative"
exl-id: f3298836-668b-43fb-b4f3-85a650766f05
source-git-commit: 990fe9162c5b2970f269a5b0668916b7b6e61f44
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Modificare le destinazioni

Scopri come modificare vari componenti di una connessione di destinazione esistente, tra cui come aggiornare le credenziali di autenticazione, la posizione di esportazione e altro ancora utilizzando l’interfaccia utente di Experience Platform.

>[!IMPORTANT]
>
>Questa funzionalità è disponibile in versione beta solo per alcuni clienti. Per richiedere l’accesso, contatta il tuo rappresentante Adobe.

>[!NOTE]
>
> Le operazioni di modifica descritte in questo tutorial sono supportate anche tramite operazioni API. Per ulteriori informazioni, leggi il tutorial su come [modificare le destinazioni nell&#39;API](/help/destinations/api/edit-destination.md).

Per modificare vari componenti di una connessione di destinazione esistente:

1. Passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]**.
2. Seleziona la destinazione desiderata da modificare.
3. Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Nome] e utilizzare il controllo ![Modifica destinazione](/help/images/icons/edit.png)**[!UICONTROL Modifica destinazione ]**per modificare le connessioni di destinazione esistenti.
4. Nella finestra modale, modifica le impostazioni desiderate. Al termine, seleziona **[!UICONTROL Salva]**.

Nella finestra di modifica della destinazione è possibile aggiornare tutte le impostazioni configurate al momento della connessione iniziale alla destinazione. Queste impostazioni sono diverse in base alla piattaforma di destinazione che stai aggiornando.

A seconda della configurazione della destinazione, alcuni campi potrebbero essere di sola lettura e non possono essere modificati. Per modificare il valore dei campi di sola lettura, è necessario [creare una nuova connessione di destinazione](../ui/connect-destination.md) con i nuovi valori dei campi.

![Schermata che mostra un campo di sola lettura.](../assets/ui/edit-destinations/read-only.png)

Di seguito sono riportati alcuni esempi delle impostazioni che è possibile aggiornare per [Amazon S3](../catalog/cloud-storage/amazon-s3.md), [Azure Event Hubs](../catalog/cloud-storage/azure-event-hubs.md) e [Google Ads](../catalog/advertising/google-ads-destination.md) destinazioni.

<div style="display: flex; gap: 12px; justify-content: flex-start; align-items: flex-start;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-amazon-s3-connection.png" alt="Finestra Modifica destinazione per la destinazione Amazon S3." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-eventhubs-connection.png" alt="Schermata Modifica destinazione per la destinazione Azure EventHubs." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
  <img class="modal-image" src="../assets/ui/edit-destinations/edit-google-ads-connection.png" alt="Schermata Modifica destinazione per la destinazione Google Ads." style="max-width: 200px; height: auto; border: 1px solid #ccc;">
</div>

>[!SUCCESS]
>
>Le impostazioni della connessione di destinazione sono state aggiornate.

## Altre opzioni di modifica

Utilizzando l’interfaccia utente di Experience Platform o l’API del servizio Flusso, puoi modificare diverse configurazioni di destinazione, come descritto nei collegamenti seguenti:

| Utilizzo dell’interfaccia utente di Experience Platform | Utilizzo dell’API del servizio Flusso |
|---------|----------|
| Modifica connessioni di destinazione (questa pagina) | [Modifica componenti di connessione di destinazione (percorso di archiviazione e altri componenti)](/help/destinations/api/edit-destination.md#patch-target-connection) |
| [Modifica account](/help/destinations/ui/update-accounts.md) | [Modifica componenti di connessione di base (parametri di autenticazione e altri componenti)](/help/destinations/api/edit-destination.md#patch-base-connection) |
| [Modifica flussi di dati di attivazione](/help/destinations/ui/edit-activation.md) | [Aggiorna flussi di dati di destinazione](/help/destinations/api/update-destination-dataflows.md) |

## Passaggi successivi

Seguendo questa esercitazione, hai utilizzato correttamente l&#39;area di lavoro **[!UICONTROL destinazioni]** per aggiornare le connessioni di destinazione esistenti.

Per ulteriori informazioni sulle destinazioni, consulta la [panoramica sulle destinazioni](../catalog/overview.md).
