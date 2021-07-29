---
title: Estensioni
description: Scopri come funzionano le estensioni di tag in Adobe Experience Platform.
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 70%

---

# Estensioni

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Un&#39;estensione è un set di codice che estende le funzionalità fornite dai tag o dall&#39;inoltro di eventi.

L&#39;aggiunta di un&#39;estensione aggiunge nuovi elementi dati e nuove opzioni per la creazione di regole.

Le estensioni determinano gli elementi disponibili per la creazione di proprietà, regole e elementi di dati. Essi forniscono:

* Eventi, condizioni ed eccezioni
* Elementi dati
* Codice lato client

Utilizza i collegamenti nella parte superiore dell&#39;elenco Estensioni per visualizzare le estensioni installate, il catalogo delle estensioni o gli aggiornamenti.

Seleziona un’estensione, quindi fai clic su [!UICONTROL Configura] per visualizzarne e modificarne le impostazioni. Per ulteriori informazioni, consulta la sezione sull’ [aggiunta di una nuova estensione](#add-a-new-extension) per informazioni sulle opzioni di estensione.

>[!IMPORTANT]
>
>Le modifiche diventano effettive solo dopo la loro [pubblicazione](../../publishing/overview.md).

Per impostazione predefinita, Adobe fornisce estensioni che supportano integrazioni comuni. Le estensioni possono essere modificate con configurazioni personalizzate. Le configurazioni vengono fornite tramite le estensioni. Per creare una configurazione, fai clic sulla scheda dell’estensione, quindi seleziona **[!UICONTROL Aggiungi nuova configurazione]**.

## Catalogo delle estensioni

Utilizza il catalogo delle estensioni per sfogliare, configurare e distribuire tecnologie marketing e pubblicitarie create e gestite da fornitori software indipendenti, oltre che da estensioni per soluzioni di Adobe.

La pagina Estensioni offre tre visualizzazioni:

* Installate

   Mostra tutte le estensioni installate.

* Catalogo
* Mostra tutte le estensioni disponibili.
* Aggiornamenti

   Mostra aggiornamenti alle estensioni installate.

Fai clic su **[!UICONTROL Estensioni]** per visualizzare tutte le estensioni installate. Puoi inoltre utilizzare il catalogo per visualizzare un elenco di tutte le estensioni disponibili e per quali estensioni sono disponibili aggiornamenti.

Consulta [Riferimento estensioni](../../../extensions/web/overview.md) per informazioni dettagliate sulle estensioni di proprietà di Adobe.

## Aggiungi una nuova estensione {#add-a-new-extension}

I tag sono altamente estensibili. Le estensioni aggiungono funzionalità di base ai tag. Un uso comune delle estensioni consiste nel creare integrazioni con altre applicazioni.

1. Dalla pagina della panoramica di una proprietà, apri la scheda **[!UICONTROL Estensioni]**.
1. Selezionare un&#39;estensione.

   ![]()../../../images/extensions.png)

   * Se l&#39;estensione esiste, selezionala dal catalogo delle estensioni.
   * Passa il cursore sopra un&#39;estensione nell&#39;elenco per configurarla o disattivarla.
   * Se non sono presenti nell&#39;elenco, aggiungi altre estensioni dal catalogo.

   L&#39;estensione Core è il punto iniziale della nuova estensione. L&#39;estensione predefinita fornisce:

   * Evento predefinito
   * Condizioni ed eccezioni
   * Codice lato client predefinito

   Queste impostazioni predefinite sono alla base delle regole personalizzate che verranno create per creare l&#39;estensione.

Quando crei o modifichi elementi, puoi salvarli e generarli nella [libreria attiva](../../publishing/libraries.md#active-library). In questo modo la tua libreria viene salvata immediatamente e viene eseguita una build. Viene visualizzato lo stato della build. Puoi anche creare una nuova libreria dal menu a discesa Libreria attiva.

## Configurare un&#39;estensione

Passa il puntatore del mouse su un’estensione installata e seleziona **[!UICONTROL Configura]**.

>[!NOTE]
>
>Alcune estensioni non richiedono configurazione e non offrono opzioni di configurazione.

Ciascuna estensione configurabile dispone di opzioni univoche. Per informazioni sulle opzioni disponibili per ciascuna estensione Adobe, fai riferimento a [Estensioni Reference](../../../extensions/web/overview.md) .
