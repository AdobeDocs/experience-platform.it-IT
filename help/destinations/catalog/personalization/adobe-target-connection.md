---
keywords: personalizzazione mirata; destinazione; destinazione target experience platform;destinazione adobe target;
title: Connessione Adobe Target (Beta)
description: Adobe Target è un’applicazione che fornisce personalizzazione e sperimentazione in tempo reale, 1:1 e basate sull’intelligenza artificiale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---


# Connessione Adobe Target (Beta) {#adobe-target-connection}

## Panoramica {#overview}

>[!IMPORTANT]
>
>La connessione Adobe Target in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Adobe Target è un’applicazione che fornisce personalizzazione e sperimentazione in tempo reale, 1:1 , basate sull’intelligenza artificiale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.

Adobe Target è una connessione di personalizzazione in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Questa integrazione è basata su [Adobe Experience Platform Web SDK](../../../edge/home.md). Devi usare questo SDK per usare questa destinazione.

## Tipo di esportazione {#export-type}

**Richiesta profilo** : richiedi tutti i segmenti mappati nella destinazione Adobe Target per un singolo profilo.

## Casi di utilizzo {#use-cases}

**Personalizzazione di un banner della home page**

Una società di noleggio e vendita di casa vuole personalizzare la propria home page con un banner, in base alle qualifiche del segmento di clienti in Adobe Experience Platform. L’azienda può selezionare i tipi di pubblico che devono ottenere un’esperienza personalizzata e inviarli ad Adobe Target come criteri di targeting per la loro offerta Target.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Experience Platform si connette automaticamente all’istanza Adobe Target della tua azienda. Non è richiesta alcuna autenticazione.

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **Nome**: Compila il nome preferito per questa destinazione.
* **Descrizione**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
* **ID** Datastream: Questo determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. Per ulteriori informazioni, consulta [Configurazione di un datastream](../../../edge/fundamentals/datastreams.md) .

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, leggi [Attivare profili e segmenti nelle destinazioni di richiesta del profilo](../../ui/activate-profile-request-destinations.md) .

## Dati esportati {#exported-data}

Adobe Target legge i dati del profilo da Adobe Experience Platform Edge Network, quindi non vengono esportati dati.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
