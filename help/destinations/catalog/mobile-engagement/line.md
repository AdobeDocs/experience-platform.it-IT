---
keywords: mobile;mobile engagement destinations;LINE;LINE mobile engagement destinations;LINE mobile engagement destination
title: Connessione LINE
description: La destinazione LINE ti consente di aggiungere profili al pubblico di Platform e di fornire esperienze personalizzate agli utenti connessi.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 2%

---

# Connessione [!DNL LINE]

## Panoramica {#overview}

[[!DNL LINE]](https://line.me/en/) è una piattaforma di comunicazione popolare che collega persone, servizi e informazioni ed è cresciuta da un&#39;app di chat a un hub per l&#39;intrattenimento, il social e le attività quotidiane.

Questa [!DNL Adobe Experience Platform] [destinazione](/help/destinations/home.md) sfrutta l&#39;API [[!DNL LINE] Messaging](https://developers.line.biz/en/reference/messaging-api/). Puoi attivare profili dai tipi di pubblico di Experience Platform come connessioni all&#39;interno di [!DNL LINE] per le tue esigenze aziendali.

[!DNL LINE] utilizza i token Bearer come meccanismo di autenticazione per comunicare con l&#39;API di messaggistica [!DNL LINE]. Le istruzioni per l&#39;autenticazione nell&#39;istanza [!DNL LINE] sono riportate di seguito, nella sezione [Autentica nella destinazione](#authenticate).

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, puoi indirizzare l&#39;attività agli utenti in una destinazione di coinvolgimento mobile, con tipi di pubblico incorporati in [!DNL Adobe Experience Platform]. Inoltre, puoi fornire loro esperienze personalizzate, basate sugli attributi dei loro profili [!DNL Adobe Experience Platform], non appena i tipi di pubblico e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Prerequisiti {#prerequisites}

### [!DNL LINE] prerequisiti {#prerequisites-destination}

Per esportare i dati da Platform al tuo account [!DNL LINE], tieni presente i seguenti prerequisiti in [!DNL LINE]:

#### Devi avere un account [!DNL LINE] {#prerequisites-account}

Se non ne hai già uno, devi registrarti e creare un account [!DNL LINE]. Per creare un account:

1. Accedi alla pagina [!DNL LINE] [account di accesso](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F)
2. Selezionare **[!UICONTROL Crea un account]**.

#### Raccogliere [!DNL LINE channel access token (long-lived)] dalla console per sviluppatori [!DNL LINE] {#gather-credentials}

Per consentire a Platform di accedere alle risorse [!DNL LINE], è necessario *[!DNL Channel access token (long-lived)]* dal canale [!DNL LINE] *Messaging API* desiderato.

1. Accedi con il tuo account [!DNL LINE] alla [[!DNL LINE] Console sviluppatori](https://developers.line.biz/console).
1. Accedere all&#39;elenco *[!DNL Providers]*, quindi selezionare *[!DNL Provider]* di interesse e infine selezionare il canale *API di messaggistica* per accedere alle relative impostazioni. Se accedi alla console per sviluppatori per la prima volta, segui la [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per completare i passaggi necessari per creare un provider.
1. Infine, passa alla sezione ***[!DNL Channel access token]*** e copia il valore ***[!DNL Channel access token (long-lived)]*** richiesto nel passaggio [Autentica nella destinazione](#authenticate).

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

Consulta la [[!DNL LINE] documentazione](https://developers.line.biz/en/docs/messaging-api/getting-started/) per informazioni su come creare un canale o aggiungere un canale all&#39;account [!DNL LINE] esistente tramite la console per sviluppatori [!DNL LINE].

## Identità supportate {#supported-identities}

[!DNL LINE] supporta l&#39;aggiornamento e l&#39;esportazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| ID per inserzionisti (IFA) | Selezionare l&#39;ID per l&#39;identità di destinazione degli inserzionisti (IFA) quando le identità di origine sono spazi dei nomi IFA *(Apple ID per inserzionisti)* o GAID *(Google Advertising ID). |
| ID utente LINE | Selezionare l&#39;identità di destinazione UserID quando le identità di origine sono ID utente LINE. |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL LINE]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

All&#39;interno di **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, cerca [!DNL LINE]. In alternativa, è possibile individuarlo nella categoria **[!UICONTROL Mobile engagement]**.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.
![Schermata dell&#39;interfaccia utente di Platform che mostra come eseguire l&#39;autenticazione.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

Compila i campi obbligatori di seguito.
* **[!UICONTROL Token Bearer]**: [!DNL LINE Channel access token (long-lived)] dalla console per sviluppatori [!DNL LINE]. Consulta la sezione [raccogliere le credenziali](#gather-credentials).

Se i dettagli forniti sono validi, nell&#39;interfaccia utente viene visualizzato lo stato **[!UICONTROL Connesso]** con un segno di spunta verde. A questo punto è possibile procedere al passaggio successivo.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Schermata dell&#39;interfaccia utente di Platform che mostra i dettagli della destinazione.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Tipo di pubblico]**: seleziona **[!UICONTROL ID per inserzionisti (IFA)]** se le identità che desideri esportare sono di tipo *ID per inserzionisti (IFA)*. Selezionare **[!UICONTROL ID utente LINE]** se le identità da esportare sono di tipo *ID utente LINE*. Per ulteriori informazioni sui tipi di identità, consulta la sezione [Identità supportate](#supported-identities).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da Adobe Experience Platform alla destinazione [!DNL LINE], è necessario eseguire il passaggio di mappatura dei campi. La mappatura consiste nella creazione di un collegamento tra i campi dello schema Experience Data Model (XDM) nell’account Platform e i corrispondenti equivalenti dalla destinazione. Per mappare correttamente i campi XDM ai campi di destinazione [!DNL LINE], effettua le seguenti operazioni:

A seconda dell’identità di origine, è necessario mappare i seguenti spazi dei nomi dell’identità di destinazione:

| Identità di destinazione | Campo origine | Campo di destinazione |
| --- | --- | --- |
| ID per inserzionisti (IFA) | `IDFA` o `GAID` | `LineId` |
| ID utente LINE | `UserID` | `LineId` |

Se le identità di destinazione sono *ID utente LINE*, sarà necessario quanto segue:
![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra la mappatura di Target quando si utilizzano gli ID utente LINE per le identità di destinazione.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

Se l&#39;identità di destinazione è *ID per inserzionisti(IFA)*, sarà necessario quanto segue:
![Esempio di schermata dell&#39;interfaccia utente di Platform che mostra la mappatura di Target quando si utilizza un ID per gli inserzionisti (IFA) per le identità di destinazione.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## Convalidare l’esportazione dei dati {#exported-data}

Dopo un&#39;esportazione dei dati riuscita in Experience Platform, la destinazione [!DNL LINE] crea un nuovo pubblico in [!DNL LINE] utilizzando il nome del pubblico selezionato.

Per verificare di aver impostato correttamente la destinazione, segui i passaggi seguenti:

1. In [!DNL LINE], accedere alla console [Manager](https://manager.line.biz/).

1. Quindi, passa a **[!UICONTROL Controlli dati]** > **[!UICONTROL Tipi di pubblico]** e controlla il nome corrispondente al pubblico selezionato all&#39;interno della colonna **[!UICONTROL Nome pubblico]**.

1. Il volume aggiornato corrisponderebbe al conteggio all’interno del segmento.

1. La colonna *Type* menzionerà **[!UICONTROL UserID]** se le identità esportate sono di tipo *UserID*. Analogamente, la colonna *Tipo* menzionerà **[!UICONTROL ID annuncio mobile]** se le identità esportate sono di tipo *IDFA*.

Di seguito è riportato un esempio di configurazione in [!DNL LINE]:
![Schermata dell&#39;interfaccia utente LINE che mostra il volume del pubblico.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
