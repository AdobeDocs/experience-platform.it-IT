---
keywords: 'pubblicità; bing; '
title: Connessione Microsoft Bing
description: Con la destinazione di connessione Microsoft Bing, è possibile eseguire il retargeting e campagne digitali mirate al pubblico in Microsoft Display Advertising.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] connection {#bing-destination}

## Panoramica {#overview}

La destinazione [!DNL Microsoft Bing] ti aiuta a inviare i dati del profilo a [!DNL Microsoft Display Advertising].

Per inviare i dati del profilo a [!DNL Microsoft Bing], è necessario prima connettersi alla destinazione.

## Casi di utilizzo {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Microsoft Advertising IDs] per indirizzare gli utenti tramite pubblicità display tra [!DNL Microsoft Advertising] canali.

## Identità supportate {#supported-identities}

[!DNL Microsoft Bing] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| MAID | ID pubblicità Microsoft |

## Tipo di esportazione {#export-type}

**[!DNL Segment Export]** - stai esportando tutti i membri di un segmento (pubblico) nella  [!DNL Microsoft Bing] destinazione.

## Prerequisiti {#prerequisites}

Se stai cercando di creare la tua prima destinazione con [!DNL Microsoft Bing] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza avevi impostato le integrazioni [!DNL Microsoft Bing] in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

Durante la configurazione della destinazione, devi fornire le seguenti informazioni:

* [!UICONTROL ID] account: questo è il  [!DNL Bing Ads CID], in formato intero.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: Il tuo  [!DNL Bing Ads CID].

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico nelle destinazioni, consulta [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md) .

Nel passaggio [Pianificazione segmento](../../ui/activate-destinations.md#segment-schedule) , devi mappare manualmente i segmenti sul loro ID o nome descrittivo corrispondente nella destinazione.

Durante la mappatura dei segmenti, è consigliabile utilizzare il nome del segmento [!DNL Platform] o una sua forma più breve, per facilitarne l’utilizzo. Tuttavia, l&#39;ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nel tuo account [!DNL Platform] . Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Microsoft Bing], controlla il tuo account [!DNL Microsoft Bing Ads]. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
