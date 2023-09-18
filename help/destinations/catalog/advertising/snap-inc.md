---
title: Connessione Snap Inc
description: Scopri come connettersi alla piattaforma Snapchat Ads ed esportare i tipi di pubblico da Experienci Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# Connessione Snap Inc

## Panoramica {#overview}

[Annunci Snapchat](https://forbusiness.snapchat.com/) sono realizzati per ogni azienda, indipendentemente dalle dimensioni o dal settore. Partecipa alle conversazioni quotidiane di Snapchatters con annunci digitali a schermo intero che ispirano l&#39;azione delle persone più importanti per la tua attività.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da *Snap Inc* team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *dev-support@snap.com*

## Casi d’uso {#use-cases}

Questa destinazione consente agli addetti al marketing di importare in Snapchat Ads i tipi di pubblico per utenti creati in Experienci Platform e di utilizzarli per indirizzare i propri annunci.

## Prerequisiti {#prerequisites}

Per utilizzare questa destinazione, è necessario disporre di un account Snapchat Ads. Fai riferimento a questa documentazione per informazioni su come crearne una:

[Guida introduttiva a Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitazioni  {#limitations}

* Snap Inc non supporta più identità per un determinato segmento di pubblico. Esegui il mapping di una sola identità durante l’attivazione di un segmento.
* Snap Inc non supporta la ridenominazione dei segmenti. Per rinominare un segmento, è necessario disattivarlo, rinominarlo e quindi attivarlo.
* Non è possibile definire un periodo di conservazione per i membri di un segmento di pubblico. Tutti i membri sono mantenuti per tutta la vita e rimarranno nel pubblico fino a quando non verranno rimossi.

## Identità supportate {#supported-identities}

Il *Snap Inc* la destinazione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

Tutti gli identificatori inviati al *Snap Inc* La destinazione deve avere un hash in formato SHA-256. Per aggiungere hash agli identificatori di testo normale prima di inviarli alla destinazione, seleziona la **[!UICONTROL Applica trasformazione]** quando si mappano gli identificatori di destinazione per la destinazione.

>[!WARNING]
> 
> Gli identificatori senza hash non verranno accettati dalla destinazione Snap Inc e l&#39;invio potrebbe causare errori.


>[!IMPORTANT]
> 
> La destinazione Snap Inc non supporta più identità. Seleziona una sola identità.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| Indirizzo e-mail | Indirizzo e-mail con hash SHA-256 | Mappare gli indirizzi e-mail nel campo identità di destinazione *emailAddress*. |
| Numero di telefono | Numero di telefono con hash SHA-256 | Mappare gli indirizzi e-mail nel campo identità di destinazione *phoneNumber*. |
| GAID | ID Google Advertising con hash SHA-256 | Mappare gli ID Google Advertising nel campo identità di destinazione *gaid*. |
| IDFA | ID pubblicità Apple con hash SHA-256 | Mappare gli ID Apple Advertising nel campo identità di destinazione *idfa*. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati in *DESTINAZIONE* destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connessione a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

### Autentica nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, effettua le seguenti operazioni:

1. Trova il *Snap Inc* dal catalogo di destinazione di Adobe Experience Platform e selezionare **Configurazione**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**. Verrai reindirizzato alla seguente schermata:
   ![Schermata di autenticazione 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Immetti le credenziali di Snapchat e seleziona **Accedi**.
4. Verranno visualizzati i dati di Snapchat a cui Adobe Experience Platform potrà accedere. Seleziona **Continua** per procedere con il processo di connessione.

![Schermata di autenticazione 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Dopo aver selezionato Continua, attendi di essere reindirizzato a Adobe Experience Platform.

### Inserisci i dettagli della destinazione {#destination-details}

![Dettagli della destinazione](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Per configurare i dettagli per la destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: l’ID dell’account dell’annuncio associato all’account dell’annuncio in cui importare i tipi di pubblico. Per ulteriori informazioni su come reperire questa risorsa, fare riferimento a [questa documentazione sul Centro assistenza di Snapchat Business](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Se si immette un ID account Snapchat Ad errato o non valido, l’attivazione del pubblico non riuscirà. Verifica di aver inserito l&#39;ID dell&#39;account dell&#39;annuncio corretto.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Dopo aver attivato i tipi di pubblico su *Snap Inc* destinazione, sarà possibile visualizzare i tipi di pubblico in Snap Ads Manager [**Tipi di pubblico** sezione](https://businesshelp.snapchat.com/s/article/audience-sharing). Per passare a questa sezione, effettua le seguenti operazioni:

1. Accedi a [Gestione annunci snap](https://ads.snapchat.com/)
2. Seleziona **Tipi di pubblico** dal menu a discesa nell’angolo superiore sinistro dello schermo. I tipi di pubblico attivati in Adobe Experience Platform sono visualizzati nella Libreria tipi di pubblico:

![Tipi di pubblico](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tieni presente che quando un pubblico di Adobi viene attivato per la prima volta in Snap Inc, inizialmente verrà visualizzato come un pubblico vuoto. Questo perché Adobe Experience Platform non esporta i dati dei membri in Snap Inc finché non valuta il pubblico. Per ulteriori informazioni sulla valutazione dei tipi di pubblico, consulta l’ Experience Platform [Panoramica del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).
