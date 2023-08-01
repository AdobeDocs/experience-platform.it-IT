---
title: Connessione Verizon MediaYahoo DataX
description: DataX è un’infrastruttura aggregata Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i propri partner esterni in modo sicuro, automatizzato e scalabile.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] connessione

## Panoramica {#overview}

[!DNL DataX] è un aggregato [!DNL Verizon Media/Yahoo] infrastruttura che ospita vari componenti che consentono [!DNL Verizon Media/Yahoo] scambiare dati con i propri partner esterni in modo sicuro, automatizzato e scalabile.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da [!DNL Verizon Media/Yahoo]di [!DNL DataX] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Prerequisiti {#prerequisites}

**ID MDM**

Identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per la configurazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo [!DNL Yahoo DataX] responsabile dell’account.

**Metadati di tassonomia**

La risorsa Tassonomia definisce un’estensione sulla base [!DNL DataX] Struttura dei metadati

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

Ulteriori informazioni su [Metadati tassonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) nel [!DNL DataX] documentazione per gli sviluppatori.

## Limiti di velocità e protezioni {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Quando si attivano più di 100 tipi di pubblico in [!DNL Verizon Media/Yahoo DataX], dalla destinazione potrebbero venire visualizzati errori di limitazione della frequenza. Quando attivi i tipi di pubblico in questa destinazione, prova ad attivare meno di 100 tipi di pubblico in un unico flusso di dati di attivazione. Se devi attivare più segmenti, crea una nuova destinazione sullo stesso account.

[!DNL DataX] è limitato dalla tariffa in base ai limiti di quota per i posti di tassonomia e pubblico descritti nella [Documentazione di DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Codice di errore | Messaggio di errore | Descrizione |
|---------|----------|---------|
| 429 Troppe richieste | Limite tariffa superato all&#39;ora **(Limite: 100)** | Numero di richieste consentite in un’ora per provider. |

{style="table-layout:auto"}

## Identità supportate {#supported-identities}

[!DNL Verizon Media] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (E-mail, GAID, IDFA) utilizzati nella destinazione Verizon Media. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi di utilizzo {#use-cases}

[!DNL DataX] Le API sono disponibili per gli inserzionisti che desiderano indirizzare un gruppo di pubblico specifico ricavato dagli indirizzi e-mail in [!DNL Verizon Media] (VMG) può creare rapidamente un nuovo pubblico e inviare messaggi push al gruppo di pubblico desiderato utilizzando l’API quasi in tempo reale di VMG.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

![Scheda di destinazione Yahoo DataX nell’interfaccia utente di Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID MDM]**: identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per la configurazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo [!DNL Yahoo DataX] responsabile dell’account.  Con gli ID MDM, l’uso dei dati può essere limitato solo a un determinato insieme di utenti esclusivi (come i dati di prime parti per gli inserzionisti).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e pubblico in una destinazione](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico nelle destinazioni.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, leggere [!DNL Yahoo/Verizon Media] [documentazione su [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
