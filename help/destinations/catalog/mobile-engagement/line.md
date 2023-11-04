---
keywords: mobile;mobile engagement destinations;LINE;LINE mobile engagement destinations;LINE mobile engagement destination
title: Connessione LINE
description: La destinazione LINE ti consente di aggiungere profili al pubblico di Platform e di fornire esperienze personalizzate agli utenti connessi.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# Connessione [!DNL LINE]

## Panoramica {#overview}

[[!DNL LINE]](https://line.me/en/) è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un’app di chat a un hub per l’intrattenimento, il social e le attività quotidiane.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL LINE] API Messaging](https://developers.line.biz/en/reference/messaging-api/). Puoi attivare profili dal pubblico di Experienci Platform come connessioni in [!DNL LINE] per le esigenze aziendali.

[!DNL LINE] utilizza i token Bearer come meccanismo di autenticazione per comunicare con [!DNL LINE] API di messaggistica. Istruzioni per l’autenticazione [!DNL LINE] sono riportati di seguito, entro [Autentica nella destinazione](#authenticate) sezione.

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi indirizzare l’attività agli utenti in una destinazione di coinvolgimento mobile, con il pubblico integrato [!DNL Adobe Experience Platform]. Inoltre, puoi offrire loro esperienze personalizzate basate sugli attributi delle rispettive [!DNL Adobe Experience Platform] profili, non appena i tipi di pubblico e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Prerequisiti {#prerequisites}

### [!DNL LINE] prerequisiti {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti in [!DNL LINE], per esportare i dati da Platform al tuo [!DNL LINE] account:

#### Devi avere un [!DNL LINE] account {#prerequisites-account}

È necessario registrarsi e creare un [!DNL LINE] account, se non ne hai già uno. Per creare un account:

1. Accedi a [!DNL LINE] [accesso account](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) pagina
2. Seleziona **[!UICONTROL Creare un account]**.

#### Raccogliere il [!DNL LINE channel access token (long-lived)] dal [!DNL LINE] console per sviluppatori {#gather-credentials}

Per consentire l’accesso a Platform [!DNL LINE] risorse, è necessario disporre di *[!DNL Channel access token (long-lived)]* dal desiderato [!DNL LINE] *API Messaging* canale.

1. Accedi con il [!DNL LINE] account per [[!DNL LINE] Console per sviluppatori](https://developers.line.biz/console).
1. Quindi, accedi a *[!DNL Providers]* , quindi selezionare *[!DNL Provider]* e infine selezionare la *API Messaging* canale per accedere alle relative impostazioni. Se accedi alla Developer Console per la prima volta, segui la [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per completare i passaggi necessari per creare un provider.
1. Infine, passa a ***[!DNL Channel access token]*** e copia il ***[!DNL Channel access token (long-lived)]*** valore richiesto entro [Autentica nella destinazione](#authenticate) passaggio.

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Il [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulta la sezione [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per indicazioni sulla creazione di un canale o sull’aggiunta di un canale al [!DNL LINE] account tramite [!DNL LINE] console per sviluppatori.

## Identità supportate {#supported-identities}

[!DNL LINE] supporta l’aggiornamento e l’esportazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| ID per inserzionisti (IFA) | Seleziona l’ID di destinazione per gli inserzionisti (IFA) quando le identità di origine sono IFA *(Apple ID per inserzionisti)* o gli spazi dei nomi GAID *(Google Advertising ID). |
| ID utente LINE | Selezionare l&#39;identità di destinazione UserID quando le identità di origine sono ID utente LINE. |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati in [!DNL LINE] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Entro **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cerca [!DNL LINE]. In alternativa, è possibile posizionarlo sotto il **[!UICONTROL Coinvolgimento mobile]** categoria.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente di Platform che mostra come eseguire l’autenticazione.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Compila i campi obbligatori di seguito.
* **[!UICONTROL Token Bearer]**: il tuo [!DNL LINE Channel access token (long-lived)] dal [!DNL LINE] Developer Console. Consulta la sezione [raccogliere le credenziali](#gather-credentials) sezione.

Se i dettagli forniti sono validi, nell’interfaccia utente viene visualizzato un **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Tipo di pubblico]**: Seleziona **[!UICONTROL ID per inserzionisti (IFA)]** se le identità che desideri esportare sono di tipo *ID per inserzionisti (IFA)*. Seleziona **[!UICONTROL ID utente LINE]** se le identità che desideri esportare sono di tipo *ID utente LINE*. Consulta la sezione [Identità supportate](#supported-identities) per ulteriori informazioni sui tipi di identità.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform a [!DNL LINE] destinazione, devi passare attraverso il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM su [!DNL LINE] campi di destinazione, effettua le seguenti operazioni:

A seconda dell’identità di origine, è necessario mappare i seguenti spazi dei nomi dell’identità di destinazione: | Identità target | Campo di origine | Campo di destinazione | | — | — | — | | ID per inserzionisti (IFA) | `IDFA` o `GAID` | `LineId` | | ID utente LINE | `UserID` | `LineId` |

Se le identità di destinazione sono *ID utente LINE* avrà bisogno di quanto segue:
![Esempio di schermata dell’interfaccia utente di Platform che mostra la mappatura di Target quando si utilizzano gli ID utente LINE per le identità di destinazione.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Se l’identità di destinazione è *ID per inserzionisti (IFA)* avrà bisogno di quanto segue:
![Esempio di schermata dell’interfaccia utente di Platform che mostra la mappatura di Target quando si utilizza un ID per gli inserzionisti (IFA) per le identità di destinazione.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Convalidare l’esportazione dei dati {#exported-data}

In caso di esportazione corretta dei dati in Experience Platform, il [!DNL LINE] destinazione crea un nuovo pubblico in [!DNL LINE] utilizzando il nome del pubblico selezionato.

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. In entrata [!DNL LINE], accedi a [Console Manager](https://manager.line.biz/).

1. Quindi, passa a **[!UICONTROL Controlli dati]** > **[!UICONTROL Tipi di pubblico]** e controlla il nome che corrisponde al pubblico selezionato all’interno di **[!UICONTROL Nome del pubblico]** colonna.

1. Il volume aggiornato corrisponderebbe al conteggio all’interno del segmento.

1. Il *Tipo* la colonna menzionerà **[!UICONTROL UserID]** se le identità esportate sono di tipo *UserID*. Analogamente, *Tipo* la colonna menzionerà **[!UICONTROL ID annuncio mobile]** se le identità esportate sono di tipo *IDFA*.

Un esempio di configurazione in [!DNL LINE] è mostrato di seguito:
![Schermata dell’interfaccia utente LINE che mostra il volume del pubblico.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).
