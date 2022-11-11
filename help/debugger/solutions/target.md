---
title: Test di un’implementazione Adobe Target con Adobe Experience Platform Debugger
description: Scopri come utilizzare Adobe Experience Platform Debugger per testare ed eseguire il debug di un sito web abilitato con Adobe Target.
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 5%

---

# Test di un&#39;implementazione Adobe Target con Adobe Experience Platform Debugger

Adobe Experience Platform Debugger fornisce una suite di strumenti utili per testare e eseguire il debug di un sito web dotato di strumenti di implementazione Adobe Target. Questa guida descrive alcuni flussi di lavoro comuni e best practice per l’utilizzo di Platform Debugger su un sito web abilitato per Target.

## Prerequisiti

Per utilizzare Platform Debugger per Target, il sito web deve utilizzare il [libreria at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versione 1.x o successiva. Le versioni precedenti non sono supportate.

## Inizializzazione di Platform Debugger

Apri il sito web da testare in un browser, quindi apri l’estensione Platform Debugger.

Seleziona **[!DNL Target]** nella navigazione a sinistra. Se Platform Debugger rileva che sul sito è in esecuzione una versione compatibile di at.js, vengono visualizzati i dettagli dell’implementazione di Adobe Target.

![Vista Target selezionata in Platform Debugger, che indica che Adobe Target è attivo nella pagina del browser attualmente visualizzata](../images/solutions/target/target-initialized.png)

## Informazioni sulla configurazione globale

Le informazioni sulla configurazione globale dell’implementazione vengono visualizzate nella parte superiore della vista Target in Platform Debugger.

![Informazioni di configurazione globale per Target evidenziate in Platform Debugger](../images/solutions/target/global-config.png)

| Nome | Descrizione |
| --- | --- |
| Codice client | Un ID univoco che identifica l&#39;organizzazione. |
| Versione | Versione della libreria Adobe Target attualmente installata sul sito web. |
| Nome richiesta globale | Nome della [mbox globale](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) per l’implementazione di Target, il nome predefinito è `target-global-mbox`. |
| Evento caricamento pagina | Un valore booleano che indica se è [evento di caricamento pagina](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) ha avuto luogo. Gli eventi di caricamento pagina sono supportati solo per at.js 2.x. Per le versioni non compatibili, il valore predefinito è `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

Seleziona **[!DNL Network Requests]** per visualizzare informazioni di riepilogo su ogni richiesta di rete effettuata sulla pagina.

![La [!DNL Network Requests] sezione per Target selezionata in Platform Debugger](../images/solutions/target/network-requests.png)

Quando esegui delle azioni sulla pagina (incluso il ricaricamento della pagina), nuove colonne vengono aggiunte automaticamente alla tabella, consentendoti di visualizzare la sequenza di azioni e la modalità di modifica dei valori tra le due richieste.

![La [!DNL Network Requests] sezione per Target selezionata in Platform Debugger](../images/solutions/target/new-request.png)

Vengono acquisiti i seguenti valori:

| Nome | Descrizione |
| --- | --- |
| [!DNL Page Title] | Titolo della pagina che ha avviato la richiesta. |
| [!DNL Page URL] | URL della pagina che ha avviato la richiesta. |
| [!DNL URL] | URL non elaborato della richiesta. |
| [!DNL Method] | Il metodo HTTP per la richiesta. |
| [!DNL Query String] | Stringa di query della richiesta, prelevata dall’URL. |
| [!DNL POST Body] | Il corpo della richiesta (impostato solo per le richieste POST). |
| [!DNL Pathname] | Il percorso dell’URL della richiesta. |
| [!DNL Hostname] | Nome host dell’URL della richiesta. |
| [!DNL Domain] | Dominio dell’URL della richiesta. |
| [!DNL Timestamp] | Una marca temporale di quando si è verificata la richiesta (o l’evento), entro il fuso orario del browser. |
| [!DNL Time Since Page Load] | Tempo trascorso dal caricamento iniziale della pagina al momento della richiesta. |
| [!DNL Initiator] | Iniziatore della richiesta. In altre parole, chi ha fatto la richiesta? |
| [!DNL clientCode] | Identificatore dell&#39;account dell&#39;organizzazione riconosciuto da Target. |
| [!DNL requestType] | API utilizzata per la richiesta. Se utilizzi at.js 1.x, il valore è `/json`. Se utilizzi at.js 2.x, il valore è `delivery`. |
| [!DNL Audience Manager Blob] | Fornisce informazioni sui metadati di Audience Manager crittografati denominati &quot;blob&quot;. |
| [!DNL Audience Location Hint] | L&#39;ID della regione di raccolta dati. Questo è un identificatore numerico per la posizione geografica di un particolare datacenter del servizio ID. Per ulteriori informazioni, consulta la documentazione di Audience Manager su [ID regioni DCS, posizioni e nomi host](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=it) e la guida al servizio Experience Cloud Identity su [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | L’altezza in pixel del browser. |
| [!DNL Browser Time Offset] | Offset temporale del browser associato al relativo fuso orario. |
| [!DNL Browser Width] | Larghezza del browser in pixel. |
| [!DNL Color Depth] | Profondità colore dello schermo. |
| [!DNL context] | Un oggetto che contiene informazioni contestuali sul browser utilizzato per effettuare la richiesta, incluse le dimensioni dello schermo e la piattaforma client. |
| [!DNL prefetch] | I parametri utilizzati in `prefetch` elaborazione. |
| [!DNL execute] | I parametri utilizzati durante `execute` elaborazione. |
| [!DNL Experience Cloud Visitor ID] | Se viene rilevato uno, fornisce informazioni sul [ID Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) viene assegnato al visitatore del sito corrente. |
| [!DNL experienceCloud] | Contiene gli ID Experience Cloud per questa specifica sessione utente: a A4T [ID dati supplementare](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)e [ID visitatore (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | La [ID target](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) per il visitatore. |
| [!DNL Mbox Host] | La [host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) a cui è stata effettuata la richiesta di Target. |
| [!DNL Mbox PC] | Una stringa che incapsula il [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) l&#39;ID della sessione e [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) hint posizione Questo valore viene utilizzato da at.js per garantire che la sessione e la posizione Edge rimangano permanenti. |
| [!DNL Mbox Referrer] | Il referente URL per lo specifico [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) richiesta. |
| [!DNL Mbox URL] | L’URL per [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) server. |
| [!DNL Mbox Version] | Versione di [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) in uso. |
| [!DNL mbox3rdPartyId] | La [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) assegnato al visitatore corrente. |
| [!DNL mboxRid] | La [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) ID richiesta. |
| [!DNL requestId] | Un ID univoco per la richiesta. |
| [!DNL Screen Height] | Altezza dello schermo in pixel. |
| [!DNL Screen Width] | Larghezza dello schermo in pixel. |
| [!DNL Supplemental Data ID] | Un ID generato dal sistema utilizzato per abbinare i visitatori alle corrispondenti chiamate Adobe Target e Adobe Analytics. Consulta la sezione [Guida alla risoluzione dei problemi di A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) per ulteriori informazioni. |
| [!DNL vst] | La [Configurazione API del servizio Experience Cloud Identity](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Fornisce informazioni sul modulo di rendering WebGL utilizzato nella pagina, se applicabile. |

{style=&quot;table-layout:auto&quot;}

Per visualizzare i dettagli di un parametro in un particolare evento di rete, selezionare la cella della tabella in questione. Viene visualizzato un puntatore che fornisce ulteriori informazioni sul parametro, tra cui una descrizione e il relativo valore. Se il valore è un oggetto JSON, la finestra di dialogo include una visualizzazione completamente navigabile della struttura dell’oggetto.

![La [!DNL Network Requests] sezione per Target selezionata in Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Seleziona **[!DNL Configuration]** per abilitare o disabilitare una selezione di strumenti di debug aggiuntivi per Target.

![La [!DNL Configuration Requests] sezione per Target selezionata in Platform Debugger](../images/solutions/target/configuration.png)

| Strumento di debug | Descrizione |
| --- | --- |
| [!DNL Target Console Logging] | Quando abilitato, consente di accedere ai registri di at.js nella scheda console del browser. Puoi abilitare questa funzione anche aggiungendo un’ `mboxDebug` parametro di query (con qualsiasi valore) all’URL del browser. |
| [!DNL Target Diable] | Quando abilitata, tutte le funzionalità di Target sono disabilitate nella pagina. Può essere utilizzato per determinare se un’offerta specifica di Target è la causa del problema sulla pagina. |
| [!DNL Target Trace] | **Nota**: Devi aver effettuato l’accesso per abilitare questa funzione.<br><br>Quando abilitato, i token di tracciamento vengono inviati con ogni richiesta e viene restituito un oggetto trace in ogni risposta. `at.js` analizza la risposta `window.__targetTraces`. Ogni oggetto trace contiene le stesse informazioni di [[!DNL Network Requests] scheda], con le seguenti aggiunte:<ul><li>Un’istantanea di profilo che ti consente di visualizzare gli attributi prima e dopo le richieste.</li><li>Corrispondenza e senza corrispondenza [attività](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), che mostra il motivo per cui il profilo corrente si è qualificato o meno per attività specifiche.<ul><li>Questo può aiutare a identificare i tipi di pubblico per i quali un profilo si qualifica in un dato momento e perché.</li><li>I documenti di Target contengono ulteriori informazioni sui diversi tipi di attività</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
