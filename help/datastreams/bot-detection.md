---
title: Configurare il rilevamento di bot per gli stream di dati
description: Scopri come configurare il rilevamento di bot per i flussi di dati, per differenziare il traffico umano e non umano.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 0787876d80e308c1687304ace7538a51d9a754ff
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 1%

---

# Configurare il rilevamento di bot per gli stream di dati

Il traffico non umano proveniente da programmi automatizzati, web scraper, spider e scanner scriptati può rendere difficile identificare gli eventi provenienti dai visitatori umani. Questo tipo di traffico può influenzare negativamente importanti metriche aziendali, portando a rapporti di traffico errati.

Il rilevamento dei bot consente di identificare gli eventi generati da [Web SDK](/help/collection/js/js-overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) e [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/api/) come generati da spider e bot noti.

>[!NOTE]
>
>Utilizza [!DNL Bot Detection Service] per identificare e filtrare il traffico non umano (bot) dai tuoi dati. Questo riduce il rumore nei set di dati raccolti e consente di garantire che le analisi e i rapporti riflettano le interazioni effettive degli utenti.

Configurando il rilevamento di bot per gli stream di dati, puoi identificare indirizzi IP, intervalli IP e intestazioni di richiesta specifici da classificare come eventi bot. Questo consente di fornire una misurazione più accurata dell’attività dell’utente sul sito o sull’app mobile.

Quando una richiesta ad Edge Network corrisponde a una qualsiasi delle regole di rilevamento di bot, lo schema XDM viene aggiornato con un punteggio bot (sempre impostato su 1), come illustrato di seguito:

```json
{
  "botDetection": {
    "score": 1
  }
}
```

Questo punteggio bot consente alle soluzioni che ricevono la richiesta di identificare correttamente il traffico da bot.

>[!IMPORTANT]
>
>Il rilevamento dei bot non elimina alcuna richiesta di bot. Aggiorna lo schema XDM solo con il punteggio bot e inoltra l&#39;evento al servizio [datastream](configure.md) configurato.
>
>Le soluzioni Adobe possono gestire il punteggio bot in diversi modi. Adobe Analytics, ad esempio, utilizza il proprio [servizio di filtro bot](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html?lang=it) e non utilizza il punteggio impostato da Edge Network. I due servizi utilizzano lo stesso [elenco di bot IAB](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), pertanto il punteggio bot è identico.

## Considerazioni tecniche {#technical-considerations}

Prima di abilitare il rilevamento di bot sui flussi di dati, ecco alcuni punti chiave da tenere a mente per garantire risultati accurati e un’implementazione fluida:

* Il rilevamento dei bot si applica solo alle richieste non autenticate inviate a `edge.adobedc.net`.
* Authenticated requests sent to `server.adobedc.net` are not evaluated for bot traffic, as authenticated traffic is considered trustworthy.
* Bot detection rules can take up to 15 minutes to propagate across the Edge Network after being created.

## Prerequisiti {#prerequisites}

For bot detection to work on your datastream, you must add the **[[!UICONTROL [Bot Detection Information]]](../xdm/field-groups/event/bot-detection-information.md)** field group to your schema. See the [XDM schema](../xdm/ui/resources/schemas.md#add-field-groups) documentation to learn how to add field groups to a schema.

## Configurare il rilevamento di bot per gli stream di dati {#configure}

You can configure bot detection after creating a datastream configuration. See the documentation on how to [create and configure a datastream](configure.md), then follow the instructions below to add bot detection capabilities to your datastream.

Go to the datastreams list and select the datastream to which you want to add bot detection.

![Datastreams user interface showing the list of datastreams.](assets/bot-detection/datastream-list.png)

In the datastream details page, select the **[!UICONTROL Bot Detection]** option on the right rail.

![Bot detection option highlighted in the datastreams user interface.](assets/bot-detection/bot-detection.png)

The **[!UICONTROL Bot Detection Rules]** page is shown.

![Bot detection settings in the datastream settings page.](assets/bot-detection/bot-detection-page.png)

From the Bot Detection Rules page, you can configure bot detection by using the following functionalities:

* Using the [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/).
* Creating your own bot detection rules.

### Use the IAB/ABC International Spiders and Bots List {#iab-list}

The [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) is a third-party, industry-standard list of internet spiders and bots. This list helps you identify automated traffic such as search engine crawlers, monitoring tools, and other nonhuman traffic that you may not want to include in your analytics counts.

To configure your datastream to use the IAB/ABC International Spiders and Bots List:

1. Toggle the **[!UICONTROL Use IAB/ABC International Spiders and Bots List for bot detection on this datastream]** option.
2. Select **[!UICONTROL Save]** to apply the bot detection settings to your datastream.

![IAB spiders and bot list enabled.](assets/bot-detection/bot-detection-list.png)

### Create bot detection rules {#rules}

In addition to using the [IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/), you can define your own bot detection rules for each datastream.

Puoi creare regole di rilevamento bot in base a **indirizzi IP** e **intervalli di indirizzi IP**.

Se hai bisogno di regole di rilevamento bot più granulari, puoi combinare le condizioni IP con le condizioni dell’intestazione della richiesta. Le regole di rilevamento dei bot possono utilizzare le intestazioni seguenti:

| Intestazione HTTP | Descrizione |
| --- | --- |
| `user-agent` | Intestazione che consente ai server e ai peer di rete di identificare l&#39;applicazione, il sistema operativo, il fornitore e/o la versione dell&#39;agente utente richiedente. |
| `content-type` | Indica il tipo di file multimediale originale della risorsa (prima di qualsiasi codifica di contenuto applicata per l’invio). |
| `referer` | Identifica l’indirizzo della pagina web da cui è stata richiesta la risorsa. |
| `sec-ch-ua` | Fornisce il brand e la versione significativa per ogni brand associato al browser in un elenco separato da virgole. |
| `sec-ch-ua-mobile` | Indica se il browser si trova su un dispositivo mobile. Può essere utilizzato anche da un browser desktop per indicare una preferenza per un’esperienza di utilizzo mobile. |
| `sec-ch-ua-platform` | Fornisce la piattaforma o il sistema operativo su cui è in esecuzione l&#39;agente utente. Ad esempio: &quot;Windows&quot; o &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | Fornisce la versione del sistema operativo in cui è in esecuzione l&#39;agente utente. |
| `sec-ch-ua-arch` | Fornisce l&#39;architettura CPU sottostante dell&#39;agente utente, ad esempio ARM o x86. |
| `sec-ch-ua-model` | Indica il modello di dispositivo su cui è in esecuzione il browser. |
| `sec-ch-ua-bitness` | Fornisce il &quot;bit&quot; dell’architettura CPU sottostante dell’agente utente. Dimensione in bit di un numero intero o di un indirizzo di memoria, in genere 64 o 32 bit. |
| `sec-ch-ua-wow64` | Indica se un file binario dell&#39;agente utente è in esecuzione in modalità a 32 bit in Windows a 64 bit. |

Per creare una regola di rilevamento bot, effettua le seguenti operazioni:

1. Seleziona **[!UICONTROL Add New Rule]**.

   ![Schermata delle impostazioni di rilevamento bot con il pulsante Aggiungi nuova regola evidenziato.](assets/bot-detection/bot-detection-new-rule.png)

2. Digitare un nome per la regola nel campo **[!UICONTROL Rule Name]**.

   ![Schermata delle regole di rilevamento bot con il nome della regola evidenziato.](assets/bot-detection/rule-name.png)

3. Selezionare **[!UICONTROL Add new IP condition]** per aggiungere una nuova regola basata su IP. È possibile definire la regola in base all’indirizzo IP o all’intervallo di indirizzi IP.

   ![Schermata delle regole di rilevamento bot con il campo dell&#39;indirizzo IP evidenziato.](assets/bot-detection/ip-address-rule.png)

   ![Schermata delle regole di rilevamento bot con il campo dell&#39;intervallo IP evidenziato.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >Le condizioni IP si basano su un&#39;operazione logica `OR`. Una richiesta è contrassegnata come proveniente da un bot se corrisponde a una qualsiasi delle condizioni IP definite.

4. Se si desidera aggiungere condizioni di intestazione alla regola, selezionare **[!UICONTROL Add header conditions group]**, quindi selezionare le intestazioni da utilizzare per la regola.

   ![Schermata delle regole di rilevamento bot con le condizioni di intestazione evidenziate.](assets/bot-detection/header-conditions.png)

   Quindi, aggiungi le condizioni da utilizzare per l’intestazione selezionata.

   ![Schermata delle regole di rilevamento bot con le condizioni di intestazione evidenziate.](assets/bot-detection/header-condition-rule.png)

5. Dopo aver configurato le regole di rilevamento bot desiderate, seleziona **[!UICONTROL Save]** per applicare le regole allo stream di dati.

   ![Schermata delle regole di rilevamento bot con le condizioni di intestazione evidenziate.](assets/bot-detection/bot-detection-save.png)


## Esempi di regole di rilevamento bot {#examples}

Per aiutarti a iniziare a rilevare i bot, puoi utilizzare gli esempi dettagliati di seguito per creare le regole di rilevamento dei bot.

### Rilevamento bot basato su un indirizzo IP {#one-ip}

Per contrassegnare tutte le richieste provenienti da un indirizzo IP specifico come traffico da bot, crea una nuova regola di rilevamento bot che valuti un singolo indirizzo IP, come illustrato nell’immagine seguente.

![Regola di rilevamento bot basata su un indirizzo IP.](assets/bot-detection/bot-detection-one-ip.png)

### Rilevamento dei bot basato su due indirizzi IP {#two-ip}

Per contrassegnare tutte le richieste provenienti da uno di due indirizzi IP specifici come traffico da bot, crea una nuova regola di rilevamento bot che valuta due indirizzi IP, come illustrato nell’immagine seguente.

![Regola di rilevamento bot basata su due indirizzi IP.](assets/bot-detection/bot-detection-two-ips.png)

### Rilevamento di bot basato su un intervallo di indirizzi IP {#range}

Per contrassegnare tutte le richieste provenienti da qualsiasi indirizzo IP in un intervallo specifico come traffico da bot, crea una nuova regola di rilevamento bot che valuti un intero intervallo di indirizzi IP, come illustrato nell’immagine seguente.

![Regola di rilevamento bot basata sull&#39;intervallo IP.](assets/bot-detection/bot-detection-range.png)

### Rilevamento di bot basato su un indirizzo IP e un’intestazione di richiesta {#ip-header}

Per contrassegnare come traffico bot tutte le richieste provenienti da un indirizzo IP specifico e contenenti un’intestazione di richiesta specifica, crea una nuova regola di rilevamento bot, come illustrato nell’immagine seguente.

Questa regola controlla se la richiesta proviene da un indirizzo IP specifico e se l&#39;intestazione della richiesta `referer` inizia con `www.adobe.com`.

![Regola di rilevamento bot basata sull&#39;indirizzo IP e sull&#39;intestazione della richiesta.](assets/bot-detection/bot-detection-header-ip.png)

### Rilevamento dei bot in base a più condizioni {#multiple-conditions}

Puoi creare regole di rilevamento bot in base a:

* **Condizioni diverse multiple**: condizioni diverse vengono valutate come un&#39;operazione logica `AND`, il che significa che le condizioni devono essere soddisfatte simultaneamente affinché la richiesta possa essere identificata come proveniente da un bot.
* **Condizioni multiple dello stesso tipo**: le condizioni dello stesso tipo vengono valutate come un&#39;operazione `OR` logica, il che significa che se una qualsiasi delle condizioni viene soddisfatta, la richiesta viene identificata come proveniente da un bot.

La regola mostrata nell’immagine seguente identifica una richiesta di origine da bot se sono soddisfatte le seguenti condizioni:

La richiesta proviene da uno dei due indirizzi IP, l&#39;intestazione `referer` inizia con `www.adobe.com` e l&#39;intestazione `sec-ch-ua-mobile` identifica la richiesta come proveniente da un browser desktop.

![Regola di rilevamento bot basata su più condizioni.](assets/bot-detection/bot-detection-multiple.png)
