---
keywords: pubblicità; il banco commerciale; ufficio commerciale pubblicitario
title: Il collegamento del Trade Desk
description: Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le varie fonti di visualizzazione, video e inventario mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# [!DNL The Trade Desk] connection

## Panoramica {#overview}

[!DNL The Trade Desk] La destinazione consente di inviare i dati del profilo a [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le sorgenti di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL Trade Desk], è innanzitutto necessario connettersi alla destinazione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Trade Desk IDs] o gli ID dispositivo per creare campagne digitali di retargeting o con targeting per il pubblico.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| ID ufficio commerciale | ID inserzionista nella piattaforma Trade Desk |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nella destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Se desideri creare la tua prima destinazione con [!DNL The Trade Desk] e non hanno attivato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se hai già configurato [!DNL The Trade Desk] integrazioni in Audience Manager, le sincronizzazioni ID impostate riportano su Platform.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: Le [!DNL Trade Desk] [!UICONTROL ID account].
* **[!UICONTROL Posizione server]**: Chiedi a [!DNL Trade Desk] rappresenta il server regionale da utilizzare. Questi sono i server regionali disponibili tra cui è possibile scegliere:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL America del Nord Est]**
   * **[!UICONTROL America del Nord occidentale]**
   * **[!UICONTROL America Latina]**

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

In [Pianificazione del segmento](../../ui/activate-segment-streaming-destinations.md#scheduling) al passaggio , devi mappare manualmente i segmenti sul loro ID o nome descrittivo corrispondente nella piattaforma di destinazione.

Durante la mappatura dei segmenti, ti consigliamo di utilizzare il nome del segmento di Platform o una sua forma più breve, per facilitarne l’utilizzo. Tuttavia, l’ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nell’account Platform. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

Se utilizzi più mappature dispositivo (ID cookie, [!DNL IDFA], [!DNL GAID]), assicurati di utilizzare lo stesso valore di mappatura per tutte e tre le mappature. [!DNL The Trade Desk] li aggrega in un singolo segmento, con una suddivisione a livello di dispositivo.

![ID mappatura segmento](../../assets/common/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL The Trade Desk] destinazione, controlla il tuo [!DNL Trade Desk] conto. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
