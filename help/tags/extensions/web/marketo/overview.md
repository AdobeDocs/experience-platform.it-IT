---
title: Estensione Marketo Munchkin Panoramica
description: Scopri l’estensione tag Marketo Munchkin in Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 88%

---

# Panoramica dell’estensione Marketo Munchkin

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Utilizza l&#39;estensione per integrare il codice di tracciamento [!DNL Marketo Munchkin] JavaScript con la tua proprietà. [!DNL Marketo Munchkin] JavaScript consente di tracciare le visite degli utenti finali e di navigare sulle pagine di destinazione e sulle pagine web esterne Marketo.

## Installazione dell&#39;estensione Marketo Munchkin

Se l’estensione [!DNL Marketo Munchkin] non è ancora installata, apri la proprietà, quindi seleziona **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore sull’estensione [!DNL Marketo Munchkin] e fai clic su **[!UICONTROL Installa]**.

Non ci sono configurazioni necessarie per questa estensione.

## Tipi di azioni dell&#39;estensione Marketo Munchkin

In questa sezione sono descritti i tipi di azioni disponibili nell&#39;estensione [!DNL Marketo Munchkin].

### Inizializza

![](../../../images/munchkin-Init.png)

**Munchkin ID: (obbligatorio)** l&#39;ID account Munchkin trovato nel menu Amministrazione > Integrazione > Munchkin.

**Configurations:** tutti i parametri configurabili sono indicati [qui](https://developers.marketo.com/javascript-api/lead-tracking/configuration/).

### Visita pagina web

![](../../../images/munchkin-visit-page.png)

**url: (obbligatorio)** il percorso file URL utilizzato per registrare una visita di pagina.

**params:** una stringa di query dei parametri desiderati da registrare.

**name:** il nome personalizzato della risorsa della pagina Web.

### Fai clic sul collegamento

![](../../../images/munchkin-click-link.png)

**href: (obbligatorio)** Percorso del file URL utilizzato per registrare la selezione di un collegamento.
