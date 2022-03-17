---
keywords: personalizzazione mirata; destinazione; destinazione target experience platform;destinazione adobe target;
title: Connessione Adobe Target
description: Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: c5d2427635d90f3a9551e2a395d01d664005e8bc
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 1%

---

# Connessione Adobe Target {#adobe-target-connection}

## Panoramica {#overview}

Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.

Adobe Target è una connessione di personalizzazione in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md). Devi usare questo SDK per usare questa destinazione.

>[!IMPORTANT]
>
>Prima di creare un [!DNL Adobe Target] connessione, leggere la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/configure-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi d’uso di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo tutti i segmenti mappati nella destinazione Adobe Target per un singolo profilo. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casi d’uso {#use-cases}

**Personalizzazione di un banner della home page**

Una società di noleggio e vendita di casa vuole personalizzare la propria home page con un banner, in base alle qualifiche del segmento di clienti in Adobe Experience Platform. L’azienda può selezionare i tipi di pubblico che devono ottenere un’esperienza personalizzata e inviarli ad Adobe Target come criteri di targeting per la loro offerta Target.

## Collegati alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informazioni sugli ID di datastream"
>abstract="Questa opzione determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. È necessario configurare un datastream prima di poter configurare la destinazione."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Scopri come configurare un datastream."

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Experience Platform si connette automaticamente all’istanza Adobe Target della tua azienda. Non è richiesta alcuna autenticazione.

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **Nome**: Compila il nome preferito per questa destinazione.
* **Descrizione**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
* **ID Datastream**: Questo determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. Vedi [Configurazione di un datastream](../../../edge/fundamentals/datastreams.md) per ulteriori dettagli.

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attivare profili e segmenti nelle destinazioni di richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Adobe Target legge i dati del profilo da Adobe Experience Platform Edge Network, quindi non vengono esportati dati.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
