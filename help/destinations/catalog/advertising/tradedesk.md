---
keywords: pubblicità; il banco commerciale; ufficio commerciale pubblicitario
title: Il collegamento del Trade Desk
description: Il Trade Desk è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le varie fonti di visualizzazione, video e inventario mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# [!DNL The Trade Desk] connection

## Panoramica {#overview}

[!DNL The Trade Desk] La destinazione ti consente di inviare i dati del profilo a  [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per gli acquirenti di annunci che esegue il retargeting e campagne digitali mirate per il pubblico tra le sorgenti di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL Trade Desk], è necessario prima connettersi alla destinazione.

## Casi di utilizzo {#use-cases}

In qualità di addetto al marketing, voglio essere in grado di utilizzare segmenti generati da [!DNL Trade Desk IDs] o ID dispositivo per creare campagne di retargeting o campagne digitali mirate al pubblico.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| ID ufficio commerciale | ID inserzionista nella piattaforma Trade Desk |

## Tipo di esportazione {#export-type}

**[!DNL Segment export]** - stai esportando tutti i membri di un segmento (pubblico) nella destinazione.

## Prerequisiti {#prerequisites}

Se stai cercando di creare la tua prima destinazione con [!DNL The Trade Desk] e non hai abilitato in passato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID di Experience Cloud (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare le sincronizzazioni degli ID. Se in precedenza avevi impostato le integrazioni [!DNL The Trade Desk] in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: Il tuo ID  [!DNL Trade Desk] [!UICONTROL account].
* **[!UICONTROL Percorso]** server: Chiedi al tuo  [!DNL Trade Desk] rappresentante quale server regionale utilizzare. Questi sono i server regionali disponibili tra cui è possibile scegliere:
   * **[!UICONTROL Europa]**
   * **[!UICONTROL Singapore]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL America del Nord Est]**
   * **[!UICONTROL America del Nord occidentale]**
   * **[!UICONTROL America Latina]**

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

Nel passaggio [Pianificazione segmento](../../ui/activate-segment-streaming-destinations.md#scheduling) , devi mappare manualmente i segmenti sul loro ID o nome descrittivo corrispondente nella piattaforma di destinazione.

Durante la mappatura dei segmenti, ti consigliamo di utilizzare il nome del segmento di Platform o una sua forma più breve, per facilitarne l’utilizzo. Tuttavia, l’ID o il nome del segmento nella destinazione non deve necessariamente corrispondere a quello nell’account Platform. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

Se utilizzi più mappature dispositivo (ID cookie, [!DNL IDFA], [!DNL GAID]), assicurati di utilizzare lo stesso valore di mappatura per tutte e tre le mappature. [!DNL The Trade Desk] li aggrega in un singolo segmento, con una suddivisione a livello di dispositivo.

![ID mappatura segmento](../../assets/common/segment-mapping-id.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL The Trade Desk] , controlla il tuo account [!DNL Trade Desk] . Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.
