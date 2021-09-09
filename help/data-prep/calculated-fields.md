---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare csv su xdm;guida interfaccia utente;mappatura;mappatura;preparazione dati;preparazione dati;preparazione dei dati;
solution: Experience Platform
title: Panoramica sulla preparazione dei dati
topic-legacy: overview
description: Questo documento introduce Data Prep in Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Campi calcolati

I campi calcolati consentono la creazione di valori in base agli attributi nello schema di input. Questi valori possono quindi essere assegnati agli attributi nello schema di destinazione e ricevere un nome e una descrizione per facilitarne il riferimento.

Per creare un campo calcolato, selezionare **[!UICONTROL Aggiungi campo calcolato]**.

![](./images/calculated-fields/add-calculated-field.png)

Viene visualizzato il pannello **[!UICONTROL Crea campo calcolato]** . La finestra di dialogo a sinistra contiene i campi, le funzioni e gli operatori supportati nei campi calcolati. Seleziona una delle schede per iniziare ad aggiungere funzioni, campi o operatori all’editor di espressioni.

![](./images/calculated-fields/create-calculated-field.png)

| Scheda | Descrizione |
| --- | ----------- |
| Funzione | Nella scheda Funzioni sono elencate le funzioni disponibili per la trasformazione dei dati. Per ulteriori informazioni sulle funzioni che è possibile utilizzare all&#39;interno dei campi calcolati, leggere la guida sulle funzioni [Preparazione dati (mappatore)](./functions.md). |
| Campo | Nella scheda Campi sono elencati i campi e gli attributi disponibili nello schema di origine. |
| Operatore | La scheda operatori elenca gli operatori disponibili per la trasformazione dei dati. |

Puoi aggiungere manualmente campi, funzioni e operatori utilizzando l’editor espressioni al centro. Seleziona l’editor per iniziare a creare un’espressione.

![](./images/calculated-fields/write-calculated-field.png)

Selezionare **[!UICONTROL Salva]** per continuare.

La schermata di mappatura viene visualizzata nuovamente con il campo sorgente appena creato. Applica il campo di destinazione corrispondente appropriato e seleziona **[!UICONTROL Fine]** per completare la mappatura.

![](./images/calculated-fields/new-calculated-field.png)