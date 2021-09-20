---
title: Destinazione Marketo Engage
description: Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1f18e07af7ef0d90f882fa668c5659330bce5960
workflow-type: tm+mt
source-wordcount: '307'
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

## Impostare la destinazione e attivare i segmenti {#set-up}

Per istruzioni dettagliate su come impostare la destinazione e attivare i segmenti, leggi [Push an Adobe Experience Platform Segment to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) nella documentazione di Marketo.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->