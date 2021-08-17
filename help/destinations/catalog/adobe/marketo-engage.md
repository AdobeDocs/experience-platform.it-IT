---
title: Destinazione Marketo Engage
description: Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---


# Destinazione Marketo Engage (Beta) {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>La destinazione del Marketo Engage in Adobe Experience Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.

Il connettore dei segmenti consente agli addetti al marketing di inviare i segmenti creati in Adobe Experience Platform a Marketo dove verranno visualizzati come elenchi statici.

## Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione |
|---|---|
| ECID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/ecid.md) . |
| E-mail | Spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |

## Tipo di esportazione {#export-type}

Esportazione segmento : esporta tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione del Marketo Engage.

## Configurazione {#set-up}

Le istruzioni su come impostare la destinazione [sono disponibili qui](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .
