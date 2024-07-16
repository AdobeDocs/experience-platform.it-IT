---
keywords: pubblicità; criteri;
title: Connessione critica
description: Criteo potenzia la pubblicità di fiducia e di impatto per offrire esperienze più ricche a ogni consumatore attraverso l'internet aperto. Con il set di dati di e-commerce più grande al mondo e l’intelligenza artificiale migliore della classe, Criteo assicura che ogni punto di contatto nel percorso sia personalizzato per raggiungere i clienti con l’annuncio giusto, al momento giusto.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# (Beta) Connessione critica

## Panoramica {#overview}

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da Criteo. Attualmente si tratta di un prodotto beta la cui funzionalità è soggetta a modifiche. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Criteo [qui](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo potenzia la pubblicità di fiducia e di impatto per offrire esperienze più ricche a ogni consumatore attraverso l&#39;internet aperto. Con il set di dati di e-commerce più grande al mondo e l’intelligenza artificiale migliore della classe, Criteo assicura che ogni punto di contatto nel percorso sia personalizzato per raggiungere i clienti con l’annuncio giusto, al momento giusto.

## Prerequisiti {#prerequisites}

* È necessario disporre di un account utente amministratore in [Centro gestione criteri](https://marketing.criteo.com).
* Avrai bisogno del tuo ID Criteo Advertiser (chiedi al tuo contatto Criteo se non hai questo ID).
* È necessario fornire [!DNL GUM caller ID], nel caso si desideri utilizzare [!DNL GUM ID] come identificatore.

## Limitazioni {#limitations}

* Criteo accetta solo e-mail con hash e testo normale di [!DNL SHA-256] (da trasformare in [!DNL SHA-256] prima dell&#39;invio). Non inviare dati PII (informazioni personali identificabili, come nomi o numeri di telefono di persone).
* Il criterio richiede almeno un identificatore che deve essere fornito dal client. Dà priorità a [!DNL GUM ID] come identificatore rispetto all&#39;e-mail con hash in quanto contribuisce a un tasso di corrispondenza migliore.

![Prerequisiti](../../assets/catalog/advertising/criteo/prerequisites.png)

## Identità supportate {#supported-identities}

Il criterio supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
| --- | --- | --- |
| `email_sha256` | Indirizzi e-mail con hash con algoritmo SHA-256 | Gli indirizzi e-mail con hash SHA-256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, seleziona l&#39;opzione [!UICONTROL Applica trasformazione] per fare in modo che Platform esegua automaticamente l&#39;hash dei dati all&#39;attivazione. |
| `gum_id` | Identificatore cookie [!DNL GUM] criterio | [!DNL GUM IDs] consente ai client di mantenere una corrispondenza tra il proprio sistema di identificazione utente e l&#39;identificazione utente di Criteo ([!DNL UID]). Se il tipo di identificatore è `gum_id`, è necessario includere anche un parametro aggiuntivo, [!DNL GUM Caller ID]. Rivolgiti al team del tuo account Criteo per [!DNL GUM Caller ID] appropriato o per ottenere ulteriori informazioni su questa sincronizzazione di [!DNL GUM ID], se necessario. |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| --- | --- | --- |
| Tipo di esportazione | Esportazione pubblico | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL Criteo]. |
| Frequenza di esportazione | Streaming | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](../../destination-types.md#streaming-destinations). |

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come utilizzare la destinazione [!DNL Criteo], ecco alcuni obiettivi che i clienti Adobe Experience Platform possono raggiungere con [!DNL Criteo]:

### Caso d&#39;uso 1: recupero del traffico

Presenta la tua azienda con offerte di prodotti pertinenti e creatività flessibile. Con consigli sui prodotti intelligenti, gli annunci presenteranno automaticamente i prodotti che hanno più probabilità di attivare visite e coinvolgimento. Il targeting flessibile ti consente di creare tipi di pubblico dal set di dati di e-commerce di Criteo o dai tuoi elenchi di potenziali clienti e dai segmenti CDP di Adobe.

### Caso d’uso 2: aumentare le conversioni dei siti web

Quando i visitatori lasciano il tuo sito web, ricorda loro cosa non riescono a fare con annunci di retargeting che aumentano le conversioni mostrando offerte speciali e offerte iperrilevanti, ovunque vadano dopo. Connetti il tuo pubblico Adobe di CDP per coinvolgere nuovamente i clienti esistenti o rivolgerti ai consumatori in modo simile ai tuoi acquirenti più fedeli.

## Connetti a criterio {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autentica su criterio

I passaggi per la connessione sono i seguenti:

1. Accedi a Adobe Experience Platform e connettiti alla destinazione critica.

   ![Accesso](../../assets/catalog/advertising/criteo/connect-destination.png)

1. Verrai reindirizzato a Criteo per autorizzare la connessione. Potrebbe essere necessario accedere prima con le credenziali Criteo:

   ![Accesso a Criteo](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Accesso a Criteo](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Accesso a Criteo](../../assets/catalog/advertising/criteo/log-in-3.png)


### Parametri di connessione {#connection-parameters}

Dopo l’autenticazione nella destinazione, compila i seguenti parametri di connessione.

![Parametri di connessione](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Campo | Descrizione | Obbligatorio |
| --- | --- | --- |
| Nome | Un nome per aiutarti a riconoscere questa destinazione in futuro. Il nome scelto sarà il nome [!DNL Audience] in Criteo Management Center e non potrà essere modificato in un secondo momento. | Sì |
| Descrizione | Una descrizione per identificare questa destinazione in futuro. | No |
| ID inserzionista | ID inserzionista del criterio dell’organizzazione. Per maggiori informazioni, contatta il tuo account manager Criteo. | Sì |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] della tua organizzazione. Rivolgiti al team del tuo account Criteo per [!DNL GUM Caller ID] appropriato o per ottenere ulteriori informazioni su questa sincronizzazione di [!DNL GUM], se necessario. | Sì, ogni volta che [!DNL GUM ID] viene fornito come identificatore |

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate-segments}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](../../ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Dati esportati {#exported-data}

Puoi visualizzare i tipi di pubblico esportati nel [Centro gestione criteri](https://marketing.criteo.com/audience-manager/dashboard).

Il corpo della richiesta di aggiunta di un profilo utente ricevuto dalla connessione [!DNL Criteo] è simile al seguente:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

Il corpo della richiesta di rimozione del profilo utente ricevuto dalla connessione [!DNL Criteo] è simile al seguente:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Utilizzo dei dati e governance {#data-usage}

Tutte le destinazioni Adobe Experience Platform sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come Adobe Experience Platform applica la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive

* [Centro assistenza Criteo](https://help.criteo.com/kb/en)
* [Portale per sviluppatori Criteo](https://developers.criteo.com)
