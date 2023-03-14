---
title: Scheda Rete
description: Scopri come utilizzare la scheda Rete in Adobe Experience Platform Debugger.
keywords: debugger;estensione Debugger di Experience Platform;chrome;estensione;rete;informazioni
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 58%

---

# Scheda Rete

Il **Rete** La scheda aggrega tutte le chiamate della soluzione Adobe Experience Cloud effettuate sulla pagina e le visualizza in ordine da sinistra a destra. I parametri standard vengono etichettati automaticamente con nomi descrittivi e disposti per raggruppare parametri comuni sullo stesso ruolo.

![](images/network.jpg)

Questa schermata è utile per confrontare coppie di valori chiave tra i diversi riscontri. Puoi verificare che i parametri utilizzati per le integrazioni, come Experience Cloud Visitor ID o Supplemental Data ID, siano coerenti tra le diverse integrazioni.

>[!NOTE]
>
>Al momento, non tutti i parametri passati nelle chiamate della soluzione (ad esempio, variabili di contesto di Analytics, parametri personalizzati di Target o ID cliente del servizio Experience Cloud ID) sono visibili nella schermata Rete.

Per cambiare le informazioni in base alla soluzione, seleziona la soluzione da visualizzare dall’elenco nella barra di navigazione a sinistra. Nell’esempio seguente il filtro è impostato in modo da mostrare solo Analytics:

![](images/network-analytics.jpg)

Per visualizzare di nuovo tutte le soluzioni, seleziona **[!UICONTROL Rete]**

Selezionare un elemento nella visualizzazione di rete per visualizzare una visualizzazione espansa. Dalla finestra di visualizzazione espansa, puoi copiare le informazioni visualizzate negli Appunti.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Per cancellare l’elenco, seleziona **[!UICONTROL Rimuovi eventi]**.

Per scaricare un file Excel con le informazioni di questa schermata, seleziona **[!UICONTROL Scarica]**.
