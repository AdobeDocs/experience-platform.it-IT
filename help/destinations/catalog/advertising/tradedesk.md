---
keywords: pubblicità; ufficio commerciale; ufficio commerciale di pubblicità
title: La connessione a Trade Desk
description: Trade Desk è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 3%

---

# Connessione [!DNL The Trade Desk]

## Panoramica {#overview}


>[!IMPORTANT]
>
> A seguito dell&#39;[aggiornamento interno](../../../release-notes/2025/july-2025.md#destinations) al servizio Destinazioni a partire da luglio 2025, potrebbe verificarsi un calo di **profili attivati** nei flussi di dati a [!DNL The Trade Desk].
> &#x200B;> Questo calo è causato dall&#39;introduzione del **requisito di mappatura ECID** per tutte le attivazioni su questa piattaforma di destinazione. Per informazioni dettagliate, consulta la sezione [mappatura obbligatoria](#mandatory-mappings) in questa pagina.
>
>**Modifica:**
>
>* Il mapping ECID (Experience Cloud ID) è ora **obbligatorio** per tutte le attivazioni di profilo.
>* I profili senza mappatura ECID verranno **eliminati** dai flussi di dati di attivazione esistenti.
>
>**Operazioni da eseguire:**
>
>* Esamina i dati del pubblico per verificare che i profili abbiano valori ECID validi.
>* Monitora le metriche di attivazione per verificare i conteggi dei profili previsti.


Utilizzare questo connettore di destinazione per inviare i dati del profilo a [!DNL The Trade Desk]. Questo connettore invia dati all&#39;endpoint di prime parti [!DNL The Trade Desk]. L&#39;integrazione tra Adobe Experience Platform e [!DNL The Trade Desk] non supporta l&#39;esportazione dei dati nell&#39;endpoint di terze parti [!DNL The Trade Desk].

[!DNL The Trade Desk] è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile.

Per inviare i dati del profilo a [!DNL The Trade Desk], è necessario prima connettersi alla destinazione, come descritto nelle sezioni seguenti di questa pagina.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, desidero poter utilizzare tipi di pubblico creati da [!DNL Trade Desk IDs] o ID dispositivo per creare campagne digitali di retargeting o mirate al pubblico.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l&#39;attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Di seguito sono riportate le identità supportate dalla destinazione [!DNL The Trade Desk]. Queste identità possono essere utilizzate per attivare i tipi di pubblico in [!DNL The Trade Desk].

Tutte le identità nella tabella seguente sono mappature obbligatorie.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Questa identità è obbligatoria per il corretto funzionamento dell’integrazione, ma non viene utilizzata per l’attivazione del pubblico. |
| ID Trade Desk | ID inserzionista nella piattaforma [!DNL The Trade Desk] | Utilizza questa identità durante l’attivazione di tipi di pubblico in base all’ID proprietario del Trade Desk. |

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

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL The Trade Desk] e non hai abilitato in passato la funzionalità di sincronizzazione [ID](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync) nel servizio Experience Cloud ID (con Adobe Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato [!DNL The Trade Desk] integrazioni in Audience Manager, le sincronizzazioni ID configurate vengono trasferite ad Experience Platform.

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

### Mappature obbligatorie {#mandatory-mappings}

Tutte le identità di destinazione descritte nella sezione [identità supportate](#supported-identities) devono essere mappate nel passaggio di mappatura del flusso di lavoro di attivazione del pubblico. Ciò include:

* [!DNL GAID] (Google Advertising ID)
* [!DNL IDFA] (Apple ID per inserzionisti)
* [!DNL ECID] (Experience Cloud ID)
* [!DNL The Trade Desk ID]

![Schermata che mostra le mappature obbligatorie](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

La mappatura di tutte le identità di destinazione garantisce che l’attivazione possa essere suddivisa correttamente e fornire profili utilizzando qualsiasi identità presente. Ciò non significa che tutte le identità debbano essere presenti su ciascun profilo.

Affinché l&#39;esportazione nel Trade Desk abbia esito positivo, un profilo deve contenere:

* [!DNL ECID] e
* almeno uno tra: [!DNL GAID], [!DNL IDFA] o [!DNL The Trade Desk ID]

Esempi:

* Solo [!DNL ECID]: non esportato
* [!DNL ECID] + [!DNL The Trade Desk ID]: esportato
* [!DNL ECID] + [!DNL IDFA]: esportato
* [!DNL ECID] + [!DNL GAID]: esportato
* [!DNL IDFA] + [!DNL The Trade Desk ID] (nessun [!DNL ECID]): non esportato

>[!NOTE]
> 
>In seguito all&#39;aggiornamento [luglio 2025](/help/release-notes/2025/july-2025.md#destinations) al servizio delle destinazioni, viene applicato il mapping [!DNL ECID]. I profili mancanti per [!DNL ECID] vengono ora eliminati come previsto, il che potrebbe far emergere conteggi di attivazione più bassi rispetto al comportamento legacy.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL The Trade Desk], controllare l&#39;account [!DNL The Trade Desk]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.
