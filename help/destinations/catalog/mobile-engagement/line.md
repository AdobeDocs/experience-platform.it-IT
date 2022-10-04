---
keywords: mobile;destinazioni di coinvolgimento mobile;LINE;LINE;destinazione di coinvolgimento mobile LINE
title: Collegamento LINE
description: La destinazione LINE ti consente di aggiungere profili al segmento Platform e di fornire esperienze personalizzate agli utenti collegati.
source-git-commit: 10c04bdee8536194baea00d3466c758f848c46c5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# [!DNL LINE] connection

## Panoramica {#overview}

[[!DNL LINE]](https://line.me/en/) è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un&#39;app di chat a un hub per l&#39;intrattenimento, i social e le attività quotidiane.

Questo [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta [[!DNL LINE] API di messaggistica](https://developers.line.biz/en/reference/messaging-api/). Puoi attivare profili dai segmenti di Experience Platform come connessioni all’interno di [!DNL LINE] per le tue esigenze aziendali.

[!DNL LINE] utilizza i token portatori come meccanismo di autenticazione per comunicare con [!DNL LINE] API di messaggistica. Istruzioni per l&#39;autenticazione al tuo [!DNL LINE] l&#39;istanza è più in basso, all&#39;interno di [Autentica a destinazione](#authenticate) sezione .

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi indirizzare gli utenti a una destinazione di coinvolgimento mobile, con i segmenti incorporati [!DNL Adobe Experience Platform]. Inoltre, puoi fornire loro esperienze personalizzate, in base agli attributi dei rispettivi [!DNL Adobe Experience Platform] non appena i segmenti e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Prerequisiti {#prerequisites}

### [!DNL LINE] prerequisiti {#prerequisites-destination}

Prendi nota dei seguenti prerequisiti in [!DNL LINE], per esportare i dati da Platform al tuo [!DNL LINE] account:

#### Devi avere un [!DNL LINE] account {#prerequisites-account}

Vai a [!DNL LINE] [iscrizione](https://account.line.biz/signup) per registrare e creare un account, se non ne hai già uno.

#### Raccogli [!DNL LINE channel access token (long-lived)] dal [!DNL LINE] console per sviluppatori {#gather-credentials}

Per consentire l’accesso a Platform [!DNL LINE] risorse, sarà necessario *[!DNL Channel access token (long-lived)]* dal desiderato [!DNL LINE] *API di messaggistica* canale.

1. Accedi con il tuo [!DNL LINE] al [[!DNL LINE] Console per sviluppatori](https://developers.line.biz/console).
1. Quindi, accedi al *[!DNL Providers]* seleziona l’elenco *[!DNL Provider]* di interesse e infine seleziona il *API di messaggistica* per accedere alle relative impostazioni. Se accedi per la prima volta alla console di sviluppo , segui la [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per completare i passaggi necessari per creare un provider.
1. Infine, passa alla ***[!DNL Channel access token]*** e copia la sezione ***[!DNL Channel access token (long-lived)]*** valore richiesto in [Autentica a destinazione](#authenticate) passo.

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | Il [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Fai riferimento a [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per informazioni sulla creazione di un canale o sull’aggiunta di un canale al tuo esistente [!DNL LINE] tramite [!DNL LINE] console per sviluppatori.

## Identità supportate {#supported-identities}

[!DNL LINE] supporta l’aggiornamento e l’esportazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| ID per inserzionisti (IFA) | Seleziona l’ID per l’identità di destinazione degli inserzionisti (IFA) quando le identità di origine sono IFA *(Apple ID per gli inserzionisti)* namespace o GAID *(Google Advertising ID). |
| ID utente LINE | Selezionare l&#39;identità di destinazione UserID quando le identità di origine sono ID utente LINE. |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nel [!DNL LINE] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Within **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]** cercare [!DNL LINE]. In alternativa, è possibile individuarlo sotto il **[!UICONTROL Partecipazione mobile]** categoria.

### Autentica a destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, seleziona **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell’interfaccia utente della piattaforma che mostra come eseguire l’autenticazione.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Compila i campi richiesti di seguito.
* **[!UICONTROL Token portatore]**: Le [!DNL LINE Channel access token (long-lived)] dal [!DNL LINE] console per sviluppatori. Fai riferimento a [raccogliere le credenziali](#gather-credentials) sezione .

Se i dettagli forniti sono validi, l’interfaccia utente visualizza un **[!UICONTROL Connesso]** stato con un segno di spunta verde. Puoi quindi procedere al passaggio successivo.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell’interfaccia utente della piattaforma che mostra i dettagli della destinazione.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Tipo di pubblico]**: Seleziona **[!UICONTROL ID per inserzionisti (IFA)]** se le identità che desideri esportare sono di tipo *ID per inserzionisti (IFA)*. Seleziona **[!UICONTROL ID utente LINE]** se le identità che desideri esportare sono di tipo *ID utente LINE*. Fai riferimento a [Identità supportate](#supported-identities) per ulteriori informazioni sui tipi di identità.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Mappare attributi e identità {#map}

Per inviare correttamente i dati del pubblico da Adobe Experience Platform al [!DNL LINE] destinazione, devi passare attraverso il passaggio di mappatura dei campi . La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM su [!DNL LINE] campi di destinazione, segui questi passaggi:

A seconda dell’identità di origine, è necessario mappare i seguenti namespace dell’identità di destinazione: | Identità di destinazione | Campo di origine | Campo di destinazione | | — | — | — | | ID per inserzionisti (IFA) | `IDFA` o `GAID` | `LineId` | | ID utente LINE | `UserID` | `LineId` |

Se le identità di destinazione sono *ID utente LINE* ti servirà quanto segue:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target quando si utilizzano gli ID utente LINE per le identità di destinazione.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Se l&#39;identità di destinazione è *ID per inserzionisti (IFA)* ti servirà quanto segue:
![Esempio di schermata dell’interfaccia utente della piattaforma che mostra la mappatura di Target quando si utilizza ID per gli inserzionisti (IFA) per le identità target.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Convalida esportazione dati {#exported-data}

Dopo un&#39;esportazione di dati riuscita da un Experience Platform, il [!DNL LINE] crea un nuovo pubblico all’interno di [!DNL LINE] utilizzando il nome del segmento selezionato.

Per verificare di aver configurato correttamente la destinazione, effettua le seguenti operazioni:

1. In [!DNL LINE], accedi a [Console Manager](https://manager.line.biz/).

1. Quindi, passa a **[!UICONTROL Controlli dei dati]** > **[!UICONTROL Tipi di pubblico]** e controlla il nome che corrisponde al segmento selezionato all’interno della **[!UICONTROL Nome del pubblico]** colonna.

1. Il volume aggiornato corrisponderebbe al conteggio all’interno del segmento.

1. La *Tipo* la colonna sarà menzionata **[!UICONTROL UserID]** se le identità esportate sono di tipo *UserID*. Analogamente, il *Tipo* la colonna sarà menzionata **[!UICONTROL ID annuncio mobile]** se le identità esportate sono di tipo *IDFA*.

Un esempio di configurazione in [!DNL LINE] è mostrato di seguito:
![Schermata dell’interfaccia utente LINE che mostra il volume di pubblico.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).