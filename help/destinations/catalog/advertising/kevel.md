---
title: Connessione Kevel
description: Utilizza la destinazione di streaming Kevel per attivare il pubblico direttamente nelle API UserDB e Segment Management di Kevel e supportare il targeting in tempo reale al momento della decisione.
source-git-commit: d820485fd81efd08d8626f8476338558c4585c20
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 3%

---


# Connessione [!DNL Kevel] {#kevel}

## Panoramica {#overview}

[[!DNL Kevel]](https://www.kevel.com/) fornisce la tecnologia basata sull&#39;intelligenza artificiale e la guida di esperti che aiutano i leader di settore innovativi a lanciare, scalare e avere successo nel settore dei media retail. Retail Media Cloud di [!DNL Kevel] offre formati di annunci mirati, attribuibili e personalizzabili per la pubblicità nel sito e fuori dal sito.

La destinazione di streaming [!DNL Kevel] per Adobe Experience Platform consente ai clienti di attivare i tipi di pubblico di Adobe direttamente nelle API UserDB e Segment Management di [!DNL Kevel] per supportare il targeting in tempo reale al momento della decisione dell&#39;annuncio.

>[!IMPORTANT]
> 
>Se hai domande o desideri richiedere un aggiornamento sulla destinazione [!DNL Kevel] o sulla relativa documentazione, invia un&#39;e-mail al team [!DNL Kevel] all&#39;indirizzo [support@kevel.com](mailto:support@kevel.com).

## Casi d’uso {#use-cases}

Puoi attivare tipi di pubblico comportamentali avanzati e di prime parti nelle esperienze multimediali per la vendita al dettaglio, per offrire annunci più rilevanti e prestazioni più elevate. In Experience Platform, puoi creare tipi di pubblico di alto valore basati su intent, ad esempio acquirenti di categorie frequenti o utenti con interessi recenti sui prodotti, e sincronizzare tali appartenenze a [!DNL Kevel] in tempo reale. [!DNL Kevel] rende immediatamente disponibili questi segmenti per le decisioni sugli annunci, abilitando il targeting preciso per i prodotti sponsorizzati e altri formati nelle esperienze di ricerca, navigazione e app. Non appena gli utenti si qualificano, puoi agire su questi segnali per ottenere impressioni più rilevanti, un targeting migliore e misurazioni e ROAS migliorati.

## Prerequisiti {#prerequisites}

Per prepararsi a utilizzare la destinazione [!DNL Kevel], verificare che siano soddisfatti i prerequisiti seguenti:

- È necessario disporre di una rete **[!DNL Kevel]** attiva e dell&#39;accesso API.
- È necessaria una chiave API **[!DNL Kevel]** con autorizzazioni per creare segmenti e aggiornare record UserDB.
- Devi configurare in Experience Platform gli spazi dei nomi delle identità mappati alle identità inviate dal sito o dall&#39;app durante [!DNL Kevel] richieste di annunci (ad esempio, ECID, GAID, IDFA, ID fedeltà, ecc.).
- I clienti di Adobe devono mappare solo le identità utilizzate durante le richieste di annunci in tempo reale, in quanto ogni identità darà luogo a un record UserDB.

## Identità supportate {#supported-identities}

La destinazione [!DNL Kevel] supporta l&#39;attivazione di qualsiasi identità utilizzata dall&#39;applicazione per l&#39;invio di richieste di annunci a [!DNL Kevel]. Puoi mappare fino a tre spazi dei nomi di identità per generare i record UserDB corrispondenti.

[!DNL Kevel] supporta i seguenti spazi dei nomi di identità di Experience Platform:

| Spazio dei nomi identità | Descrizione | Utilizzo tipico |
|--------------------|---------------------------------|----------------------------------------------------------------|
| **ECID** | Experience Cloud ID | Utilizzato per la personalizzazione nel sito e l’identificazione tra più Adobe. |
| **GAID** | GOOGLE ADVERTISING ID | Utilizzato per il traffico dell’app/dispositivo Android. |
| **IDFA** | APPLE ADVERTISING ID | Utilizzato per il traffico dell’app/dispositivo iOS (soggetto al consenso ATT). |
| **EXTERNAL_ID** | ID esterno (identificatore personalizzato) | Trasmette ID proprietari o generati dal back-end. |

{style="table-layout:auto"}

### Supporto per spazi dei nomi di identità personalizzati

La destinazione [!DNL Kevel] di **accetta anche spazi dei nomi personalizzati**, come definito nell&#39;implementazione di Experience Platform.

Ciò significa che:

- È possibile mappare **spazi dei nomi di identità specifici del cliente** (ad esempio: `loyalty_id`, `gigya_id` o qualsiasi identità personalizzata definita in Identity Service).
- Questi spazi dei nomi possono essere assegnati a `kevel_user_key1`, `kevel_user_key2` o `kevel_user_key3` nello stesso modo degli spazi dei nomi globali.
- [!DNL Kevel] genererà **un record UserDB per istanza di ogni identità mappata**, consentendo la corrispondenza in tempo reale al momento della decisione dell&#39;annuncio per ogni identificatore inviato dai sistemi.

### Comportamento di mappatura identità

- È possibile mappare **fino a tre** spazi dei nomi di identità di Experience Platform ai tre slot di identità di [!DNL Kevel].
- Per ogni profilo attivato, [!DNL Kevel] riceve **un record UserDB per istanza di ogni identità mappata**.
- I clienti devono mappare solo le identità effettivamente inviate nelle richieste di annunci a [!DNL Kevel] per evitare un inutile archivio UserDB.

![Esempio di mappatura per la destinazione Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-mappings.png)

## Tipi di pubblico supportati {#supported-audiences}

| Origine pubblico | Supportato | Descrizione |
|-----------------------|-----------|---------------------------------------------------------- |
| Servizio di segmentazione | Sì | Tipi di pubblico di Adobe Profile valutati dal motore di segmentazione. |
| Caricamenti personalizzati | No | Al momento non supportato. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

| Elemento | Tipo | Note |
|------|------|-------|
| Tipo di esportazione | **Esportazione segmento** | [!DNL Kevel] riceve un aggiornamento ogni volta che un profilo si qualifica per un pubblico o ne esce. |
| Frequenza di esportazione | **Streaming** | Gli aggiornamenti vengono inviati in tempo reale utilizzando Destination SDK Streaming Framework. |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

Segui il flusso di lavoro standard di Experience Platform [connetti una destinazione](../../ui/connect-destination.md).

>[!IMPORTANT]
> 
>È necessario disporre di **autorizzazioni Visualizza destinazioni** e **Gestisci destinazioni**.

### Autenticarsi nella destinazione {#authenticate}

Durante la connessione a [!DNL Kevel], fornire il seguente campo:

- **Token Bearer** - Chiave API [!DNL Kevel].

![Opzioni di autenticazione per la destinazione Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-authentication.png)

### Inserire i dettagli della destinazione {#destination-details}

Dopo l’autenticazione, configura:

- **Nome**: etichetta per identificare l&#39;istanza di destinazione.
- **Descrizione** — Testo facoltativo per descrivere questa istanza di destinazione.
- **[!DNL Kevel]ID di rete** — L&#39;identificatore di rete [!DNL Kevel].

![Dettagli destinazione per destinazione Kevel](/help/destinations/assets/catalog/advertising/kevel-destination-details.png)

## Attiva i segmenti in questa destinazione {#activate}

Per inviare tipi di pubblico a [!DNL Kevel], segui il flusso di lavoro in\
[Attiva profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md).

### Disattivazione dei tipi di pubblico {#deactivate}

Quando un pubblico viene disattivato o rimosso dalla destinazione [!DNL Kevel] in Experience Platform, Experience Platform smette di inviare ulteriori aggiornamenti di qualificazione del profilo per tale pubblico. Qualsiasi segmento esistente creato in [!DNL Kevel] rimane disponibile e non viene eliminato automaticamente.

Se il segmento [!DNL Kevel] è attualmente utilizzato in una campagna attiva, [!DNL Kevel] impedisce l&#39;eliminazione per evitare di interrompere la consegna live. In questo caso, la disattivazione in Experience Platform determina quanto segue:

- Il flusso di dati di Experience Platform si interrompe
- Il segmento [!DNL Kevel] continua a esistere e può rimanere associato alle campagne fino alla rimozione manuale o all&#39;aggiornamento della campagna

Per interrompere completamente il targeting in [!DNL Kevel], assicurati che il segmento venga rimosso da tutte le campagne attive nel sistema di gestione campagne di [!DNL Kevel].

### Mappare attributi e identità {#map}

[!DNL Kevel] richiede:

- **Spazi dei nomi di identità**: fino a tre spazi dei nomi di identità mappati a [!DNL Kevel] slot di identità.
- **Appartenenza al segmento**: non è richiesta alcuna mappatura manuale; Experience Platform trasmette automaticamente gli identificatori e gli alias di appartenenza al segmento.

Durante l&#39;attivazione, selezionare gli spazi dei nomi di identità configurati per [!DNL Kevel]. Ogni identità genera la propria chiamata di aggiornamento UserDB.

## Dati esportati / Convalida esportazione dati {#exported-data}

Quando un profilo si qualifica per un pubblico o ne esce, Experience Platform invia un aggiornamento in streaming a [!DNL Kevel].

### Payload di esempio ricevuto da [!DNL Kevel] UserDB

```json
PUT /udb/{networkId}/segments?userKey=ECID-12345
{
  "segments": [1723, 3344, 9988]
}
```

| Parametro | Descrizione |
|-----------|-------------|
| **chiaveUtente** | Derivato dall’identità Adobe mappata. |
| **segmenti** | Il set di [!DNL Kevel] ID segmento corrispondenti ai tipi di pubblico di Adobe per i quali è attualmente realizzato il profilo. |

{style="table-layout:auto"}

### Profilo Experience Platform di esempio utilizzato durante l’esportazione {#sample-profile}

Quando si attivano i tipi di pubblico nella destinazione [!DNL Kevel], Experience Platform invia frammenti di profilo contenenti sia le **qualifiche del segmento** che le **identità mappate dal cliente** agli slot di identità di [!DNL Kevel].

Di seguito è riportato un esempio di profilo esportato che mostra:

- Più spazi dei nomi di identità mappati a `kevel_user_key1`, `kevel_user_key2` e `kevel_user_key3`
- Un singolo segmento attivato nello spazio dei nomi `ups`

```json
{
  "segmentMembership": {
    "ups": {
      "9d161bbb-c785-474a-965b-7d7bc2adf879": {
        "status": "realized",
        "lastQualificationTime": "2025-12-10T21:43:38.541076Z"
      }
    }
  },
  "identityMap": {
    "kevel_user_key1": [
      {
        "id": "ECID-fN1zo"
      },
      {
        "id": "ECID-9Xr2p"
      }
    ],
    "kevel_user_key2": [
      {
        "id": "GAID-4oic4"
      }
    ],
    "kevel_user_key3": [
      {
        "id": "IDFA-nB5fU"
      }
    ]
  }
}
```

#### Come [!DNL Kevel] interpreta questo profilo

Con la configurazione di destinazione [!DNL Kevel], ogni identità mappata genera un record UserDB distinto, ovvero [!DNL Kevel] riceve:

- Un aggiornamento per `ECID-fN1zo`
- Un aggiornamento per `ECID-9Xr2p`
- Un aggiornamento per `GAID-4oic4`
- Un aggiornamento per `IDFA-nB5fU`

Questo consente di riconoscere la stessa persona al momento della decisione dell’annuncio utilizzando una qualsiasi delle identità disponibili, con ogni identità che trasporta un identico set di appartenenze a segmenti.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

- [[!DNL Kevel] Riferimento UserDB](https://dev.kevel.com/reference/userdb)
- [[!DNL Kevel] Impostazione destinazione segmento utente](https://dev.kevel.com/docs/segment-targeting)
