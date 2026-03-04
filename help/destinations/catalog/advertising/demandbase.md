---
title: Connessione Demandbase
description: Utilizza questa destinazione per attivare i tipi di pubblico di account per i casi d’uso di Account-Based Marketing (ABM). Pubblicizza a persone e ruoli rilevanti negli account target tramite il Demand Side Platform B2B (DSP) di DemandBase. Gli account target possono inoltre essere arricchiti con dati di terze parti di DemandBase, per altri casi d’uso downstream nel marketing e nelle vendite.
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 5a03902df358d804cbafb401ffcef54eab240dfd
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 14%

---


# Connessione Demandbase {#demandbase}

>[!AVAILABILITY]
>
>La funzionalità per attivare il pubblico dell&#39;account nella destinazione Demandbase è disponibile per le aziende che acquistano le edizioni [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) di Real-time Customer Data Platform.

Attivare i profili per le campagne Demandbase per il targeting, la personalizzazione e la soppressione dei gruppi di destinatari in base ai [gruppi di destinatari dell&#39;account](/help/segmentation/types/account-audiences.md).

## Caso d’uso {#use-case}

Utilizza questa destinazione per attivare i tipi di pubblico di account per i casi d’uso di Account-Based Marketing (ABM). Pubblicizza a persone e ruoli rilevanti negli account target tramite il Demand Side Platform B2B (DSP) di DemandBase. Gli account target possono inoltre essere arricchiti con dati di terze parti di DemandBase, per altri casi d’uso downstream nel marketing e nelle vendite.

Ad esempio, sfrutta l’ad-tech DSP di Demandbase per eseguire il targeting di utenti tipo o ruoli specifici all’interno di account chiave per la generazione di lead top-of-funnel, oppure per creare e incrementare i gruppi di acquisto. Utilizza la destinazione Demandbase per esplorare altri casi d’uso per eseguire il targeting efficace dei tuoi account.

Con questa integrazione, puoi anche personalizzare l’esperienza del sito web utilizzando la ricerca delle informazioni dell’account in tempo reale per ottimizzare il coinvolgimento.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sì | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini dei gruppi di destinatari al di fuori dei gruppi di destinatari generati tramite [!DNL Segmentation Service]. Leggi le [varie origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li> gruppi di destinatari personalizzati [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV,</li><li> pubblico simile, </li><li> pubblico federato, </li><li> gruppi di destinatari generati in altre app di Experience Platform come Adobe Journey Optimizer, </li><li> e altro ancora. </li></ul> |

{style="table-layout:auto"}

Gruppi di destinatari supportati per tipo di dati:

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
|--------------------|-----------|-------------|-----------|
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti, consente di eseguire il targeting di gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | Sì | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Individui che non sono ancora clienti ma condividono le caratteristiche con il pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake di Adobe Experience Platform. | Report, flussi di lavoro di data science |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-and-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|--------------|-----------|---------------------------|
| Tipo di esportazione | Esportazione pubblico | Tutti i membri del pubblico verranno esportati con identificatori chiave come nome, numero di telefono e altro ancora. |
| Frequenza | Streaming | Connessioni basate su API &quot;Always-on&quot;. Gli aggiornamenti vengono inviati a valle immediatamente dopo la modifica del profilo. |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per esportare i tipi di pubblico dell’account in Demandbase, è necessario disporre dei seguenti elementi:

1. Un account Demandbase.
2. Un token API Demandbase. Puoi generare un token API con l’utente in Demandbase. Per generare un token, accedi a [Il mio profilo > Token API](https://web.demandbase.com/o/ad/at) dopo aver effettuato l’accesso all’account Demandbase.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessaria l&#39;autorizzazione **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica del controllo di accesso](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;[esercitazione sulla configurazione di destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

![Aggiungi token bearer](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL Bearer token]**: compila il token Bearer per l&#39;autenticazione nella destinazione. Visualizza [prerequisiti](#prerequisites) per informazioni su come ottenere il token.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Aggiungi informazioni sulla connessione di destinazione](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Entity type]**: selezionare **[!UICONTROL Account]** come tipo di entità.

Ora puoi attivare i tipi di pubblico in Demandbase.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei gruppi di destinatari dell&#39;account in questa destinazione, leggi [Attiva gruppi di destinatari dell&#39;account](/help/destinations/ui/activate-account-audiences.md).

### Mapping obbligatori {#mandatory-mappings}

Durante l&#39;attivazione dei gruppi di destinatari nella destinazione [!DNL Demandbase], è necessario configurare le mappature dei campi obbligatorie seguenti nel passaggio di mappatura:

| Campo di origine | Campo di destinazione | Descrizione |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | Nome dell’account |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | Dominio e-mail dell’organizzazione dell’account |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | Identificatore principale dell’account |

![Mappature Demandbase](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Queste mappature sono necessarie per il corretto funzionamento della destinazione e devono essere configurate prima di poter procedere con il flusso di lavoro di attivazione.

## Note aggiuntive e callout importanti {#additional-notes}

* **Denominazione dei gruppi di destinatari**: se un gruppo di destinatari con lo stesso nome è stato attivato in precedenza in Demandbase, non sarà possibile riattivarlo tramite un flusso di dati diverso nella destinazione Demandbase.
* **Guardrail API Demandbase**: se hai esportato tipi di pubblico in Demandbase e le esportazioni hanno avuto esito positivo in Experience Platform, ma non tutti i dati raggiungono Demandbase, potresti aver riscontrato una limitazione API sul lato Demandbase. Rivolgiti a loro per chiarimenti.
* **Eliminazione elenco**: gli elenchi account sono univoci, pertanto non è possibile ricreare un nuovo elenco con un nome già in uso. Quando si rimuovono account da un elenco, questi non saranno più disponibili, ma non verranno eliminati.
* **Ora di attivazione**: il caricamento dei dati in Demandbase è soggetto a elaborazione notturna.
