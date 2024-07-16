---
title: Panoramica dell’estensione Adobe Audience Manager
description: Scopri l’estensione tag Adobe Audience Manager in Adobe Experience Platform.
exl-id: d345e145-fdb9-4ca3-88c2-9c2a247ea59a
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 96%

---

# Panoramica dell’estensione Adobe Audience Manager

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Con l’estensione tag Audience Manager, puoi integrare il codice DIL utilizzato da Audience Manager con le proprietà in Adobe Experience Platform.

Utilizza questo riferimento per informazioni sulle opzioni disponibili quando utilizzi questa estensione per creare una regola.

>[!NOTE]
>
>Questa estensione non è destinata all’inoltro di eventi dei dati di Adobe Analytics. Per l’inoltro di eventi, utilizza l’[estensione Adobe Analytics](../analytics/overview.md).

## Configura l&#39;estensione Adobe Audience Manager

Se l’estensione Adobe Audience Manager non è ancora stata installata, apri la proprietà, quindi fai clic su **[!UICONTROL Estensioni > Catalogo]**, passa il puntatore sull’estensione Adobe Audience Manager e fai clic su **[!UICONTROL Installa]**.

Per configurare l’estensione, apri la scheda [!UICONTROL Estensioni], passa il puntatore sull’estensione e fai clic su **[!UICONTROL Configura]**.

### Impostazioni DIL

Configura le impostazioni DIL. Sono disponibili le seguenti configurazioni:

![](../../../images/ext-aam-config.png)

#### Versione DIL

Mostra la versione Data Integration Library (DIL).

Non è possibile modificare questa impostazione.

#### Escludi percorsi specifici

Se l&#39;URL corrisponde a qualsiasi percorso escluso, l&#39;estensione non viene caricata.

Fai clic su **[!UICONTROL Aggiungi percorso]** per specificare un URL escluso.

Abilita Regex se l&#39;URL è un&#39;espressione regolare.

#### Utilizza DIL Site Catalyst Module

Il [modulo SiteCatalyst](https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_dil_sc_init.html) funziona con DIL per inviare gli elementi tag Analytics ad Audience Manager.

Utilizza il Code Editor per configurare il file siteCatalyst.init.

Puoi anche creare una nota contenente informazioni su questa configurazione.

#### Utilizza DIL Google Analytics Module

Attiva il modulo [Google Analytics](https://experiencecloud.adobe.com/resources/help/it_IT/aam/dil-google-universal-analytics.html).

#### Proprietà inizializzazione DIL.create

Aggiungi le proprietà di inizializzazione utilizzate da [DIL.create](https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_dil_create.html) e la sottoproprietà spazio nomi per [l&#39;oggetto visitorService](https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_dil_visitor_service.html). Nei commenti al codice, vale a dire nel Code Editor, sono inclusi due casi d&#39;uso di esempio.

Seleziona **[!UICONTROL Scegli un elemento]** per aggiungere altre proprietà.

Passa il puntatore sull&#39;icona &quot;i&quot; per ottenere informazioni sul funzionamento di ciascuna proprietà. Per ulteriori informazioni sulle proprietà consulta la [documentazione Audience Manager DIL](https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_dil_create.html).

Al termine della configurazione dell’estensione, fai clic su **[!UICONTROL Salva]**.

## Tipi di azioni di estensione di Adobe Audience Manager

In questo argomento sono descritti i tipi di azione disponibili nell&#39;estensione Audience Manager.

L&#39;estensione Adobe Audience Manager fornisce le seguenti azioni nella sezione Then di una regola:

### Esegui codice personalizzato

Esegui il codice personalizzato configurato nel Code Editor.

Immetti il codice desiderato nel Code Editor, quindi fornisci un nome per il codice. Questo codice diventerà disponibile nella sezione Then del generatore di regole.

![](../../../images/ext-aam-then.png)

Puoi anche aggiungere una nota con informazioni sulla configurazione.
