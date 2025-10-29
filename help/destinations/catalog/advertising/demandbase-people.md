---
title: Connessione Demandbase People
description: Utilizza questa destinazione per attivare i tipi di pubblico e arricchirli con i dati di terze parti Demandbase, per altri casi d’uso a valle nel marketing e nelle vendite.
exl-id: 748f5518-7cc1-4d65-ab70-4a129d9e2066
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 4%

---

# Connessione Demandbase People {#demandbase-people}

Attiva profili per le campagne Demandbase per il targeting, la personalizzazione e l’eliminazione del pubblico.

>[!IMPORTANT]
>
>Per i casi di utilizzo B2B in cui è necessario [attivare i tipi di pubblico dell&#39;account](../../ui/activate-account-audiences.md), utilizza il connettore di destinazione [Demandbase](demandbase.md).

## Caso d’uso {#use-case}

Gli addetti al marketing possono utilizzare Adobe Real-Time CDP per creare un Elenco persone di contatti di prime parti e attivarlo in Demandbase per un coinvolgimento ottimizzato e orchestrato sulla piattaforma lato domanda (DSP) e su altri canali come LinkedIn.

Questo approccio consente agli addetti al marketing di dare priorità alla spesa delle campagne su individui noti provenienti dal proprio sistema di gestione delle relazioni con i clienti o di automazione del marketing, garantendo che le attività di marketing si concentrino su potenziali clienti di alto valore.

Una volta attivata, Demandbase ottimizza la distribuzione degli annunci, perfezionando le strategie di targeting per massimizzare il coinvolgimento, la portata e i tassi di conversione, migliorando in ultima analisi l’efficienza della campagna.

## Identità supportate {#supported-identities}

La connessione [!DNL Demandbase People] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzi e-mail in testo normale | Solo gli indirizzi di posta elettronica in testo normale sono supportati dalla connessione [!DNL Demandbase People]. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importati](../../../segmentation/ui/overview.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-and-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|--------------|-----------|---------------------------|
| Tipo di esportazione | Esportazione pubblico | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione *Demandbase*. |
| Frequenza | Streaming | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per esportare i tipi di pubblico in Demandbase, è necessario quanto segue:

1. Un account Demandbase.
2. Un token API Demandbase. Puoi generare un token API con l’utente in Demandbase. Per generare un token, passa a [Profilo personale > Token API](https://web.demandbase.com/o/ad/at) dopo aver effettuato l&#39;accesso all&#39;account Demandbase.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione di controllo di accesso **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

![Aggiungi token bearer](../../assets/catalog/advertising/demandbase-people/bearer-token.png)

* **[!UICONTROL Bearer token]**: compila il token Bearer per l&#39;autenticazione nella destinazione. Visualizza [prerequisiti](#prerequisites) per informazioni su come ottenere il token.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Aggiungi informazioni sulla connessione di destinazione](../../assets/catalog/advertising/demandbase-people/name-and-description.png)

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

Ora puoi attivare i tuoi tipi di pubblico in Demandbase People.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappature obbligatorie {#mandatory-mappings}

Quando si attivano i tipi di pubblico nella destinazione [!DNL Demandbase People], è necessario configurare le seguenti mappature di campi obbligatorie nel passaggio di mappatura:

| Campo di origine | Campo di destinazione | Descrizione |
|--------------|--------------|-------------|
| `xdm: b2b.personKey.sourceKey` | `xdm: externalPersonId` | Identificatore univoco della persona |
| `xdm: person.name.lastName` | `xdm: lastName` | Cognome della persona |
| `xdm: person.name.firstName` | `xdm: firstName` | Nome della persona |
| `xdm: workEmail.address` | `Identity: email` | Indirizzo e-mail aziendale della persona |

![Mappature persone Demandbase](/help/destinations/assets/catalog/advertising/demandbase-people/demandbase-people-mapping.png)

Queste mappature sono necessarie per il corretto funzionamento della destinazione e devono essere configurate prima di poter procedere con il flusso di lavoro di attivazione.

## Note aggiuntive e callout importanti {#additional-notes}

* **Guardrail API Demandbase**: se hai esportato tipi di pubblico in Demandbase e le esportazioni hanno avuto esito positivo in Experience Platform, ma non tutti i dati raggiungono Demandbase, potresti aver riscontrato una limitazione API sul lato Demandbase. Rivolgiti a loro per chiarimenti.
* **Eliminazione elenco**: gli elenchi Persone sono univoci, pertanto non è possibile ricreare un nuovo elenco con un nome già in uso. Quando si rimuovono persone da un elenco, queste non saranno più disponibili, ma non verranno eliminate.
* **Ora di attivazione**: il caricamento dei dati in Demandbase è soggetto a elaborazione notturna.
* **Denominazione del pubblico**: se un pubblico account con lo stesso nome è stato attivato in precedenza in Demandbase, non è possibile riattivarlo tramite un flusso di dati diverso nella destinazione Demandbase.
