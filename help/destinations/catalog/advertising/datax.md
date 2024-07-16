---
title: Connessione Verizon MediaYahoo DataX
description: DataX è un’infrastruttura aggregata Verizon Media/Yahoo che ospita vari componenti che consentono a Verizon Media/Yahoo di scambiare dati con i propri partner esterni in modo sicuro, automatizzato e scalabile.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 3%

---

# Connessione [!DNL Verizon Media/Yahoo DataX]

## Panoramica {#overview}

[!DNL DataX] è un&#39;infrastruttura [!DNL Verizon Media/Yahoo] aggregata che ospita vari componenti che consentono a [!DNL Verizon Media/Yahoo] di scambiare dati con i propri partner esterni in modo sicuro, automatizzato e scalabile.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL DataX] di [!DNL Verizon Media/Yahoo]. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## Prerequisiti {#prerequisites}

**ID MDM**

Questo è un identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per la configurazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo account manager [!DNL Yahoo DataX].

**Metadati di tassonomia**

La risorsa di tassonomia definisce un&#39;estensione sulla struttura metadati di base [!DNL DataX]

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

Ulteriori informazioni su [Metadati di tassonomia](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) nella documentazione per gli sviluppatori di [!DNL DataX].

## Limiti di velocità e protezioni {#rate-limits-guardrails}

>[!IMPORTANT]
>
>Quando si attivano più di 100 tipi di pubblico in [!DNL Verizon Media/Yahoo DataX], è possibile che dalla destinazione vengano visualizzati errori di limitazione della frequenza. Quando attivi i tipi di pubblico in questa destinazione, prova ad attivare meno di 100 tipi di pubblico in un unico flusso di dati di attivazione. Se devi attivare più segmenti, crea una nuova destinazione sullo stesso account.

[!DNL DataX] è limitato dalla tariffa in base ai limiti di quota per la tassonomia e i post del pubblico descritti nella [documentazione di DataX](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| Codice di errore | Messaggio di errore | Descrizione |
|---------|----------|---------|
| 429 Troppe richieste | Limite di velocità superato all&#39;ora **(Limite: 100)** | Numero di richieste consentite in un’ora per provider. |

{style="table-layout:auto"}

## Identità supportate {#supported-identities}

[!DNL Verizon Media] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (E-mail, GAID, IDFA) utilizzati nella destinazione Verizon Media. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi d’uso {#use-cases}

Le API [!DNL DataX] sono disponibili per gli inserzionisti che desiderano indirizzare un gruppo di pubblico specifico ricavato dagli indirizzi e-mail in [!DNL Verizon Media] (VMG) possono creare rapidamente un nuovo pubblico e inviare il gruppo di pubblico desiderato utilizzando l&#39;API quasi in tempo reale di VMG.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

![Scheda di destinazione Yahoo DataX nell&#39;interfaccia utente di Platform](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID MDM]**: si tratta di un identificatore univoco in [!DNL Yahoo DataX] ed è un campo obbligatorio per la configurazione delle esportazioni di dati verso questa destinazione. Se non conosci questo ID, contatta il tuo account manager [!DNL Yahoo DataX].  Con gli ID MDM, l’uso dei dati può essere limitato solo a un determinato insieme di utenti esclusivi (come i dati di prime parti per gli inserzionisti).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico in una destinazione](../../ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione di tipi di pubblico nelle destinazioni.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, leggere la [!DNL Yahoo/Verizon Media] [documentazione in data [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
