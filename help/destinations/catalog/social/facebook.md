---
keywords: estensioni facebook;estensione facebook;destinazioni facebook;facebook;instagram;messenger;facebook messenger
title: Destinazione Facebook
seo-title: Destinazione Facebook
description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
seo-description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
translation-type: tm+mt
source-git-commit: d0b6225a726c13e2b77ea0f61446ea489df81e69
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 3%

---


# [!DNL Facebook] Destinazione

## Panoramica {#overview}

Attiva profili per le tue campagne [!DNL Facebook] per il targeting dell&#39;audience, la personalizzazione e la soppressione basate su e-mail con hash.

Puoi utilizzare questa destinazione per il targeting dell&#39;audience tra [!DNL Facebook’s] la famiglia di app supportate da [!DNL Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell’app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione Facebook nell’interfaccia utente di Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casi d’uso

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Facebook], ecco due esempi di casi di utilizzo che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso di utilizzo n. 1

Un rivenditore online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate in base ai loro ordini precedenti. Il rivenditore online può inserire indirizzi e-mail da CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare questi segmenti alla [!DNL Facebook] piattaforma social, ottimizzando le spese pubblicitarie.

### Caso di utilizzo n. 2

Una compagnia aerea ha diversi livelli di clienti (Bronzo, Argento e Oro) e vuole fornire a ciascuno dei livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l&#39;app mobile della compagnia aerea e alcuni di essi non hanno effettuato l&#39;accesso al sito Web della società. Gli unici identificatori della società per questi clienti sono gli ID iscrizione e gli indirizzi e-mail.

Per utilizzarli nei social media, possono tenere a bordo i dati del cliente dal CRM all&#39;Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

In seguito, possono utilizzare i dati offline, inclusi gli ID di appartenenza associati e i livelli cliente, per creare nuovi segmenti di pubblico ai quali indirizzare attraverso la destinazione [!DNL Facebook].

## Specifiche di destinazione {#destination-specs}

### Gestione dei dati per [!DNL Facebook] destinazioni {#data-governance}

>[!IMPORTANT]
>
>I dati inviati a [!DNL Facebook] non devono includere identità unite. L&#39;Utente è tenuto a rispettare tale obbligo e può farlo accertandosi che i segmenti selezionati per l&#39;attivazione non utilizzino un&#39;opzione di cucitura nel proprio criterio di unione. Ulteriori informazioni su [criteri di unione](/help/profile/ui/merge-policies.md).

### Tipo di esportazione {#export-type}

**Esportazione**  segmento - vengono esportati tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono, ecc.) utilizzato nella destinazione Facebook.

### Prerequisiti dell&#39;account Facebook {#facebook-account-prerequisites}

Prima di inviare i segmenti di pubblico a [!DNL Facebook], verifica di soddisfare i seguenti requisiti:

- L&#39;account utente [!DNL Facebook] deve avere l&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che si intende utilizzare.
- L&#39;account **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Per ulteriori informazioni, vedere [Aggiungi partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook.
   >[!IMPORTANT]
   >
   > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, è necessario abilitare l&#39;autorizzazione **Gestisci campagne**. Questa è richiesta per l’integrazione di [!DNL Adobe Experience Platform].
- Leggi e firma le [!DNL Facebook Custom Audiences] Condizioni del servizio. Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

### Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] richiede che non siano inviate informazioni personali (PII) in modo chiaro. Di conseguenza, è possibile disattivare gli identificatori [!DNL Facebook] con hash *con*, ad esempio indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

#### Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

- **Inserimento di numeri** di telefono non elaborati: è possibile inserire i numeri di telefono non elaborati nel  [!DNL E.164] formato  [!DNL Platform], che verranno automaticamente crittografati al momento dell&#39;attivazione. Se scegliete questa opzione, accertatevi di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164`.
- **Inserimento di numeri** di telefono con hash: è possibile pre-hash i numeri di telefono prima di inviarli in  [!DNL Platform]. Se scegliete questa opzione, accertatevi di inserire sempre i numeri di telefono con hash nello spazio dei nomi `Phone_SHA256`.

>[!NOTE]
>
>I numeri di telefono acquisiti nello spazio dei nomi `Phone` non possono essere attivati in [!DNL Facebook].


#### Requisiti di hashing e-mail {#email-hashing-requirements}

Potete scegliere di hash gli indirizzi e-mail prima di inviarli in Adobe Experience Platform, oppure potete scegliere di lavorare con gli indirizzi e-mail in  Experience Platform e ottenere l&#39;hash del nostro algoritmo al momento dell&#39;attivazione.

Per informazioni sull&#39;acquisizione di indirizzi e-mail in  Experience Platform, vedere la [panoramica sull&#39;assimilazione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull&#39;assimilazione a vapore](/help/ingestion/streaming-ingestion/overview.md).

Se selezionate l’hash degli indirizzi e-mail, accertatevi di soddisfare i seguenti requisiti:

- Rifila tutti gli spazi iniziali e finali dalla stringa e-mail; esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
- Durante l&#39;hashing delle stringhe e-mail, assicurarsi di eseguire l&#39;hash della stringa minuscola;
   - Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
- Verificate che la stringa con hash sia in lettere minuscole
   - Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Non saldare la stringa.

I dati provenienti dagli spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] al momento dell&#39;attivazione.

I dati origine attributo non vengono automaticamente crittografati. Se il campo di origine contiene attributi non crittografati, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione.
![Trasformazione mapping identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare lo spazio dei nomi `Extern_ID` per inviare dati a [!DNL Facebook], assicurarsi di sincronizzare i propri identificatori utilizzando [!DNL Facebook Pixel]. Per informazioni dettagliate, vedere la [documentazione ufficiale](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers).

## Connetti alla destinazione {#connect-destination}

Per connettersi alla destinazione [!DNL Facebook], vedere [Flusso di lavoro di autenticazione delle destinazioni social network](./workflow.md).

## Attivare i segmenti su [!DNL Facebook] {#activate-segments}

Per istruzioni su come attivare i segmenti in [!DNL Facebook], vedere [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

Nel passaggio **[!UICONTROL Segment schedule]**, è necessario fornire il [!UICONTROL Origin of audience] quando si inviano segmenti a [!DNL Facebook Custom Audiences].

![Facebook Origin of Audience](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], un&#39;attivazione riuscita implica la creazione di un&#39;audience [!DNL Facebook] personalizzata a livello di programmazione in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L&#39;integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta i backfill storici del pubblico. Tutte le qualifiche del segmento storico vengono inviate a [!DNL Facebook] quando si attivano i segmenti nella destinazione.