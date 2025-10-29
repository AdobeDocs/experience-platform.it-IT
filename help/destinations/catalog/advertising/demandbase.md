---
title: Connessione Demandbase
description: Utilizza questa destinazione per attivare i tipi di pubblico del tuo account per i casi d’uso di Account-Based Marketing (ABM). Pubblicizza a persone e ruoli rilevanti negli account target tramite il Demand Side Platform B2B (DSP) di DemandBase. Gli account target possono inoltre essere arricchiti con dati di terze parti di DemandBase, per altri casi d’uso downstream nel marketing e nelle vendite.
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
exl-id: a84609a2-f1d3-4998-9db4-ad59c0a0b631
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 17%

---

# Connessione Demandbase {#demandbase}

>[!AVAILABILITY]
>
>La funzionalità per attivare i tipi di pubblico dell&#39;account nella destinazione Demandbase è disponibile per le aziende che acquistano le edizioni [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) e [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) di Real-Time Customer Data Platform.

Attiva profili per le campagne Demandbase per il targeting, la personalizzazione e l&#39;eliminazione del pubblico, in base a [tipi di pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) .

## Caso d’uso {#use-case}

Utilizza questa destinazione per attivare i tipi di pubblico del tuo account per i casi d’uso di Account-Based Marketing (ABM). Pubblicizza a persone e ruoli rilevanti negli account target tramite il Demand Side Platform B2B (DSP) di DemandBase. Gli account target possono inoltre essere arricchiti con dati di terze parti di DemandBase, per altri casi d’uso downstream nel marketing e nelle vendite.

Ad esempio, sfrutta l’ad-tech DSP di Demandbase per eseguire il targeting di utenti tipo o ruoli specifici all’interno di account chiave per la generazione di lead top-of-funnel, oppure per creare e incrementare i gruppi di acquisto. Utilizza la destinazione Demandbase per esplorare altri casi d’uso per eseguire il targeting efficace dei tuoi account.

Con questa integrazione, puoi anche personalizzare l’esperienza del sito web utilizzando la ricerca delle informazioni dell’account in tempo reale per ottimizzare il coinvolgimento.

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
| Tipo di esportazione | Esportazione pubblico | Tutti i membri del pubblico verranno esportati con identificatori chiave come nome, numero di telefono e altro ancora. |
| Frequenza | Streaming | Connessioni basate su API sempre attive. Gli aggiornamenti vengono inviati a valle immediatamente dopo le modifiche al profilo. |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per esportare i tipi di pubblico dell’account in Demandbase, è necessario disporre dei seguenti elementi:

1. Un account Demandbase.
2. Un token API Demandbase. Puoi generare un token API con l’utente in Demandbase. Per generare un token, passa a [Profilo personale > Token API](https://web.demandbase.com/o/ad/at) dopo aver effettuato l&#39;accesso all&#39;account Demandbase.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione di controllo di accesso **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [&#128279;](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

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

Leggi [Attiva pubblico account](/help/destinations/ui/activate-account-audiences.md) per le istruzioni sull&#39;attivazione del pubblico account in questa destinazione.

### Mappature obbligatorie {#mandatory-mappings}

Quando si attivano i tipi di pubblico nella destinazione [!DNL Demandbase], è necessario configurare le seguenti mappature di campi obbligatorie nel passaggio di mappatura:

| Campo di origine | Campo di destinazione | Descrizione |
|--------------|--------------|-------------|
| `xdm: accountName` | `xdm: accountName` | Nome dell’account |
| `xdm: accountOrganization.domain` | `xdm: accountEmailDomain` | Dominio e-mail dell’organizzazione dell’account |
| `xdm: accountKey.sourceKey` | `Identity: primaryId` | Identificatore principale dell’account |

![Mappature Demandbase](/help/destinations/assets/catalog/advertising/demandbase/demandbase-mapping.png)

Queste mappature sono necessarie per il corretto funzionamento della destinazione e devono essere configurate prima di poter procedere con il flusso di lavoro di attivazione.

## Note aggiuntive e callout importanti {#additional-notes}

* Se un pubblico di account con lo stesso nome è stato attivato in precedenza in Demandbase, non puoi attivarlo nuovamente tramite un flusso di dati diverso nella destinazione Demandbase.
* Se hai esportato tipi di pubblico in Demandbase e le esportazioni hanno avuto esito positivo in Experience Platform, ma non tutti i dati raggiungono Demandbase, potresti aver riscontrato una limitazione API sul lato Demandbase. Rivolgiti a loro per chiarimenti.
