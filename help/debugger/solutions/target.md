---
title: Testare un’implementazione di Adobe Target con Adobe Experience Platform Debugger
description: Scopri come utilizzare Adobe Experience Platform Debugger per testare ed eseguire il debug di un sito web abilitato con Adobe Target.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Testare un’implementazione di Adobe Target con Adobe Experience Platform Debugger

Adobe Experience Platform Debugger fornisce una suite di strumenti utili per testare e eseguire il debug di un sito web che è stato dotato di un’implementazione Adobe Target. Questa guida descrive alcuni flussi di lavoro comuni e best practice per l’utilizzo di Experience Platform Debugger su un sito web abilitato per Target.

## Prerequisiti

Per utilizzare Experience Platform Debugger per Target, il sito Web deve utilizzare la [libreria at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versione 1.x o successiva. Le versioni precedenti non sono supportate.

## Inizializzazione di Experience Platform Debugger

Apri il sito web da testare in un browser, quindi apri l’estensione Experience Platform Debugger.

Selezionare **[!DNL Target]** nel menu di navigazione a sinistra. Se Experience Platform Debugger rileva che sul sito è in esecuzione una versione compatibile di at.js, vengono visualizzati i dettagli di implementazione di Adobe Target.

![Visualizzazione di destinazione selezionata in Experience Platform Debugger, che indica che Adobe Target è attivo nella pagina del browser attualmente visualizzata](../images/solutions/target/target-initialized.png)

## Informazioni di configurazione globali

Le informazioni sulla configurazione globale dell’implementazione vengono visualizzate nella parte superiore della vista Target in Experience Platform Debugger.

![Informazioni di configurazione globali per Target evidenziate in Experience Platform Debugger](../images/solutions/target/global-config.png)

| Nome | Descrizione |
| --- | --- |
| Codice client | Un ID univoco che identifica la tua organizzazione. |
| Versione | Versione della libreria di Adobe Target attualmente installata sul sito web. |
| Nome richiesta globale | Il nome dell&#39;[mbox globale](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) per l&#39;implementazione di Target. Il nome predefinito è `target-global-mbox`. |
| Evento caricamento pagina | Valore booleano che indica se si è verificato un [evento di caricamento pagina](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams). Gli eventi di caricamento pagina sono supportati solo per at.js 2.x. Per le versioni non compatibili, il valore predefinito è `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Selezionare **[!DNL Network Requests]** per visualizzare informazioni di riepilogo su ogni richiesta di rete effettuata nella pagina.

![La sezione [!DNL Network Requests] per Target selezionata in Experience Platform Debugger](../images/solutions/target/network-requests.png)

Quando esegui azioni sulla pagina (compreso il ricaricamento della pagina), vengono aggiunte automaticamente nuove colonne alla tabella, che ti consentono di visualizzare la sequenza delle azioni e il modo in cui i valori vengono modificati tra ogni richiesta.

![La sezione [!DNL Network Requests] per Target selezionata in Experience Platform Debugger](../images/solutions/target/new-request.png)

Vengono acquisiti i seguenti valori:

| Nome | Descrizione |
| --- | --- |
| [!DNL Page Title] | Titolo della pagina che ha avviato la richiesta. |
| [!DNL Page URL] | URL della pagina che ha avviato la richiesta. |
| [!DNL URL] | L’URL non elaborato della richiesta. |
| [!DNL Method] | Il metodo HTTP per la richiesta. |
| [!DNL Query String] | Stringa di query della richiesta, tratta dall’URL. |
| [!DNL POST Body] | Corpo della richiesta (impostato solo per le richieste POST). |
| [!DNL Pathname] | Il percorso dell’URL della richiesta. |
| [!DNL Hostname] | Il nome host dell’URL della richiesta. |
| [!DNL Domain] | Dominio dell’URL della richiesta. |
| [!DNL Timestamp] | Una marca temporale di quando si è verificata la richiesta (o l’evento), entro il fuso orario del browser. |
| [!DNL Time Since Page Load] | Tempo trascorso dal caricamento iniziale della pagina al momento della richiesta. |
| [!DNL Initiator] | Iniziatore della richiesta. In altre parole, chi ha presentato la richiesta? |
| [!DNL clientCode] | L’identificatore dell’account della tua organizzazione come riconosciuto da Target. |
| [!DNL requestType] | API utilizzata per la richiesta. Se utilizzi at.js 1.x, il valore è `/json`. Se utilizzi at.js 2.x, il valore è `delivery`. |
| [!DNL Audience Manager Blob] | Fornisce informazioni sui metadati Audience Manager crittografati denominati BLOB. |
| [!DNL Audience Location Hint] | L&#39;ID della regione di raccolta dati. Questo è un identificatore numerico per la posizione geografica di un particolare datacenter del servizio ID. Per ulteriori informazioni, consulta la documentazione di Audience Manager su [ID regioni DCS, posizioni e nomi host](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=it) e la guida del servizio Experience Cloud Identity in [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=it#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | Altezza del browser in pixel. |
| [!DNL Browser Time Offset] | Offset orario del browser associato al relativo fuso orario. |
| [!DNL Browser Width] | Larghezza del browser in pixel. |
| [!DNL Color Depth] | Profondità colore dello schermo. |
| [!DNL context] | Oggetto che contiene informazioni contestuali sul browser utilizzato per effettuare la richiesta, incluse le dimensioni dello schermo e la piattaforma client. |
| [!DNL prefetch] | Parametri utilizzati in durante l&#39;elaborazione di `prefetch`. |
| [!DNL execute] | Parametri utilizzati durante l&#39;elaborazione di `execute`. |
| [!DNL Experience Cloud Visitor ID] | Se ne viene rilevato uno, fornisce informazioni sull&#39;[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) assegnato al visitatore del sito corrente. |
| [!DNL experienceCloud] | Contiene gli Experience Cloud ID per questa sessione utente specifica: un A4T [ID dati supplementare](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?lang=it&#section_2C1F745A2B7D41FE9E30915539226E3A) e un [ID visitatore (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it). |
| [!DNL id] | [ID destinazione](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) per il visitatore. |
| [!DNL Mbox Host] | L&#39;[host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=it) a cui è stata effettuata la richiesta di Target. |
| [!DNL Mbox PC] | Stringa che incapsula l&#39;ID sessione [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) e l&#39;hint percorso [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=it#concept_0AE2ED8E9DE64288A8B30FCBF1040934). Questo valore viene utilizzato da at.js per garantire che la sessione e la posizione di Edge rimangano permanenti. |
| [!DNL Mbox Referrer] | URL referrer per la richiesta [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) specifica. |
| [!DNL Mbox URL] | URL del server [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL Mbox Version] | Versione di [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) in uso. |
| [!DNL mbox3rdPartyId] | [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=it) assegnato al visitatore corrente. |
| [!DNL mboxRid] | ID della richiesta [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL requestId] | Un ID univoco per la richiesta. |
| [!DNL Screen Height] | Altezza dello schermo in pixel. |
| [!DNL Screen Width] | Larghezza dello schermo in pixel. |
| [!DNL Supplemental Data ID] | ID generato dal sistema e utilizzato per associare i visitatori alle chiamate corrispondenti di Adobe Target e Adobe Analytics. Per ulteriori informazioni, vedere la [Guida alla risoluzione dei problemi di A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?lang=it&#section_75002584FA63456D8D9086172925DD8D). |
| [!DNL vst] | Configurazione dell&#39;API del servizio [Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html?lang=it). |
| [!DNL webGLRenderer] | Fornisce informazioni sul renderer WebGL utilizzato nella pagina, se applicabile. |

{style="table-layout:auto"}

Per visualizzare i dettagli di un parametro in un particolare evento di rete, selezionare la cella della tabella in questione. Viene visualizzata una finestra a comparsa che fornisce ulteriori informazioni sul parametro, inclusa una descrizione e il relativo valore. Se il valore è un oggetto JSON, la finestra di dialogo include una visualizzazione completamente navigabile della struttura dell’oggetto.

![La sezione [!DNL Network Requests] per Target selezionata in Experience Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Selezionare **[!DNL Configuration]** per abilitare o disabilitare una selezione di strumenti di debug aggiuntivi per Target.

![La sezione [!DNL Configuration Requests] per Target selezionata in Experience Platform Debugger](../images/solutions/target/configuration.png)

| Strumento di debug | Descrizione |
| --- | --- |
| [!DNL Target Console Logging] | Quando è abilitata, ti consente di accedere ai registri at.js nella scheda della console del browser. Questa funzionalità può essere abilitata anche aggiungendo un parametro di query `mboxDebug` (con qualsiasi valore) all&#39;URL del browser. |
| [!DNL Target Disable] | Quando è abilitata, tutte le funzionalità di Target sono disabilitate sulla pagina. Questa può essere utilizzata per determinare se l’origine del problema sulla pagina è un’offerta specifica di Target. |
| [!DNL Target Trace] | **Nota**: per abilitare questa funzione è necessario aver effettuato l&#39;accesso.<br><br>Se questa opzione è attivata, i token di tracciamento vengono inviati con ogni richiesta e in ogni risposta viene restituito un oggetto di traccia. `at.js` analizza la risposta `window.__targetTraces`. Ogni oggetto trace contiene le stesse informazioni della scheda [[!DNL Network Requests]], con le seguenti aggiunte:<ul><li>Uno snapshot del profilo, che consente di visualizzare gli attributi prima e dopo le richieste.</li><li>[attività](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=it) corrispondenti e senza corrispondenza, che indica il motivo per cui il profilo corrente è idoneo o meno per attività specifiche.<ul><li>Questo può aiutare a identificare i tipi di pubblico per cui un profilo si qualifica in un dato punto e perché.</li><li>I documenti di Target contengono ulteriori informazioni su diversi tipi di attività</li></ul></li></ul> |

{style="table-layout:auto"}
