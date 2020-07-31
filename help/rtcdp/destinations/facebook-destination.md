---
title: Destinazione Facebook
seo-title: Destinazione Facebook
description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
seo-description: Attiva profili per le tue campagne Facebook per il targeting dell'audience, la personalizzazione e la soppressione basate su e-mail con hash.
translation-type: tm+mt
source-git-commit: 7f3df12da5e93c3d0cc53eed1aa603ddbafdb0b2
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---


# [!DNL Facebook] Destinazione

## Panoramica {#overview}

Attiva profili per le tue [!DNL Facebook] campagne di targeting dell&#39;audience, personalizzazione e soppressione basate su e-mail con hash.

![Destinazione Facebook nell’interfaccia CDP in tempo reale](/help/rtcdp/destinations/assets/facebook-destination.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando devi utilizzare la [!DNL Facebook] destinazione, ecco due esempi di casi d&#39;uso che  clienti Platform di dati cliente in tempo reale Adobe possono risolvere utilizzando questa funzione.


### Caso di utilizzo n. 1


Un rivenditore online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate in base ai loro ordini precedenti. Il rivenditore online può acquisire indirizzi e-mail da CRM a  CDP in tempo reale, creare segmenti dai propri dati offline e inviare questi segmenti alla piattaforma [!DNL Facebook] social, ottimizzando le spese pubblicitarie.


### Caso di utilizzo n. 2


Una compagnia aerea ha diversi livelli di clienti (Bronzo, Argento e Oro) e vuole fornire a ciascuno dei livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l&#39;app mobile della compagnia aerea e alcuni di essi non hanno effettuato l&#39;accesso al sito Web della società. Gli unici identificatori della società per questi clienti sono gli ID iscrizione e gli indirizzi e-mail.

Per utilizzarli nei social media, possono tenere a bordo i dati del cliente dal CRM al CDP in tempo reale  Adobe, utilizzando gli indirizzi e-mail come identificatori.

In seguito, possono utilizzare i dati offline, inclusi gli ID di appartenenza associati e i livelli cliente, per creare nuovi segmenti di pubblico ai quali indirizzare attraverso la [!DNL Facebook] destinazione.

## Specifiche di destinazione {#destination-specs}

### Gestione dei dati per [!DNL Facebook] le destinazioni {#data-governance}

>[!IMPORTANT]
>
>I dati inviati a non [!DNL Facebook] devono includere identità unite. L&#39;Utente è tenuto a rispettare tale obbligo e può farlo accertandosi che i segmenti selezionati per l&#39;attivazione non utilizzino un&#39;opzione di cucitura nel proprio criterio di unione. Ulteriori informazioni sui criteri di [unione](/help/profile/ui/merge-policies.md).

### Tipo di attivazione {#activation-type}

**Esportazione** segmento - vengono esportati tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono, ecc.) utilizzato nella destinazione Facebook.

### Prerequisiti per l’account Facebook {#facebook-account-prerequisites}

Prima di inviare i segmenti di pubblico a [!DNL Facebook], accertati di soddisfare i seguenti requisiti:

1. L&#39;account [!DNL Facebook] utente deve avere l&#39; **[!DNL Manage campaigns]** autorizzazione abilitata per l&#39;account annuncio che intendi utilizzare.
2. Add the **Adobe Experience Cloud** business account as an advertising partner in your [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Per informazioni, consulta [Aggiungere partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook.
   >[!IMPORTANT]
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Questa è richiesta per l’integrazione di [!DNL Adobe Real-time CDP].
3. Leggi e firma le [!DNL Facebook Custom Audiences] Condizioni del servizio. Per fare questo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

### Requisiti di hashing e-mail {#email-hashing-requirements}

[!DNL Facebook] richiede che non siano inviate informazioni personali (PII) in modo chiaro. Di conseguenza, i tipi di pubblico a cui si [!DNL Facebook] è attivato devono essere cancellati dagli indirizzi e-mail *con hash* . Potete scegliere di hash gli indirizzi e-mail prima di inserirli in  Adobe Experience Platform, oppure potete scegliere di lavorare con gli indirizzi e-mail in modo chiaro in  Experience Platform e avere il nostro algoritmo hash al momento dell&#39;attivazione.

Per informazioni sull’assimilazione degli indirizzi e-mail in  Experience Platform, consultate la panoramica [sull’assimilazione](/help/ingestion/batch-ingestion/overview.md) batch e la panoramica [sull’assimilazione](/help/ingestion/streaming-ingestion/overview.md)accattivante.

Se selezionate l’hash degli indirizzi e-mail, accertatevi di soddisfare i seguenti requisiti:

* Rifila tutti gli spazi iniziali e finali dalla stringa e-mail; esempio: `johndoe@example.com`, not `<space>johndoe@example.com<space>`;
* Durante l&#39;hashing delle stringhe e-mail, assicurarsi di eseguire l&#39;hash della stringa minuscola;
   * Esempio: `example@email.com`, not `EXAMPLE@EMAIL.COM`;
* Verificate che la stringa con hash sia in lettere minuscole
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non saldare la stringa.


>[!IMPORTANT]
>
>Se si sceglie di non utilizzare l&#39;hash degli indirizzi e-mail,  CDP in tempo reale Adobe lo farà automaticamente quando si attivano i segmenti in [!DNL Facebook]. Nel flusso di lavoro [di](/help/rtcdp/destinations/activate-destinations.md#activate-data) attivazione (vedere il punto 5), selezionate l’ `Email` opzione come mostrato di seguito per gli indirizzi *e-mail* non elaborati e `Email_LC_SHA256` per gli indirizzi e-mail *con* hash.


![Hashing all&#39;attivazione](/help/rtcdp/destinations/assets/identity-mapping.png)

## Connetti alla destinazione {#connect-destination}

Per connettersi alla [!DNL Facebook] destinazione, vedi Flusso di lavoro [di autenticazione delle destinazioni della rete](/help/rtcdp/destinations/social-network-destinations-workflow.md)social.


## Attiva i segmenti in [!DNL Facebook] {#activate-segments}

Per istruzioni su come attivare i segmenti in [!DNL Facebook], consulta [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

## Dati esportati {#exported-data}

Ad [!DNL Facebook]esempio, un&#39;attivazione riuscita significa che un&#39;audience [!DNL Facebook] personalizzata verrà creata a livello di programmazione in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L&#39;integrazione tra  CDP in tempo reale del Adobe e [!DNL Facebook] supporta le ricadute storiche del pubblico. Tutte le qualifiche del segmento storico vengono inviate a [!DNL Facebook] quando si attivano i segmenti alla destinazione.