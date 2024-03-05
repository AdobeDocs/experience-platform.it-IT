---
title: Installare Web SDK utilizzando l’estensione tag
description: Fai riferimento alla libreria SDK web utilizzando Raccolta dati di Adobe Experience Cloud.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Installare Web SDK utilizzando l’estensione tag

Adobe offre un’estensione tag dedicata per implementare e configurare l’SDK per web. Questo metodo di implementazione è il metodo principale consigliato dall’Adobe per distribuire e gestire il codice di raccolta dati.

Dopo aver incontrato il [prerequisiti](overview.md), è possibile distribuire l’estensione tag Web SDK seguendo la procedura riportata di seguito:

## Installare l’estensione all’interno di un tag

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata o creane una.
1. Accedi a **[!UICONTROL Estensioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda.
1. Individuare e installare **[!UICONTROL Adobe Experience Platform Web SDK]** estensione.
1. Seleziona la sandbox e lo stream di dati appropriati per ogni ambiente, quindi fai clic su **[!UICONTROL Salva]**.

## Pubblicare il codice tag in Sviluppo

L’estensione Web SDK è ora installata per questo tag. Ora puoi pubblicare il codice tag da utilizzare in un ambiente di sviluppo.

1. Accedi a **[!UICONTROL Flusso di pubblicazione]**, quindi seleziona **[!UICONTROL Aggiungi libreria]**.
1. Assegna alla libreria il nome desiderato, ad esempio &quot;Aggiungi libreria SDK Web&quot;. Imposta il [!UICONTROL Ambiente] menu a discesa &quot;Development&quot;.
1. Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi fai clic su **[!UICONTROL Salva e genera in sviluppo]**.

## Installare il codice del caricatore sul sito

Ora che il codice tag è pubblicato, puoi aggiungere il codice del caricatore tag al tuo sito web.

1. Accedi a **[!UICONTROL Ambienti]**, quindi fai clic sull’icona Riquadro accanto a &quot;Sviluppo&quot; per aprire una finestra modale contenente le istruzioni di installazione per questo ambiente.
1. Copia il codice di incorporamento e incollalo nella `<head>` del sito web.

## Compila la tua implementazione e pubblica in produzione

Consulta la [Panoramica dell’estensione Web SDK](../../tags/extensions/client/web-sdk/overview.md) per ulteriori informazioni sull’estensione stessa, e [Panoramica sui tag](../../tags/home.md) per ulteriori informazioni sulla navigazione nell’interfaccia dei tag.
