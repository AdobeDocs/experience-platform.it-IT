---
title: Connessione Snap Inc
description: Scopri come connettersi alla piattaforma Snapchat Ads ed esportare i tipi di pubblico da Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 2%

---

# Connessione Snap Inc

## Panoramica {#overview}

[Gli annunci Snapchat](https://forbusiness.snapchat.com/) sono realizzati per ogni azienda, indipendentemente dalle dimensioni o dal settore. Partecipa alle conversazioni quotidiane di Snapchatters con annunci digitali a schermo intero che ispirano l&#39;azione delle persone più importanti per la tua attività.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *Snap Inc*. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo *dev-support@snap.com*

## Casi d’uso {#use-cases}

Questa destinazione consente agli addetti al marketing di importare in Snapchat Ads i tipi di pubblico per utenti creati in Experience Platform e di utilizzarli per indirizzare i propri annunci.

## Prerequisiti {#prerequisites}

Per utilizzare questa destinazione, è necessario disporre di un account Snapchat Ads. Fai riferimento a questa documentazione per informazioni su come crearne una:

[Introduzione a Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitazioni {#limitations}

* Snap Inc non supporta più identità per un determinato segmento di pubblico. Esegui il mapping di una sola identità durante l’attivazione di un segmento.
* Snap Inc non supporta la ridenominazione dei segmenti. Per rinominare un segmento, è necessario disattivarlo, rinominarlo e quindi attivarlo.
* Non è possibile definire un periodo di conservazione per i membri di un segmento di pubblico. Tutti i membri sono mantenuti per tutta la vita e rimarranno nel pubblico fino a quando non verranno rimossi.

## Identità supportate {#supported-identities}

La destinazione *Snap Inc* supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Tutti gli identificatori inviati alla destinazione *Snap Inc* devono avere un hash in formato SHA-256. Per eseguire l&#39;hashing degli identificatori di testo normale prima di inviarli alla destinazione, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** durante la mappatura degli identificatori di destinazione per la destinazione.

>[!WARNING]
> 
> Gli identificatori senza hash non verranno accettati dalla destinazione Snap Inc e l&#39;invio potrebbe causare errori.


>[!IMPORTANT]
> 
> La destinazione Snap Inc non supporta più identità. Seleziona una sola identità.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| Indirizzo e-mail | Indirizzo e-mail con hash SHA-256 | Mappa gli indirizzi e-mail nel campo identità di destinazione *emailAddress*. |
| Numero di telefono | Numero di telefono con hash SHA-256 | Mappa gli indirizzi e-mail nel campo identità di destinazione *phoneNumber*. |
| GAID | ID Advertising Google con hash SHA-256 | Mappa gli ID Google Advertising nel campo identità di destinazione *gaid*. |
| IDFA | ID Advertising di Apple con hash SHA-256 | Mappa gli ID Apple Advertising nel campo identità di destinazione *idfa*. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione *YOURDESTINATION*. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connessione a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, effettua le seguenti operazioni:

1. Trova la destinazione *Snap Inc* dal catalogo di destinazione di Adobe Experience Platform e seleziona **Configura**.
2. Selezionare **[!UICONTROL Connetti alla destinazione]**. Verrai reindirizzato alla seguente schermata:
   ![Schermata di autenticazione 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Immetti le credenziali di Snapchat e seleziona **Accedi**.
4. Verranno visualizzati i dati di Snapchat a cui Adobe Experience Platform potrà accedere. Selezionare **Continua** per continuare il processo di connessione.

![Schermata di autenticazione 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Dopo aver selezionato Continua, attendi di essere reindirizzato a Adobe Experience Platform.

### Inserire i dettagli della destinazione {#destination-details}

![Dettagli destinazione](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Per configurare i dettagli per la destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: l&#39;ID account dell&#39;annuncio associato all&#39;account dell&#39;annuncio in cui si desidera importare i tipi di pubblico. Per ulteriori informazioni su come trovare questo elemento, fare riferimento a [questa documentazione nel Centro assistenza commerciale Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>Se si immette un ID account Snapchat Ad errato o non valido, l’attivazione del pubblico non riuscirà. Verifica di aver inserito l&#39;ID dell&#39;account dell&#39;annuncio corretto.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Dopo aver attivato i tipi di pubblico nella destinazione *Snap Inc*, potrai visualizzarli nella sezione [**Tipi di pubblico** di Snap Ads Manager](https://businesshelp.snapchat.com/s/article/audience-sharing). Per passare a questa sezione, effettua le seguenti operazioni:

1. Accedi a [Gestione annunci snap](https://ads.snapchat.com/)
2. Seleziona **Tipi di pubblico** dal menu a discesa nell&#39;angolo in alto a sinistra dello schermo. I tipi di pubblico attivati in Adobe Experience Platform sono visualizzati nella Libreria tipi di pubblico:

![Tipi di pubblico](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tieni presente che quando un pubblico di Adobi viene attivato per la prima volta in Snap Inc, inizialmente verrà visualizzato come un pubblico vuoto. Questo perché Adobe Experience Platform non esporta i dati dei membri in Snap Inc finché non valuta il pubblico. Per ulteriori informazioni sulla valutazione dei tipi di pubblico in Experience Platform, consulta la [Panoramica del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html#evaluate-segments).

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
