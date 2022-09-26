---
title: Connessione Verizon MediaYahoo DataX
description: DataX è un’infrastruttura globale Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i suoi partner esterni in modo sicuro, automatizzato e scalabile.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: f61771ec11b8bd2d19e303b39e57e82da8f11ead
workflow-type: tm+mt
source-wordcount: '789'
ht-degree: 3%

---

# [!DNL Verizon Media/Yahoo DataX] connection

## Panoramica {#overview}

[!DNL DataX] è un aggregato [!DNL Verizon Media/Yahoo] infrastruttura che ospita vari componenti che consentono [!DNL Verizon Media/Yahoo] scambiare dati con i partner esterni in modo sicuro, automatizzato e scalabile.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da [!DNL Verizon Media/Yahoo]s [!DNL DataX] squadra. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Prerequisiti {#prerequisites}

**ID MDM**

Questo è un identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per l’impostazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo [!DNL Yahoo DataX] account manager.

**Metadati tassonomici**

La risorsa Tassonomia definisce un&#39;estensione sulla base [!DNL DataX] Struttura metadati

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Ulteriori informazioni [Metadati della tassonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) in [!DNL DataX] documentazione per gli sviluppatori.

## Limiti di aliquote e protezioni {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Quando si attivano più di 100 segmenti in [!DNL Verizon Media/Yahoo DataX], potresti ricevere errori di limitazione della velocità dalla destinazione. Quando si attivano i segmenti nel [!DNL Yahoo/DataX] destinazione, si consiglia di attivare meno di 100 segmenti in un flusso di dati di attivazione. Per attivare più segmenti, crea una nuova destinazione sullo stesso account.

[!DNL DataX] è limitato al tasso in base ai limiti della quota per i post di tassonomia e pubblico descritti nel [Documentazione DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Codice di errore | Messaggio di errore | Descrizione |
|---------|----------|---------|
| 429 Troppe richieste | Limite di velocità superato all&#39;ora **(Limite: 100)** | Numero di richieste consentite in un&#39;ora per provider. |

{style=&quot;table-layout:auto&quot;}

## Identità supportate {#supported-identities}

[!DNL Verizon Media] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (E-mail, GAID, IDFA) utilizzati nella destinazione Verizon Media. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casi di utilizzo {#use-cases}

[!DNL DataX] Sono disponibili API per gli inserzionisti che desiderano eseguire il targeting di un gruppo di pubblico specifico basato su indirizzi e-mail in [!DNL Verizon Media] (VMG) può creare rapidamente un nuovo segmento e inviare il gruppo di pubblico desiderato tramite l’API in tempo reale di VMG.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

![Scheda di destinazione Yahoo DataX nell’interfaccia utente di Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID MDM]**: Questo è un identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per l’impostazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo [!DNL Yahoo DataX] account manager.  Con gli ID MDM, i dati possono essere limitati per l&#39;uso solo con un certo set di utenti esclusivi (come i dati di prime parti per gli inserzionisti).

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti in una destinazione](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico nelle destinazioni.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta la sezione [!DNL Yahoo/Verizon Media] [documentazione [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
