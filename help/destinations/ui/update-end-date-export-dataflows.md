---
title: Aggiorna la data di fine dei flussi di dati di esportazione del set di dati (azione richiesta entro il 1° maggio 2025)
type: Tutorial
hide: true
hidefromtoc: true
description: Scopri come aggiornare la data di fine dei flussi di dati di esportazione del set di dati con la data di fine corrente del 1° maggio 2025.
source-git-commit: aeabbb56002f8640b79ff3a7e3dc532d01ebbadf
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Aggiorna la data di fine dei flussi di dati di esportazione del set di dati (azione richiesta entro il 1° maggio 2025)

>[!IMPORTANT]
>
>Le azioni elencate in questa pagina si applicano se l’organizzazione ha impostato flussi di dati di esportazione del set di dati prima del rilascio di Experience Platform di settembre 2024.

## Cosa succede?

La versione di Experience Platform[&#128279;](/help/release-notes/latest/latest.md#destinations) di settembre 2024 ha introdotto l&#39;opzione di impostare una data `endTime` per i flussi di dati del set di dati di esportazione. Adobe ha inoltre introdotto una data di fine predefinita del 1° maggio 2025 per tutti i flussi di dati di esportazione del set di dati creati *prima della versione di settembre 2024*. Questi flussi di dati visualizzano attualmente un messaggio simile a quello mostrato di seguito.

![Notifica dell&#39;interfaccia utente sulla necessità di aggiornare la data di fine del flusso di dati del set di dati di esportazione.](/help/destinations/assets/ui/export-datasets/update-end-date.png)

**Elemento azione**: per uno di questi flussi di dati, è necessario aggiornare manualmente la data di fine prima della scadenza; in caso contrario, le esportazioni verranno interrotte. Utilizza l’interfaccia utente di Experience Platform per identificare i flussi di dati impostati per l’interruzione il 1° maggio 2025.

## Perché mi viene inviata una notifica?

La tua organizzazione dispone di flussi di dati di esportazione di set di dati attivi con data di fine 1 maggio 2025.

## Utilizza l’interfaccia utente per aggiornare la data di fine

Utilizza l’interfaccia utente di Experience Platform per identificare i flussi di dati con data di fine 1 maggio 2025 e aggiornarli a una data futura.

### Trovare i flussi di dati da aggiornare

Passa a **Destinazioni > Sfoglia** e cerca il tipo di dati **Set di dati** nella colonna **Tipo di dati**, come illustrato di seguito. Seleziona i flussi di dati desiderati per esaminarli.

![Flussi di dati di esportazione del set di dati evidenziati nella scheda Sfoglia.](/help/destinations/assets/ui/export-datasets/view-dataset-dataflows.png)

### Aggiornare la data di fine dei flussi di dati

Per aggiornare la data di fine dei flussi di dati:

1. Nei flussi di dati selezionati per l&#39;ispezione nel passaggio precedente, selezionare **Esporta set di dati**.
   ![Il controllo Esporta set di dati è evidenziato nella scheda Sfoglia.](/help/destinations/assets/ui/export-datasets/export-datasets-control-highlighted.png)
2. Nel flusso di lavoro, passare al passaggio **Pianificazione** e selezionare **Modifica pianificazione**.
   ![Il controllo Modifica pianificazione è evidenziato nel passaggio Pianificazione.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlighted.png)
3. Scegli una data di fine desiderata dopo il 1° maggio 2025 e seleziona **Salva**.
   ![Selezionare il controllo della data di fine evidenziato nel passaggio Pianificazione.](/help/destinations/assets/ui/export-datasets/select-end-date.png)
4. Procedi alla fine del flusso di lavoro e salva gli aggiornamenti.

Per informazioni dettagliate sul passaggio di pianificazione, consulta l&#39;esercitazione sull&#39;interfaccia utente dei [set di dati di esportazione](/help/destinations/api/export-datasets.md#scheduling).

## Utilizzare l’API per aggiornare la data di fine

### Trovare i flussi di dati da aggiornare

### Aggiornare la data di fine dei flussi di dati
