---
keywords: pubblicità; ufficio commerciale; ufficio commerciale di pubblicità
title: La connessione a Trade Desk
description: Trade Desk è una piattaforma self-service per consentire agli acquirenti di annunci di eseguire campagne digitali di retargeting e targeting del pubblico tra sorgenti di visualizzazione, video e inventario mobile.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 0954b5f22d609b0b12352de70f6c618cc88757c8
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 5%

---

# Connessione [!DNL The Trade Desk]

## Panoramica {#overview}

>[!IMPORTANT]
>
>* A partire dal venerdì 31 luglio 2025 nel catalogo delle destinazioni, puoi visualizzare due schede **[!DNL The Trade Desk]** affiancate. Questo è dovuto a un aggiornamento interno del servizio destinazioni. Il connettore di destinazione **[!DNL The Trade Desk]** esistente è stato rinominato in **[!UICONTROL (Obsoleto) The Trade Desk]** e una nuova scheda con il nome **[!UICONTROL The Trade Desk]** è ora disponibile.
>* Utilizza la nuova connessione **[!UICONTROL Trade Desk]** nel catalogo per i nuovi flussi di dati di attivazione. Se sono presenti flussi di dati attivi per la destinazione **[!UICONTROL (obsoleto) The Trade Desk]**, verranno aggiornati automaticamente, pertanto non è richiesta alcuna azione da parte dell&#39;utente.
>* Se si creano flussi di dati tramite l&#39;[API del servizio Flow](https://developer.adobe.com/experience-platform-apis/references/destinations/), è necessario aggiornare [!DNL flow spec ID] e [!DNL connection spec ID] ai valori seguenti:
>   * Flow spec ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`
>   * Connection spec ID: `1029798b-a97f-4c21-81b2-e0301471166e`

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
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico nella destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL The Trade Desk] e non hai abilitato in passato la funzionalità di sincronizzazione [ID](https://experienceleague.adobe.com/it/docs/id-service/using/id-service-api/methods/idsync) nel servizio Experience Cloud ID (con Adobe Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato [!DNL The Trade Desk] integrazioni in Audience Manager, le sincronizzazioni ID configurate vengono trasferite ad Experience Platform.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: [!DNL The Trade Desk] [!UICONTROL ID account].
* **[!UICONTROL Posizione server]**: chiedere al rappresentante [!DNL The Trade Desk] quale server regionale utilizzare. Di seguito sono riportati i server regionali disponibili tra cui è possibile scegliere:

   * **[!UICONTROL APAC]**
   * **[!UICONTROL Cina]**
   * **[!UICONTROL Tokyo]**
   * **[!UICONTROL Regno Unito/UE]**
   * **[!UICONTROL Costa orientale USA]**
   * **[!UICONTROL Costa occidentale USA]**

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

Nel passaggio [Pianificazione pubblico](../../ui/activate-segment-streaming-destinations.md#scheduling), devi mappare manualmente i tipi di pubblico al loro ID o nome descrittivo corrispondente nella piattaforma di destinazione.

Quando esegui la mappatura dei tipi di pubblico, Adobe consiglia di utilizzare il nome del pubblico di Experience Platform, o una forma più breve, per facilitarne l’utilizzo. Tuttavia, l’ID o il nome del pubblico nella destinazione non deve necessariamente corrispondere a quello nel tuo account Experience Platform. Qualsiasi valore inserito nel campo di mappatura verrà riflesso dalla destinazione.

### Mappature obbligatorie {#mandatory-mappings}

Tutte le identità di destinazione descritte nella sezione [identità supportate](#supported-identities) sono obbligatorie e devono essere mappate durante il processo di attivazione del pubblico. Ciò include:

* **GAID** (Google Advertising ID)
* **IDFA** (ID Apple per inserzionisti)
* **ECID** (Experience Cloud ID)
* **ID Trade Desk**

Il mancato mapping di tutte le identità richieste impedirà l&#39;attivazione corretta del pubblico su [!DNL The Trade Desk]. Ogni identità ha uno scopo specifico nell’integrazione e tutte sono necessarie affinché la destinazione funzioni correttamente.

![Schermata che mostra le mappature obbligatorie](../../assets/catalog/advertising/tradedesk/mandatory-mappings.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL The Trade Desk], controllare l&#39;account [!DNL The Trade Desk]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.
