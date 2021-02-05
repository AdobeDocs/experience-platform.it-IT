---
keywords: ' Experience Platform;informazioni;customer ai;argomenti più comuni;customer ai segmenti'
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Creazione di segmenti di clienti con punteggi previsti
topic: Create a segment
description: Al termine di un'esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati da Profili. L'arricchimento dei profili con i punteggi AI dei clienti consente di creare segmenti di clienti per trovare audience in base ai loro punteggi di propensione. Questa sezione descrive i passaggi per la creazione di segmenti con Segment Builder (Generatore di segmenti).
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Creazione di segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati da Profili. L&#39;arricchimento dei profili con i punteggi AI dei clienti consente di creare segmenti di clienti per trovare audience in base ai loro punteggi di propensione. Questa sezione descrive i passaggi per la creazione di segmenti con Segment Builder (Generatore di segmenti). Per un&#39;esercitazione più affidabile sulla creazione di segmenti, vedete la [Guida utente di Segment Builder](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario abilitare il profilo cliente in tempo reale per il set di dati.

Nell&#39;interfaccia utente della piattaforma, fate clic su **[!UICONTROL Segments]** nella barra di navigazione a sinistra, quindi fate clic su **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

Viene visualizzato il **Generatore di segmenti**. Dalla colonna a sinistra **[!UICONTROL Fields]** e nella scheda **[!UICONTROL Attributes]** fare clic sulla cartella denominata **[!UICONTROL XDM Individual Profile]**, quindi fare clic sulla cartella contenente lo spazio dei nomi dell&#39;organizzazione. La cartella denominata **[!UICONTROL Customer AI]** contiene i risultati delle esecuzioni di previsione e prende il nome dall&#39;istanza a cui appartengono i punteggi. Fate clic su una cartella di istanza per accedere ai risultati dell’istanza desiderata.

![](../images/user-guide/results.png)

Situato al centro di Segment Builder (Generatore di segmenti), trascina e rilascia l&#39;attributo **[!UICONTROL Score]** nell&#39;area di lavoro del generatore di regole *per definire una regola.*

Nella colonna di destra *Proprietà segmento*, specificare un nome per il segmento.

![](../images/user-guide/properties.png)

Sopra la colonna a sinistra *Campi*, fare clic sull&#39;icona **ingranaggio** e selezionare un *Unisci criteri* dal menu a discesa. Fare clic su **[!UICONTROL Save]** per creare il segmento.

![](../images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, con Segment Builder (Generatore di segmenti) è stato possibile trovare le audience in base ai loro punteggi di tendenza. Ora potete eseguire il targeting delle audience attivandole nelle destinazioni. Per ulteriori informazioni, vedere la [panoramica delle destinazioni](../../../destinations/home.md).