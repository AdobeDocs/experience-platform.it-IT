---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;mapper;mappare;preparazione dati;preparazione dati;preparazione dati;
solution: Experience Platform
title: Panoramica sulla preparazione dati
description: Questo documento introduce la preparazione dati in Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---

# Campi calcolati

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati ad attributi nello schema di destinazione e ricevere un nome e una descrizione per consentire un riferimento più semplice.

Per creare un campo calcolato, selezionare **[!UICONTROL Aggiungi campo calcolato]**.

![](./images/calculated-fields/add-calculated-field.png)

Viene visualizzato il pannello **[!UICONTROL Crea campo calcolato]**. La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Seleziona una delle schede per iniziare ad aggiungere funzioni, campi o operatori all’editor di espressioni.

![](./images/calculated-fields/create-calculated-field.png)

| Scheda | Descrizione |
| --- | ----------- |
| Funzione | Nella scheda Funzioni sono elencate le funzioni disponibili per la trasformazione dei dati. Per ulteriori informazioni sulle funzioni utilizzabili nei campi calcolati, leggere la guida sulle [funzioni di preparazione dati (mapper)](./functions.md). |
| Campo | Nella scheda Campi sono elencati i campi e gli attributi disponibili nello schema di origine. |
| Operatore | Nella scheda operatori sono elencati gli operatori disponibili per la trasformazione dei dati. |

Puoi aggiungere manualmente campi, funzioni e operatori utilizzando l’editor di espressioni al centro. Seleziona l’editor per iniziare a creare un’espressione.

![](./images/calculated-fields/write-calculated-field.png)

Seleziona **[!UICONTROL Salva]** per continuare.

Viene visualizzata di nuovo la schermata di mappatura con il campo sorgente appena creato. Applica il campo di destinazione corrispondente appropriato e seleziona **[!UICONTROL Fine]** per completare la mappatura.

![](./images/calculated-fields/new-calculated-field.png)
