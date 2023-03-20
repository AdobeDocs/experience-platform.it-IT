---
title: Connessione TikTok
description: Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le tue campagne pubblicitarie. Questi tipi di pubblico possono essere di persone che hanno visitato il tuo sito web o che hanno interagito con i tuoi contenuti. Invio rapido e sicuro del segmento desiderato da Adobe Experience Platform a TikTok tramite l’integrazione in tempo reale di Adobe con TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
source-git-commit: 7bfcd0132380f0c847742ff05c1f334542adfba2
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---


# Connessione TikTok

## Panoramica {#overview}

Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le tue campagne pubblicitarie. Questi tipi di pubblico possono essere di persone che hanno visitato il tuo sito web o che hanno interagito con i tuoi contenuti. Invio rapido e sicuro del segmento desiderato da Adobe Experience Platform a TikTok tramite l’integrazione in tempo reale di Adobe con TikTok Ads Manager. Visita [Centro assistenza aziendale TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) per ulteriori informazioni.

>[!IMPORTANT]
>
>Questa pagina di documentazione è stata creata dal team TikTok. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casi d’uso {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione TikTok, ecco un esempio di caso d’uso per i clienti Adobe Experience Platform.

### Caso d’uso {#use-case-1}

Un marchio di abbigliamento atletico vuole raggiungere i clienti esistenti attraverso i loro account social media. Il brand di abbigliamento può acquisire indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti a TikTok per visualizzare annunci nei feed social media dei propri clienti.

## Prerequisiti {#prerequisites}

Prima di inviare dati al tuo [!DNL TikTok Ads Manager] account, dovrai concedere l’autorizzazione Adobe Experience Platform per accedere al tuo account annuncio per `Audience Management`. Puoi fornire questa autorizzazione inserendo l’ID inserzionista nell’Experience Platform e seguendo il reindirizzamento per concedere l’autorizzazione. Puoi trovare ulteriori istruzioni nella sezione [Documentazione API di TikTok](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378).

## Identità supportate {#supported-identities}

TikTok supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |
| Numero di telefono | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform e devono essere in formato E.164. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| E-mail | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione TikTok. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, verrai reindirizzato al tuo [!DNL TikTok Ads Manager] e autorizza Adobe a gestire i tipi di pubblico per tuo conto.

![Selezione delle autorizzazioni di TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Immagine dell’interfaccia utente di TikTok per la selezione delle autorizzazioni")

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli di connessione di destinazione](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Immagine dell’interfaccia utente di Platform, che mostra i dettagli della connessione di destinazione da compilare")

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID di TikTok Ads Manager]**: Le [!DNL TikTok Ads Manager ID]. Puoi trovarlo nel tuo [!DNL TikTok Ads manager] conto.

![ID di TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Immagine dell’interfaccia utente di TikTok Ads Manager, che mostra come ottenere l’ID TikTok Ads Manager")

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Mappare le identità {#map}

Di seguito è riportato un esempio di corretta mappatura delle identità durante l’esportazione dei segmenti in TikTok Ads Manager.

Selezione dei campi di origine:

* Seleziona un identificatore (ad esempio:` Email_LC_SHA256`) come identità sorgente che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL TikTok Ads Manager].

Selezione dei campi di destinazione:

* Seleziona lo spazio dei nomi e-mail come identità di destinazione.

![Mappatura identità](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Immagine dell’interfaccia utente della piattaforma, mappatura delle identità")

## Dati esportati {#exported-data}

Controlla il tuo [!DNL TikTok Ads Manager] conto (in **Risorse > Tipi di pubblico**) per verificare se il segmento di Experience Platform è stato esportato correttamente. Il pubblico viene popolato come tipo di pubblico: `Partner Audience`.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Fai riferimento alla [Pagina Centro assistenza TikTok](https://ads.tiktok.com/help/article/audiences?lang=en) per ulteriori informazioni.
