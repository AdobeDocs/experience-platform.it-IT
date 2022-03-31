---
keywords: Experience Platform;approfondimenti;customer ai;argomenti popolari;segmenti di customer ai
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Creare segmenti di clienti con punteggi previsti
topic-legacy: Create a segment
description: Al termine di un'esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati dai profili. L’arricchimento dei profili con i punteggi di Customer AI consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di propensione. Questa sezione descrive i passaggi necessari per creare segmenti utilizzando il Generatore di segmenti.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# Creare segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati dai profili. L’arricchimento dei profili con i punteggi di Customer AI consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di propensione. Questa sezione descrive i passaggi necessari per creare segmenti utilizzando il Generatore di segmenti. Per un’esercitazione più efficace sulla creazione dei segmenti, consulta la sezione [Guida utente di Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario abilitare Profilo cliente in tempo reale per il set di dati.

Nell’interfaccia utente di Platform, fai clic su **[!UICONTROL Segmenti]** nella navigazione a sinistra, quindi fai clic su **[!UICONTROL Creare un segmento]**.

![](../images/user-guide/segments.png)

La **Generatore di segmenti** appare. Da sinistra **[!UICONTROL Campi]** e sotto **[!UICONTROL Attributi]** fare clic sulla cartella denominata **[!UICONTROL Profilo individuale XDM]** quindi fai clic sulla cartella con lo spazio dei nomi dell’organizzazione. La cartella denominata **[!UICONTROL Customer AI]** contiene i risultati delle esecuzioni delle previsioni e vengono denominati in base all’istanza a cui appartengono i punteggi. Fai clic su una cartella di istanza per accedere ai risultati dell’istanza desiderata.

![](../images/user-guide/results.png)

Situato al centro del Generatore di segmenti, trascina e rilascia la **[!UICONTROL Punteggio]** attributo *area di lavoro del generatore di regole* per definire una regola.

Sotto la destra *Proprietà del segmento* Specifica un nome per il segmento.

![](../images/user-guide/properties.png)

Sopra la sinistra *Campi* fai clic sulla colonna **ingranaggio** e seleziona una *Criteri di unione* dal menu a discesa. Fai clic su **[!UICONTROL Salva]** per creare il segmento.

![](../images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, hai trovato correttamente i tipi di pubblico in base ai loro punteggi di propensione utilizzando il Generatore di segmenti. Ora puoi eseguire il targeting dei tuoi tipi di pubblico attivandoli nelle destinazioni. Consulta la sezione [panoramica sulle destinazioni](../../../destinations/home.md) per ulteriori informazioni.
