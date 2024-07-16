---
title: Installare Web SDK utilizzando l’estensione tag
description: Fai riferimento alla libreria SDK web utilizzando Raccolta dati di Adobe Experience Cloud.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Installare Web SDK utilizzando l’estensione tag

Adobe offre un’estensione tag dedicata per implementare e configurare l’SDK per web. Questo metodo di implementazione è il metodo principale consigliato dall’Adobe per distribuire e gestire il codice di raccolta dati.

Una volta soddisfatti i [prerequisiti](overview.md), puoi distribuire l&#39;estensione tag Web SDK seguendo la procedura seguente:

## Installare l’estensione all’interno di un tag

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata o creane una.
1. Passa a **[!UICONTROL Estensioni]**, quindi seleziona la scheda **[!UICONTROL Catalogo]**.
1. Individua e installa l&#39;estensione **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Seleziona la sandbox e lo stream di dati appropriati per ogni ambiente, quindi fai clic su **[!UICONTROL Salva]**.

Per ulteriori informazioni, consulta la documentazione su come [configurare l&#39;estensione tag Web SDK](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

## Publish il codice tag per lo sviluppo

L’estensione Web SDK è ora installata per questo tag. Ora puoi pubblicare il codice tag da utilizzare in un ambiente di sviluppo.

1. Passa a **[!UICONTROL Flusso di pubblicazione]**, quindi seleziona **[!UICONTROL Aggiungi libreria]**.
1. Assegna alla libreria il nome desiderato, ad esempio &quot;Aggiungi libreria SDK Web&quot;. Impostare il menu a discesa [!UICONTROL Ambiente] su &quot;Sviluppo&quot;.
1. Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**, quindi fai clic su **[!UICONTROL Salva e genera in sviluppo]**.

## Installare il codice del caricatore sul sito

Ora che il codice tag è pubblicato, puoi aggiungere il codice del caricatore tag al tuo sito web.

1. Passa a **[!UICONTROL Ambienti]**, quindi fai clic sull&#39;icona della casella accanto a &quot;Sviluppo&quot; per aprire una finestra modale contenente le istruzioni di installazione per questo ambiente.
1. Copiare il codice di incorporamento e incollarlo nel tag `<head>` del sito Web.

## Compila la tua implementazione e pubblica in produzione

Per ulteriori informazioni sull&#39;estensione, consulta [Panoramica dell&#39;estensione Web SDK](../../tags/extensions/client/web-sdk/overview.md) e [Panoramica tag](../../tags/home.md) per ulteriori informazioni sulla navigazione nell&#39;interfaccia dei tag.
