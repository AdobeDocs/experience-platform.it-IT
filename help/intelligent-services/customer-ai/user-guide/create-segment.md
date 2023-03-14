---
keywords: Experience Platform;approfondimenti;customer ai;argomenti popolari;segmenti customer ai
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Creare segmenti di clienti con punteggi previsti
description: Al termine di un’esecuzione di previsione, i punteggi di propensione previsti vengono utilizzati automaticamente dai profili. L’arricchimento dei profili con i punteggi di IA per l’analisi dei clienti consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di tendenza. Questa sezione descrive i passaggi da seguire per creare segmenti con il Generatore di segmenti.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Creare segmenti di clienti con punteggi previsti

Al termine di un’esecuzione di previsione, i punteggi di propensione previsti vengono utilizzati automaticamente dai profili. L’arricchimento dei profili con i punteggi di IA per l’analisi dei clienti consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di tendenza. Questa sezione descrive i passaggi da seguire per creare segmenti con il Generatore di segmenti. Per un tutorial più completo sulla creazione dei segmenti, consulta [Guida utente di Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario abilitare Real-Time Customer Profile per il set di dati.

Nell’interfaccia utente di Platform, fai clic su **[!UICONTROL Segmenti]** nel menu di navigazione a sinistra, quindi fai clic su **[!UICONTROL Crea segmento]**.

![](../images/user-guide/segments.png)

Il **Generatore di segmenti** viene visualizzato. Da sinistra **[!UICONTROL Campi]** e sotto **[!UICONTROL Attributi]** , fare clic sulla cartella denominata **[!UICONTROL Profilo individuale XDM]** quindi fai clic sulla cartella con il namespace della tua organizzazione. La cartella denominata **[!UICONTROL IA per l’analisi dei clienti]** contiene i risultati delle esecuzioni delle previsioni e sono denominati in base all’istanza a cui appartengono i punteggi. Fai clic su una cartella di istanze per accedere ai risultati dell’istanza desiderata.

![](../images/user-guide/results.png)

Situato al centro del Generatore di segmenti, trascina e rilascia il file **[!UICONTROL Punteggio]** attributo su *area di lavoro generatore regole* per definire una regola.

Sotto la mano destra *Proprietà segmento* , fornisci un nome per il segmento.

![](../images/user-guide/properties.png)

Sopra la mano sinistra *Campi* , fare clic sul pulsante **ingranaggio** e seleziona un&#39;icona *Criterio di unione* dal menu a discesa. Clic **[!UICONTROL Salva]** per creare il segmento.

![](../images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, hai trovato correttamente i tipi di pubblico in base ai loro punteggi di tendenza utilizzando il Generatore di segmenti. Ora puoi indirizzare il pubblico attivandolo nelle destinazioni. Consulta la [panoramica sulle destinazioni](../../../destinations/home.md) per ulteriori informazioni.
