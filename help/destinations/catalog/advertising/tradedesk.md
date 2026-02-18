---
keywords: pubblicità; ufficio commerciale; ufficio commerciale di pubblicità
title: La connessione a Trade Desk
description: Trade Desk è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 138bfe721bb20fe3ba614a73ffffca3e00979acb
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 2%

---

# Connessione [!DNL The Trade Desk]

## Panoramica {#overview}

Utilizzare questo connettore di destinazione per inviare i dati del profilo a [!DNL The Trade Desk]. Questo connettore invia dati all&#39;endpoint di prime parti [!DNL The Trade Desk]. L&#39;integrazione tra Adobe Experience Platform e [!DNL The Trade Desk] non supporta l&#39;esportazione dei dati nell&#39;endpoint di terze parti [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL The Trade Desk], è necessario prima connettersi alla destinazione, come descritto nelle sezioni seguenti di questa pagina.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, desidero poter utilizzare tipi di pubblico creati da [!DNL Trade Desk IDs] o ID dispositivo per creare campagne digitali di retargeting o mirate al pubblico.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l&#39;attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Di seguito sono riportate le identità supportate dalla destinazione [!DNL The Trade Desk]. Queste identità possono essere utilizzate per attivare i tipi di pubblico in [!DNL The Trade Desk].

Tutte le identità nella tabella seguente sono preconfigurate e mappate automaticamente durante l&#39;attivazione. Non è necessario configurare manualmente queste mappature nel flusso di lavoro di attivazione.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Attivato quando nel profilo è presente un GAID. |
| IDFA | Apple ID per inserzionisti | Attivato quando nel profilo è presente un identificatore IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, leggere il seguente documento in [ECID](/help/identity-service/features/ecid.md). |
| [!DNL Tradedesk] | [!DNL TDID] nella piattaforma [!DNL The Trade Desk] | Attivato quando un profilo ha un ECID ed esiste una mappatura ID da ECID a Trade Desk in Experience Platform. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico nella destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

I prerequisiti dipendono dai tipi di identità che intendi utilizzare per l’attivazione del pubblico:

**Non sono presenti prerequisiti solo per l&#39;attivazione degli ID per dispositivi mobili**. Se raccogli e gestisci gli ID (GAID e/o IDFA) per i tuoi clienti, puoi iniziare ad attivare i tipi di pubblico in [!DNL The Trade Desk].

**Per il targeting basato su cookie su[!DNL The Trade Desk]**, assicurati che sia stata stabilita una mappatura tra ECID e [!DNL Trade Desk ID]. A tale scopo, completa i passaggi seguenti:

1. **Abilita funzionalità di sincronizzazione ID**: se questa è la prima volta che configuri l&#39;attivazione di [!DNL The Trade Desk ID] e in passato non hai abilitato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/it/docs/id-service/using/id-service-api/methods/idsync) nel servizio Experience Cloud ID (con Adobe Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID.
   * Se in precedenza hai configurato [!DNL The Trade Desk] integrazioni in Audience Manager, le sincronizzazioni ID esistenti vengono automaticamente trasferite ad Experience Platform.

2. **Crea strumenti per le pagine Web**: implementa il codice nelle pagine Web per creare mappature tra [!DNL The Trade Desk ID] e Adobe ECID. Questo consente ad Experience Platform di associare gli ID Trade Desk ai profili dei clienti.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: [!DNL The Trade Desk] [!UICONTROL Account ID].
* **[!UICONTROL Server Location]**: Chiedi al tuo rappresentante [!DNL The Trade Desk] quale server regionale utilizzare. Di seguito sono riportati i server regionali disponibili tra cui è possibile scegliere:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL China]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL UK/EU]**
   * **[!UICONTROL US East Coast]**
   * **[!UICONTROL US West Coast]**

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

Nel passaggio [Pianificazione pubblico](../../ui/activate-segment-streaming-destinations.md#scheduling), devi mappare manualmente i tipi di pubblico al loro ID o nome descrittivo corrispondente nella piattaforma di destinazione.

Quando esegui la mappatura dei tipi di pubblico, Adobe consiglia di utilizzare il nome del pubblico di Experience Platform, o una forma più breve, per facilitarne l’utilizzo. Tuttavia, l’ID o il nome del pubblico nella destinazione non deve necessariamente corrispondere a quello nel tuo account Experience Platform. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

### Mappature preconfigurate {#preconfigured-mappings}

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_ttd"
>title="Set di mappatura predefiniti"
>abstract="Abbiamo preconfigurato questi quattro set di mappatura per te. Quando attivi i dati su The Trade Desk, i profili qualificati per i tipi di pubblico attivati non devono necessariamente avere tutte e quattro le identità presenti sui profili, in quanto questa destinazione funziona con una qualsiasi delle identità di destinazione mostrate qui. <br> Per il targeting basato su cookie basato sull&#39;ID del Trade Desk, è necessario che ECID sia presente nel profilo e che sia presente una mappatura di sincronizzazione ID tra l&#39;ID del Trade Desk e ECID."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/destinations/catalog/advertising/tradedesk#preconfigured-mappings" text="Ulteriori informazioni sulle mappature preconfigurate"

Le seguenti mappature di identità sono **preconfigurate e compilate automaticamente** nel flusso di lavoro di Audience Activation:

* GAID (Google Advertising ID)
* IDFA (Apple ID per inserzionisti)
* ECID (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Schermata che mostra le mappature obbligatorie](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

Queste mappature sono disattivate e di sola lettura. Non è necessario configurare nulla in questo passaggio. Selezionare **[!UICONTROL Next]** per continuare.

Experience Platform controlla automaticamente ogni profilo che appartiene ai tipi di pubblico mappati nel flusso di lavoro di attivazione per tutti i tipi di identità supportati e quindi attiva il profilo utilizzando le identità presenti.

### Requisiti di identità per tipo di attivazione

**Attivazione ID mobile (GAID/IDFA):** I profili con solo GAID o IDFA sono sufficienti per l&#39;attivazione. Non sono necessari identità o prerequisiti aggiuntivi.

**Il targeting basato su cookie ([!DNL Trade Desk ID]):** richiede entrambi:

* ECID presente nel profilo
* Mapping di sincronizzazione ID tra [!DNL Trade Desk ID] e ECID (configurato come descritto nella sezione [prerequisiti](#prerequisites))

**Comportamento con più ID:** Se un profilo contiene più identità supportate, ogni identità verrà attivata separatamente in [!DNL The Trade Desk]. Questo assicura la massima portata e flessibilità nell’attivazione del pubblico.

### Esempi di attivazione

* **Profili ID mobili:** I profili con GAID e/o IDFA vengono attivati utilizzando i rispettivi ID pubblicitari. Se un profilo contiene sia GAID che IDFA, ogni ID verrà attivato separatamente.
* **Profilo basato su cookie:** Verrà attivato un profilo con ECID e una mappatura [!DNL Trade Desk ID] corrispondente utilizzando l&#39;ID Trade Desk per il targeting basato su cookie.
* **Profilo solo ECID:** Un profilo con solo ECID e nessuna mappatura [!DNL Trade Desk ID] non verrà **esportato**. ECID da solo non è sufficiente per l&#39;attivazione.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL The Trade Desk], controllare l&#39;account [!DNL The Trade Desk]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.
