---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Creazione di segmenti di clienti con punteggi previsti
topic: Create a segment
translation-type: tm+mt
source-git-commit: fba6ae701a38737812dccbf4f63e5a07f935ad8b
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Creazione di segmenti di clienti con punteggi previsti

Al termine di un&#39;esecuzione della previsione, i punteggi di propensione previsti vengono automaticamente utilizzati da Profili. L&#39;arricchimento dei profili con i punteggi AI dei clienti consente di creare segmenti di clienti per trovare audience in base ai loro punteggi di propensione. Questa sezione descrive i passaggi per la creazione di segmenti con Segment Builder (Generatore di segmenti). Per un’esercitazione più affidabile sulla creazione di segmenti, consulta la guida [utente di](../../../segmentation/ui/overview.md)Segment Builder (Generatore di segmenti).

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario abilitare il profilo cliente in tempo reale per il set di dati.

Nell’interfaccia utente di Platform, fate clic **[!UICONTROL Segments]** nel menu di navigazione a sinistra, quindi fate clic su **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

Viene visualizzato *Segment Builder (Generatore* di segmenti). Dalla colonna *Campi* a sinistra e nella scheda *Attributi* fare clic sulla cartella denominata **[!UICONTROL XDM Individual Profile]** e quindi sulla cartella con lo spazio dei nomi dell&#39;organizzazione. La cartella denominata **[!UICONTROL Customer AI]** contiene i risultati delle esecuzioni di previsione e prende il nome dall’istanza a cui appartengono i punteggi. Fate clic su una cartella di istanza per accedere ai risultati dell’istanza desiderata.

![](../images/user-guide/results.png)

Situato al centro di Segment Builder (Generatore di segmenti), trascina e rilascia l’ **[!UICONTROL Score]** attributo nell’area di lavoro del generatore di *regole* per definire una regola.

Nella colonna delle proprietà *del* segmento a destra, specifica un nome per il segmento.

![](../images/user-guide/properties.png)

Sopra la colonna *Campi* a sinistra, fate clic sull’icona a forma di **ingranaggio** e selezionate un criterio *di* unione dall’elenco a discesa. Fate clic **[!UICONTROL Save]** per creare il segmento.

![](../images/user-guide/merge_policy.png)

## Passaggi successivi

Seguendo questa esercitazione, con Segment Builder (Generatore di segmenti) è stato possibile trovare le audience in base ai loro punteggi di tendenza. Ora potete eseguire il targeting delle audience attivandole nelle destinazioni. Per ulteriori informazioni, consulta [la panoramica](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) delle destinazioni.