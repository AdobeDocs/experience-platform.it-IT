---
keywords: streaming, destinazione Qualtrics
title: Automazioni Qualtrics
description: Sincronizza i dati relativi all’esperienza e ai clienti operativi per sbloccare la personalizzazione su larga scala. Utilizza l’aggregazione di più fonti di dati operativi in Adobe Experience Platform come input in Qualtrics Experience ID per comprendere meglio i tuoi clienti e consentire un’attività di sensibilizzazione mirata per colmare il divario quando si tratta di comprendere le intenzioni, le emozioni e i driver di esperienza.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 2%

---

# Automazioni Qualtrics

## Panoramica {#overview}

Sincronizza i dati relativi all’esperienza e ai clienti operativi per sbloccare la personalizzazione su larga scala.

Utilizza l’aggregazione di più fonti di dati operativi in Adobe Experience Platform come input in Qualtrics Experience ID per comprendere meglio i tuoi clienti e consentire un’attività di sensibilizzazione mirata per colmare il divario quando si tratta di comprendere le intenzioni, le emozioni e i driver di esperienza.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team Qualtrics. Per eventuali richieste di informazioni o richieste di aggiornamento, contattale direttamente accedendo a [Customer Success Hub](https://support-portal.qualtrics.com/).

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il *Automazioni Qualtrics* destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso {#use-case-1}

**Scenario**: un’azienda vuole misurare la soddisfazione dei clienti in vari punti di contatto digitali, come il sito web e l’app mobile. Utilizzano Adobe Experience Platform per attivare i sondaggi Qualtrics in base alle interazioni degli utenti, ad esempio per completare un acquisto o visitare una pagina web specifica.

**Risultato**: raccogliendo feedback in tempo reale, l’azienda può migliorare la customer experience in base ai dati, garantendo maggiore soddisfazione e fedeltà.

### #2 del caso d’uso {#use-case-2}

**Scenario**: un’organizzazione mira a migliorare il processo di onboarding dei dipendenti. Utilizzano Adobe Experience Platform per raccogliere feedback dai nuovi assunti attraverso sondaggi Qualtrics. I sondaggi vengono attivati automaticamente dopo un periodo di onboarding predefinito.

**Risultato**: il feedback continuo consente all’organizzazione di adattare e migliorare il processo di onboarding, con conseguente miglioramento del coinvolgimento e della produttività tra i nuovi dipendenti.

## Prerequisiti

Prima di impostare la destinazione Qualtrics in Adobe Experience Platform, accertati di aver soddisfatto i seguenti prerequisiti:

* Hai un account Qualtrics.
* Hai ottenuto il token API necessario da Qualtrics.

### Ottenimento di un token API

Di seguito sono riportati i passaggi necessari per ottenere un token API da Qualtrics.

1. Accedi al tuo account Qualtrics.
2. Vai a **Impostazioni account**.
3. Seleziona **ID Qualtrics**.
4. In questa pagina, cerca **API** , contiene una sezione **Token** campo. Questo è il token API e sarà richiesto durante la configurazione della destinazione.

## Identità supportate {#supported-identities}

*Automazioni Qualtrics* supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzi e-mail in testo normale | Solo gli indirizzi e-mail in testo normale sono supportati da Qualtrics. |
| external_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati in *Automazioni Qualtrics* destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Come parte dell’autenticazione dovrai fornire una **Nome utente** e **Password**. Il nome utente è il nome utente Qualtrics e la password è il token API dell&#39;account Qualtrics. Per recuperare il token API, segui le istruzioni del **Prerequisiti** sopra.

![Autenticazione](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL URL]**: URL trovato in [Evento JSON](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) che attiva il tuo [workflow in Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Per un esempio, consulta la schermata seguente.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Questa destinazione dispone di uno schema aperto ed è quindi possibile inviare qualsiasi proprietà a Qualtrics.

#### Mappa attributi

Per aggiungere un attributo alla mappatura, seleziona semplicemente **attributi personalizzati** quando si aggiunge una nuova mappatura. È possibile immettere un nome qualsiasi per l&#39;attributo. Qualtrics incoraggia la *CamelCase* convenzione di denominazione per i nomi degli attributi (vedi la schermata seguente per un esempio).

![Attributo personalizzato](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Per un esempio di possibili mappature di attributi, consulta la schermata seguente.

![Esempi di mappature](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Mappare le identità

È obbligatorio selezionare uno spazio dei nomi delle identità per questa destinazione. I due possibili campi sorgente per il targeting delle mappature dei campi sono:

| Campo di origine | Campo di destinazione |
|--------------------|-----------------------|
| IdentityMap: e-mail | Identità: e-mail |
| IdentityMap: ECID | Identità: external_id |

Per un esempio, consulta la schermata seguente.

![Spazio dei nomi dell’identità](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Come accennato in precedenza, questa destinazione utilizza uno schema aperto, pertanto tutte le proprietà possono essere inviate a Qualtrics. Tuttavia, i dati inviati a Qualtrics si baseranno sulla seguente struttura:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Per verificare che i dati siano stati acquisiti in Qualtrics, passa al flusso di lavoro contenente **Evento JSON**, da lì, vai a **Cronologia esecuzione** dove dovresti trovare le esecuzioni del flusso di lavoro. Ogni flusso di lavoro ha uno stato **Completato** o **Non riuscito**. Selezionando una particolare esecuzione verranno visualizzate ulteriori informazioni su di essa, consentendo la risoluzione dei problemi in caso di problemi.

Se non ci sono esecuzioni visibili in **Cronologia esecuzione**, significa che il flusso di lavoro non è ancora stato attivato, a indicare che potrebbe esserci un problema. Assicurati che il flusso di lavoro sia abilitato e che **URL** nella destinazione in Adobe Experience Platform sia corretta. Le esecuzioni del flusso di lavoro non sono istantanee, pertanto potresti dover attendere un po’ prima che venga completato.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
