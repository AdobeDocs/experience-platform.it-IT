---
title: Integrazione Verizon MediaYahoo DataX
description: DataX è un’infrastruttura globale Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i suoi partner esterni in modo sicuro, automatizzato e scalabile.
source-git-commit: 07c8a7afaf6cd2af249ad52eabfbc5f8cd6689ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Verizon Media/Yahoo DataX

## Panoramica {#overview}

DataX è un’infrastruttura globale Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i suoi partner esterni in modo sicuro, automatizzato e scalabile.

>[!IMPORTANT]
>
>Questa pagina di documentazione è stata creata dal team DataX di Verizon Media/Yahoo. Per qualsiasi richiesta di informazioni o aggiornamento, contattali direttamente all&#39;indirizzo [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Prerequisiti {#prerequisites}

**ID MDM**

Questo è un identificatore univoco in Yahoo DataX ed è un campo obbligatorio per l&#39;impostazione delle esportazioni di dati a questa destinazione. Se non conosci questo ID, contatta il tuo account manager Yahoo Data X.

**Limite di velocità**

DataX è limitato in base alla tariffa limite per i limiti di quota per la tassonomia e i post di pubblico descritti nella [documentazione DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Codice di errore | Messaggio di errore | Descrizione |
|---------|----------|---------|
| 429 Troppe richieste | Limite di velocità superato all&#39;ora **(Limite: 100)** | Numero di richieste consentite in un&#39;ora per provider. |

{style=&quot;table-layout:auto&quot;}

**Metadati della tassonomia**

La risorsa Tassonomia definisce un&#39;estensione sulla struttura Metadati Base DataX

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

Ulteriori informazioni su [Metadati tassonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) nella documentazione per gli sviluppatori di DataX.

## Identità supportate {#supported-identities}

Verizon Media supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |

{style=&quot;table-layout:auto&quot;}

## Tipo di esportazione {#export-type}

**Esportazione segmento** : esporta tutti i membri di un segmento (pubblico) con gli identificatori (e-mail) utilizzati nella destinazione Verizon Media.

## Casi d’uso {#use-cases}

Le API DataX sono disponibili per gli inserzionisti che desiderano eseguire il targeting di un gruppo di pubblico specifico tenuto fuori dagli indirizzi e-mail in Verizon Media (VMG) possono creare rapidamente un nuovo segmento e inviare il gruppo di pubblico desiderato utilizzando l&#39;API in tempo quasi reale di VMG.

## Connetti alla destinazione {#connect}

![Scheda di destinazione Yahoo DataX nell’interfaccia utente di Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** MDM: Questo è un identificatore univoco in Yahoo DataX ed è un campo obbligatorio per l&#39;impostazione delle esportazioni di dati a questa destinazione. Se non conosci questo ID, contatta il tuo account manager Yahoo Data X.  Con gli ID MDM, i dati possono essere limitati per l&#39;uso solo con un certo set di utenti esclusivi (come i dati di prime parti per gli inserzionisti).

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attivare profili e segmenti in una destinazione](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull&#39;attivazione dei segmenti di pubblico nelle destinazioni.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, consulta la documentazione di Yahoo/Verizon Media [su DataX](https://developer.verizonmedia.com/datax/guide/).