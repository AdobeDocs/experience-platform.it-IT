---
keywords: Experience Platform;approfondimenti;customer ai;argomenti popolari;segmenti di customer ai
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Creare segmenti di clienti con punteggi previsti
topic-legacy: Create a segment
description: Al termine di un'esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati dai profili. L’arricchimento dei profili con i punteggi di Customer AI consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di propensione. Questa sezione descrive i passaggi necessari per creare segmenti utilizzando il Generatore di segmenti.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Creare segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati dai profili. L’arricchimento dei profili con i punteggi di Customer AI consente di creare segmenti di clienti per trovare tipi di pubblico in base ai loro punteggi di propensione. Questa sezione descrive i passaggi necessari per creare segmenti utilizzando il Generatore di segmenti. Per un&#39;esercitazione più efficace sulla creazione dei segmenti, consulta la [Guida utente di Generatore di segmenti](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario abilitare Profilo cliente in tempo reale per il set di dati.

Nell’interfaccia utente di Platform, fai clic su **[!UICONTROL Segments]** nel menu di navigazione a sinistra, quindi fai clic su **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

Viene visualizzato il **Generatore di segmenti**. Dalla colonna **[!UICONTROL Fields]** a sinistra e sotto la scheda **[!UICONTROL Attributes]** , fai clic sulla cartella denominata **[!UICONTROL XDM Individual Profile]** e quindi fai clic sulla cartella con lo spazio dei nomi dell’organizzazione. La cartella denominata **[!UICONTROL Customer AI]** contiene i risultati delle esecuzioni della previsione e prende il nome dall’istanza a cui appartengono i punteggi. Fai clic su una cartella di istanza per accedere ai risultati dell’istanza desiderata.

![](../images/user-guide/results.png)

Situato al centro del Generatore di segmenti, trascina e rilascia l’attributo **[!UICONTROL Score]** sull’ *area di lavoro del generatore di regole* per definire una regola.

Nella colonna a destra *Proprietà segmento* , inserisci un nome per il segmento.

![](../images/user-guide/properties.png)

Sopra la colonna sinistra *Campi*, fai clic sull&#39;icona **ingranaggio** e seleziona un *Criterio di unione* dal menu a discesa. Fai clic su **[!UICONTROL Save]** per creare il segmento.

![](../images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, hai trovato correttamente i tipi di pubblico in base ai loro punteggi di propensione utilizzando il Generatore di segmenti. Ora puoi eseguire il targeting dei tuoi tipi di pubblico attivandoli nelle destinazioni. Per ulteriori informazioni, consulta la [panoramica delle destinazioni](../../../destinations/home.md) .
