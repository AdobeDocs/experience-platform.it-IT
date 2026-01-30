---
keywords: pubblicità; bing;
title: Connessione Microsoft Bing
description: Con la destinazione di connessione di Microsoft Bing, puoi eseguire campagne digitali di retargeting e mirate al pubblico in tutta la rete Microsoft Advertising, inclusi display advertising, search e native.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: ec31c1d967be4764b22f735429e2f9437f31ed20
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 5%

---

# Connessione [!DNL Microsoft Bing] {#bing-destination}

## Panoramica {#overview}

Utilizzare la destinazione [!DNL Microsoft Bing] per inviare i dati del profilo all&#39;intero [!DNL Microsoft Advertising Network], inclusi [!DNL Display Advertising], [!DNL Search] e [!DNL Native].

La destinazione [!DNL Microsoft Bing] crea *[!DNL Custom Audiences]* in Microsoft. Questi sono disponibili sia in [!DNL Microsoft Search Network] che in [!DNL Audience Network] ([!DNL Native] /[!DNL Display] /[!DNL Programmatic]) come elencato nella [documentazione di Microsoft Advertising](https://help.ads.microsoft.com/#apex/ads/en/56892/1-500).

Per inviare i dati del profilo a [!DNL Microsoft Bing], è necessario prima connettersi alla destinazione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, desidero poter utilizzare i tipi di pubblico generati da [!DNL Microsoft Advertising IDs] per eseguire il targeting degli utenti tramite pubblicità di visualizzazione o ricerca tra [!DNL Microsoft Advertising] canali.

## Identità supportate {#supported-identities}

[!DNL Microsoft Bing] supporta l&#39;attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Tutte le identità nella tabella seguente sono preconfigurate e mappate automaticamente durante l&#39;attivazione. Non è necessario configurare manualmente queste mappature.

| Identità | Descrizione | Considerazioni |
|---|---|---|
| DOMESTICA | MICROSOFT ADVERTISING ID | Attivato quando nel profilo è presente un Advertising ID di Microsoft. |
| ECID | Experience Cloud ID | **Obbligatorio.** Tutti i profili devono avere un ECID con una mappatura corrispondente di Microsoft Advertising ID per essere esportati. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

**[!DNL Audience Export]** - esportazione di tutti i membri di un pubblico nella destinazione [!DNL Microsoft Bing].

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico nella destinazione [!DNL Microsoft Bing]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

La destinazione [!DNL Microsoft Bing] richiede la seguente configurazione per funzionare correttamente:

1. **Abilita funzionalità di sincronizzazione ID**: se questa è la prima volta che configuri l&#39;attivazione di [!DNL Microsoft Bing] e in passato non hai abilitato la [funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio Experience Cloud ID (con Adobe Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID.
   * Se in precedenza hai impostato [!DNL Microsoft Bing] integrazioni in Audience Manager, le sincronizzazioni ID esistenti vengono automaticamente trasferite ad Experience Platform.

2. **Verifica ECID nei profili**: tutti i profili devono avere un ECID presente per essere esportati correttamente. ECID **obbligatorio** per questa destinazione.

Durante la configurazione della destinazione, devi fornire le seguenti informazioni:

* [!UICONTROL Account ID]: [!DNL Bing Ads CID], in formato intero.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Inserire i dettagli della destinazione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Account ID]**: [!DNL Bing Ads Customer ID] (CID). Il tuo CID è un numero intero, trovato nell&#39;URL quando accedi a [!DNL Microsoft Advertising].

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID di mappatura"
>abstract="Immetti l’ID numerico del pubblico Bing su cui desideri mappare il segmento selezionato. Se il [!UICONTROL Mapping ID] fornito non corrisponde a un ID pubblico nella destinazione Bing, i dati del pubblico previsto non verranno visualizzati nel tuo account Bing."

>[!CONTEXTUALHELP]
>id="platform_destinations_required_mappings_bing"
>title="Set di mappatura predefiniti"
>abstract="Abbiamo preconfigurato questi due set di mappatura per te. Quando attivi i dati in Microsoft Bing, i profili idonei per i tipi di pubblico attivati devono avere almeno un’identità ECID associata al loro profilo, per poter essere esportati correttamente nella destinazione."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/catalog/advertising/bing#preconfigured-mappings" text="Ulteriori informazioni sulle mappature preconfigurate"

>[!IMPORTANT]
> 
>Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

Nel passaggio [Pianificazione pubblico](../../ui/activate-segment-streaming-destinations.md#scheduling), devi mappare manualmente il nome del pubblico nel campo [!UICONTROL Mapping ID]. In questo modo i metadati del pubblico verranno trasmessi correttamente a [!DNL Bing].

![Immagine dell&#39;interfaccia utente che mostra la schermata di pianificazione del pubblico con un esempio di come mappare il nome del pubblico all&#39;ID di mappatura Bing.](../../assets/catalog/advertising/bing/mapping-id.png)

### Mappature preconfigurate {#preconfigured-mappings}

Le seguenti mappature di identità sono **preconfigurate e popolate automaticamente** durante il flusso di lavoro di Audience Activation:

* **MAID** (Microsoft Advertising ID)
* **ECID** (Experience Cloud ID)

Queste mappature sono disattivate e di sola lettura. Non è necessario configurare nulla in questo passaggio. Selezionare **[!UICONTROL Next]** per continuare.

>[!IMPORTANT]
>
>**ECID è necessario per completare l&#39;esportazione.I profili** senza ECID o senza una mappatura di sincronizzazione ID tra ECID e Microsoft Advertising ID non verranno esportati.

### Esempi di attivazione

* **Il profilo con mappatura ECID e Microsoft Advertising ID:** è stato esportato e attivato correttamente
* **Profilo con solo ECID (nessuna mappatura Microsoft Advertising ID):** Il profilo è **non esportato**. È richiesta la mappatura della sincronizzazione ID tra ECID e MAID.
* **Profilo senza ECID:** Il profilo è **non esportato**. ECID è obbligatorio per questa destinazione.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Microsoft Bing], controllare l&#39;account [!DNL Microsoft Bing Ads]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.
