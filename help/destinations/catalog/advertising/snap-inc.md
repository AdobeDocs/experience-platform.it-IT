---
title: Connessione Snap Inc
description: Scopri come connettersi alla piattaforma Snapchat Ads ed esportare i segmenti di pubblico da Experience Platform.
exl-id: 1f0f2dc0-5f3d-424b-9b22-b1a14ac30039
source-git-commit: 988ecbed3084ef162453c9f1124998c6e9ae2e45
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Connessione Snap Inc

## Panoramica {#overview}

[Annunci Snapchat](https://forbusiness.snapchat.com/) sono fatti per ogni azienda, non importa le dimensioni o l&#39;industria. Diventa parte delle conversazioni quotidiane di Snapchatters con annunci digitali a schermo intero che ispirano l&#39;azione delle persone che contano di più per la tua azienda.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *Snap Inc* squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo *dev-support@snap.com*

## Casi d’uso {#use-cases}

Questa destinazione consente agli esperti di marketing di importare i segmenti di utenti creati in Experience Platform in Snapchat Ads e di utilizzarli per il targeting dei loro annunci.

## Prerequisiti {#prerequisites}

Per utilizzare questa destinazione, è necessario avere un account Snapchat Ads. Consulta questa documentazione per informazioni su come crearne una:

[Introduzione a Snapchat Advertising](https://businesshelp.snapchat.com/s/article/overview?language=en_US)

## Limitazioni  {#limitations}

* Snap Inc non supporta più identità per un dato segmento di pubblico. Mappa una sola identità quando attivi un segmento.
* Snap Inc non supporta la ridenominazione dei segmenti. Per rinominare un segmento, è necessario disattivarlo, rinominarlo e attivarlo.
* Non è possibile definire un periodo di conservazione per i membri di un segmento di pubblico. Tutti i membri hanno una durata di conservazione e saranno inclusi nel segmento fino alla loro rimozione.

## Identità supportate {#supported-identities}

La *Snap Inc* La destinazione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

Tutti gli identificatori inviati al *Snap Inc* la destinazione deve essere crittografata in formato SHA-256. Per aggiungere hash agli identificatori di testo normale prima di inviarli alla destinazione, controlla la **[!UICONTROL Applica trasformazione]** durante la mappatura degli identificatori target per la destinazione.

>[!WARNING]
> 
> Gli identificatori con hash non verranno accettati dalla destinazione Snap Inc e l&#39;invio di tali identificatori potrebbe causare errori.


>[!IMPORTANT]
> 
> La destinazione Snap Inc non supporta più identità. Selezionare una sola identità.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| Indirizzo e-mail | Indirizzo e-mail con hash SHA-256 | Mappare gli indirizzi e-mail nel campo identità di destinazione *emailAddress*. |
| Numero di telefono | Numero di telefono con hash SHA-256 | Mappare gli indirizzi e-mail nel campo identità di destinazione *phoneNumber*. |
| GAID | SHA-256 con hash Google Advertising ID | Mappatura degli ID pubblicitari di Google nel campo di identità di destinazione *dorato*. |
| IDFA | SHA-256 con hash Apple Advertising ID | Mappatura degli ID pubblicitari di Apple nel campo identità di destinazione *idfa*. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nel *DESTINAZIONE* destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connessione a Snap Inc {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, effettua le seguenti operazioni:

1. Trova il *Snap Inc* destinazione dal Catalogo di destinazione di Adobe Experience Platform e seleziona **Configurazione**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**. Verrai reindirizzato alla seguente schermata:
   ![Schermo di autenticazione 1](/help/destinations/assets/catalog/advertising/snapchat-ads/auth1.png)
3. Immetti le tue credenziali Snapchat e seleziona **Accesso**.
4. Ti verrà mostrato i dati Snapchat a cui Adobe Experience Platform sarà in grado di accedere. Seleziona **Continua** per procedere con il processo di connessione.

![Schermo di autenticazione 2](/help/destinations/assets/catalog/advertising/snapchat-ads/auth2.png)

Dopo aver selezionato Continua, attendi di essere reindirizzato a Adobe Experience Platform.

### Compila i dettagli della destinazione {#destination-details}

![Dettagli destinazione](/help/destinations/assets/catalog/advertising/snapchat-ads/destinationdetails.png)

Per configurare i dettagli della destinazione, compila i campi richiesti e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: L’ID account dell’annuncio associato all’account dell’annuncio in cui desideri importare i segmenti. Per ulteriori informazioni su come reperirlo, consulta [questa documentazione sul centro di assistenza aziendale Snapchat](https://businesshelp.snapchat.com/s/article/biz-acct-id?language=en_US).

>[!IMPORTANT]
> 
>L’inserimento di un ID account Snapchat Ad errato o non valido causerà un errore nell’attivazione dei segmenti. Verifica di aver inserito l&#39;ID account annuncio corretto.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Convalida esportazione dati {#exported-data}

Dopo aver attivato i segmenti nella *Snap Inc* destinazione, potrai vedere i segmenti nel Gestore di annunci Snap [**Tipi di pubblico** sezione](https://businesshelp.snapchat.com/s/article/audience-sharing). Per passare a questa sezione, segui questi passaggi:

1. Accedi al [Gestione annunci Snap](https://ads.snapchat.com/)
2. Seleziona **Tipi di pubblico** dal menu a discesa nell&#39;angolo superiore sinistro dello schermo. I segmenti attivati in Adobe Experience Platform verranno visualizzati nella Libreria tipi di pubblico:

![Tipi di pubblico](/help/destinations/assets/catalog/advertising/snapchat-ads/audiences.png)

Tieni presente che quando un segmento di Adobe viene attivato per la prima volta su Snap Inc, inizialmente lo vedrai come un pubblico vuoto. Questo perché Adobe Experience Platform non esporta i dati dei membri in Snap Inc finché non valuta il segmento. Per ulteriori informazioni sulla modalità di valutazione dei segmenti in Experience Platform, consulta la [Panoramica del servizio di segmentazione](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=en#evaluate-segments).

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
