---
solution: Real-Time Customer Data Platform
title: Utilizzo dei client MCP (Beta)
description: Scopri come collegare Adobe Real-Time CDP ai client MCP utilizzando il server MCP
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2375'
ht-degree: 0%

---

# Utilizzo dei client MCP (Beta) {#rtcdp-mcp}

È possibile utilizzare l’integrazione MCP di Adobe Real-Time CDP per eseguire query su tipi di pubblico, destinazioni e stato di attivazione utilizzando prompt in linguaggio semplice, senza scrivere chiamate API o navigare tra le schermate dei prodotti. Questa pagina spiega come funziona l’integrazione, cosa puoi farci e come iniziare.

>[!AVAILABILITY]
>
>Il server MCP di Real-Time CDP è distribuito come **server di trasporto HTTP remoto** che gli utenti installano e configurano nei client MCP e nelle piattaforme di app supportati (ad esempio Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code). L&#39;autenticazione viene gestita tramite un **flusso di accesso basato su browser**. Quando il client si connette per la prima volta al server, apre il browser predefinito in modo che tu possa accedere con le tue credenziali Adobe e autorizzare l&#39;accesso. Contatta il rappresentante Adobe per accedere a questo programma Beta.

## Beta, sicurezza e note legali {#mcp-notices}

**Avviso di documentazione di Beta:** questa documentazione riguarda una funzionalità di Beta e non costituisce documentazione finale. Il contenuto qui descritto si riferisce a una versione di Beta ed è soggetto a modifiche prima della disponibilità generale. Adobe non fornisce alcuna dichiarazione sulla completezza o sull’accuratezza di questa documentazione.

Utilizzando il server Adobe Real-Time CDP MCP (Beta) (&quot;Beta&quot;), l&#39;utente riconosce che il Beta è fornito **&quot;così com&#39;è&quot; senza alcuna garanzia**. Adobe non ha alcun obbligo di mantenere, correggere, aggiornare, modificare, modificare o supportare in altro modo Beta. Si consiglia di usare cautela e di non fare affidamento in alcun modo sul corretto funzionamento o sulle prestazioni di tale Beta e/o dei materiali di accompagnamento. Beta è considerata un&#39;informazione riservata di Adobe. Qualsiasi &quot;Feedback&quot; (informazioni relative a Beta, compresi, a titolo esemplificativo e non esaustivo, problemi o difetti riscontrati durante l’utilizzo di Beta, suggerimenti, miglioramenti e raccomandazioni) fornito dall’Utente a Adobe viene assegnato ad Adobe, inclusi tutti i diritti, i titoli e gli interessi relativi a tale Feedback.

>[!WARNING]
>
>Il Model Context Protocol (MCP) è uno standard open source emergente e può presentare rischi per la sicurezza o l&#39;affidabilità. Le integrazioni server MCP di Adobe e la relativa documentazione vengono fornite &quot;così come sono&quot;, senza garanzie di alcun tipo.
>
>La connessione di client o server MCP ai prodotti Adobe è una configurazione selezionata dal cliente. I clienti sono responsabili della valutazione della sicurezza e dell&#39;idoneità di qualsiasi integrazione MCP. Adobe non è responsabile dei problemi derivanti da configurazione errata, utilizzo errato di MCP, vulnerabilità in implementazioni di terze parti o azioni non intenzionali eseguite tramite flussi di lavoro abilitati per MCP.
>
>Per ridurre i rischi, Adobe incoraggia a testare le integrazioni in un ambiente sandbox prima di utilizzarle in modo produttivo e a rivedere e convalidare attentamente tutte le azioni e le risposte avviate da MCP prima di confermarle o di fare affidamento su di esse.

## Qual è il protocollo di contesto del modello? {#mcp-overview}

I team di marketing, dati e customer-experience si affidano sempre di più ad applicazioni basate su chat e a strumenti per sviluppatori, come Anthropic Claude, OpenAI ChatGPT, Cursor e Microsoft Copilot Studio, per semplificare il loro lavoro quotidiano. Queste applicazioni supportano **Model Context Protocol (MCP)**, uno standard aperto che consente alle applicazioni di esporre gli strumenti back-end a modelli LLM (Large Language Model) in modo uniforme.

Real-Time CDP ora fornisce un server MCP che mette in evidenza le operazioni di pubblico, destinazione e attivazione direttamente all&#39;interno di qualsiasi applicazione compatibile con MCP. Con l’integrazione MCP di Real-Time CDP, utenti tipo diversi possono collaborare intorno agli stessi dati di segmentazione e attivazione, senza scrivere query sulle API REST di Adobe Experience Platform o navigare su più schermate dell’interfaccia utente. I clienti possono descrivere il proprio intento conversazionalmente e consentire al LLM di richiamare gli strumenti MCP appropriati.

## Funzionalità principali {#mcp-capabilities}

Il server MCP di Real-Time CDP consente di controllare, riepilogare e risolvere i problemi relativi a tipi di pubblico e destinazioni direttamente dall’assistente AI. Tutte le operazioni sono **di sola lettura**. Le superfici del server MCP recuperano le API come risposte in linguaggio semplice per consentire di:

* **Ottieni visibilità immediata del pubblico**: chiedi informazioni sulle definizioni del pubblico, lo stato del ciclo di vita e lo spazio dei nomi in linguaggio semplice senza navigare nei menu o richiamare i report manualmente.
* **Stimare la dimensione del pubblico prima dell&#39;attivazione** — Visualizzare in anteprima i conteggi delle appartenenze e gli intervalli di affidabilità per una query di segmenti PQL o SDD prima di impegnarsi a creare un pubblico.
* **Controlla il tuo portfolio di attivazione**: controlla le destinazioni configurate, i flussi di dati che le alimentano e le connessioni sorgente/destinazione dietro ogni flusso, senza analizzare JSON o passare da uno schermo all&#39;altro del prodotto.
* **Problemi di attivazione al volo** - La destinazione non riuscita o in esecuzione viene eseguita nel momento in cui viene richiesto, in modo che il team possa agire rapidamente.
* **Collaborazione in base a dati live**: addetti al marketing, ingegneri di dati e stakeholder possono eseguire query sugli stessi dati live di Real-Time CDP tramite il proprio assistente AI, semplificando l&#39;allineamento, la decisione e lo spostamento.

## Strumenti disponibili {#mcp-tools}

La disponibilità degli strumenti sta rapidamente cambiando con l&#39;attivazione di nuovi strumenti. Contatta il tuo rappresentante Adobe per ottenere un elenco degli strumenti più recenti disponibili.

>[!NOTE]
>
>Tutti gli strumenti sono **di sola lettura**. Le operazioni di scrittura (creazione, aggiornamento o eliminazione di tipi di pubblico, destinazioni o flussi di dati) non sono supportate nella versione corrente di Beta.

## Casi d’uso {#mcp-use-cases}

Gli esempi seguenti mostrano come interagire con il server MCP [!DNL Adobe Real-Time CDP] utilizzando il linguaggio naturale:

| Obiettivo | Esempio di prompt |
| --- | --- |
| **Individuazione catalogo di destinazione** | &quot;TikTok è disponibile come destinazione nella mia sandbox?&quot; / &quot;Per quali tipi di destinazione sono già configurati gli account?&quot; |
| **Inventario di destinazione per tipo** | &quot;Elenca tutte le mie destinazioni Amazon S3.&quot; / &quot;Ho configurato delle destinazioni di esportazione del set di dati?&quot; |
| **Controllo configurazione di destinazione** | &quot;A quale bucket scrive la destinazione `Loyalty S3 Export`?&quot; / &quot;Visualizza il percorso di destinazione e il formato del file per il flusso di dati [ID].&quot; |
| **Integrità account** | &quot;Quale dei miei account di destinazione ha credenziali scadute?&quot; / &quot;Esistono account Pinterest o Facebook in stato di errore?&quot; |
| **Integrità attivazione - ultime 24 ore** | &quot;Elenca tutte le destinazioni con un&#39;esecuzione non riuscita nelle ultime 24 ore.&quot; / &quot;La mia destinazione di esportazione del set di dati ha inviato dati nelle ultime 24 ore?&quot; |
| **Cronologia attivazioni per destinazione** | &quot;`Weekly Loyalty Export` ha esportato qualcosa negli ultimi 30 giorni?&quot; / &quot;Visualizza la cronologia di esecuzione completa per la destinazione {NAME}.&quot; |
| **Analisi errori** | &quot;Qual è la causa più comune di errore nelle destinazioni basate su file di questa settimana?&quot; / &quot;Raggruppa esecuzioni recenti non riuscite per tipo di errore.&quot; |
| **Individuazione e filtro del pubblico** | &quot;Elenca ogni pubblico basato su CSV nella sandbox `marketing-prod`.&quot; / &quot;Quali tipi di pubblico hanno un ID di pubblico esterno definito?&quot; |
| **Controllo del dimensionamento del pubblico** | &quot;Mostrami ogni pubblico con dimensione 0.&quot; / &quot;Quali tipi di pubblico sono più grandi di 1.000 profili?&quot; |
| **Controllo scadenza pubblico** | &quot;Quali destinazioni hanno tipi di pubblico con data di fine già passata?&quot; / &quot;Elenca i tipi di pubblico con scadenza prevista nei prossimi 7 giorni&quot;. |
| **Ingombro di Audience Activation** | &quot;Quali destinazioni hanno più di 10 tipi di pubblico attivati?&quot; / &quot;Quale pubblico viene attivato per il maggior numero di destinazioni?&quot; |
| **Filtro incrociato: attivazione × pubblico** | &quot;Mostra i tipi di pubblico con dimensioni superiori a 1.000 che sono attivati su almeno 2 destinazioni&quot; / &quot;Tipi di pubblico di grandi dimensioni che vengono attivati solo su una singola destinazione.&quot; |
| **Anteprima appartenenza pubblico** | &quot;Anteprima della dimensione di appartenenza per il pubblico `High-Value Loyalty Members`.&quot; / &quot;Stimare la dimensione di questa query PQL prima di salvarla: {EXPRESSION}.&quot; |

## Prerequisiti {#mcp-prerequisites}

Prima di collegare il server Real-Time CDP MCP al client MCP, verificare quanto segue:

* Hai una licenza Real-Time CDP attiva.
* Hai accesso a un client supportato che può connettersi a un server MCP remoto o a un’app MCP personalizzata, ad esempio Claude, ChatGPT, Claude Code, Codex, Cursor o VS Code.
* Hai il tuo ID organizzazione e il nome della sandbox su cui desideri eseguire la query.
* In Adobe Experience Platform disponi delle autorizzazioni necessarie per visualizzare tipi di pubblico, destinazioni ed entità del servizio di flusso.

## Collegare il server Real-Time CDP MCP {#mcp-connect}

>[!NOTE]
>
>Questa integrazione è in Beta. I menu client, i requisiti del piano e i controlli di amministrazione possono variare a seconda dell’applicazione e della versione.

Prima di iniziare, assicurati di avere i seguenti elementi:

* URL dell&#39;endpoint del server MCP: `Available to Beta customers through your Adobe representative`.
* Conferma che l’utente di Adobe abbia accesso all’organizzazione Experience Platform di destinazione e alla sandbox.

Il server MCP di Real-Time CDP è un **server MCP HTTP remoto**. In ogni client, la configurazione segue lo stesso schema:

1. Aggiungi l’URL del server.
2. Salva o abilita la connessione.
3. Completa l&#39;accesso ad Adobe basato su browser **&#x200B;**&#x200B;la prima volta che il client richiama uno strumento.
4. Fornisci `imsOrgId` e `sandboxName` per ogni richiesta.

### Eseguire l’installazione in client basati sull’interfaccia utente {#mcp-connect-ui}

#### Claude

Per `claude.ai` e Claude Desktop, aggiungi il server Real-Time CDP MCP come **connettore personalizzato** utilizzando l&#39;endpoint fornito dal tuo rappresentante Adobe. Nei singoli piani Claude, aggiungerlo in **Personalizza > Connettori**. Nei piani Team ed Enterprise, un proprietario potrebbe aver bisogno di aggiungerlo prima in **Impostazioni organizzazione > Connettori**, dopo di che ogni utente lo connette nelle proprie impostazioni Claude. Una volta configurato, abilita il connettore in una conversazione e completa l’accesso del browser Adobe al primo utilizzo.

#### ChatGPT

In ChatGPT, aggiungi il server Real-Time CDP MCP come **app/connettore personalizzato** utilizzando l&#39;endpoint fornito dal tuo rappresentante Adobe. A seconda del piano ChatGPT, potrebbe essere necessaria l&#39;approvazione di **Modalità sviluppatore** e dell&#39;amministratore dell&#39;area di lavoro. Dopo aver creato o abilitato l&#39;app o il connettore, collegalo da **Impostazioni > App** o **Impostazioni > App e connettori**, quindi esegui l&#39;autenticazione tramite l&#39;accesso del browser Adobe quando richiesto.

#### Cursore

In Cursore, aggiungi il server MCP di Real-Time CDP come server MCP remoto utilizzando l’endpoint fornito dal tuo rappresentante Adobe. Apri **Impostazioni > MCP**, aggiungi un nuovo server e incolla l&#39;URL dell&#39;endpoint. Dopo l&#39;aggiunta, abilitare il server per l&#39;area di lavoro selezionando **connetti** per l&#39;autenticazione tramite il browser.

#### Altri client basati su interfaccia utente

Per client quali VS Code o altre applicazioni desktop e Web con supporto MCP remoto, aggiungi il server MCP Real-Time CDP come server HTTP **remoto** utilizzando l&#39;endpoint fornito dal tuo rappresentante Adobe. Se il client supporta intestazioni o token Bearer opzionali, lasciali vuoti a meno che Adobe non fornisca istruzioni specifiche per il contrario; al primo utilizzo l’autenticazione viene gestita tramite il flusso di accesso di Adobe basato su browser.

### Installazione in client tecnici {#mcp-connect-technical}

#### Claude Code

Aggiungere il server dal terminale:

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

Quindi avvia Claude Code ed esegui:

```text
/mcp
```

Seleziona il server `rtcdp` e completa il flusso di accesso di Adobe nel browser. Se il server è già stato aggiunto in `claude.ai`, può essere visualizzato automaticamente anche in Claude Code quando entrambi utilizzano lo stesso account.

#### Codice

Aggiungere il server dal terminale:

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

Autentica il server:

```bash
codex mcp login rtcdp
```

Verifica la configurazione:

```bash
codex mcp list
```

È inoltre possibile aggiungere il server direttamente a `~/.codex/config.toml`:

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### Parametri di richiesta richiesti {#mcp-connect-params}

Ogni chiamata allo strumento richiede due parametri che definiscono l’ambito della richiesta:

* `imsOrgId` — l&#39;ID organizzazione, mappato all&#39;intestazione `x-gw-ims-org-id` nelle chiamate API di Experience Platform a valle.
* `sandboxName` — nome della sandbox di Experience Platform mappato all&#39;intestazione `x-sandbox-name`.

## Limitazioni note (Beta) {#mcp-limitations}

Le seguenti limitazioni si applicano alla versione corrente di Beta del server MCP [!DNL Adobe Real-Time CDP]:

| Limitazione | Descrizione | Soluzione alternativa |
| --- | --- | --- |
| **Superficie di sola lettura** | Il server MCP espone solo le API di recupero. Non puoi creare, aggiornare, attivare o eliminare tipi di pubblico, destinazioni o flussi di dati. | Utilizza l’interfaccia utente di Real-Time CDP o le API REST di AEP per le operazioni di scrittura. |
| **Nessuna metrica di coinvolgimento o consegna** | Il server MCP non restituisce le statistiche di consegna downstream, coinvolgimento o metriche di conversione dalle piattaforme di destinazione. | Utilizza la funzione di reporting della piattaforma di destinazione, Customer Journey Analytics MCP o Adobe Analytics MCP, per i dati di coinvolgimento e conversione. |
| **La query del segmento deve essere creata esternamente** | `Preview Audience Membership` richiede un&#39;espressione PQL o SDD valida come input. Il server MCP non compone la query. | Crea l’espressione PQL/SDD nell’interfaccia utente di Segment Builder o tramite l’API del servizio di segmentazione, quindi incolla nel prompt MCP. |
| **Paginazione tramite token di continuazione** | Gli strumenti elenco restituiscono risultati impaginati. L&#39;enumerazione completa in sandbox molto grandi richiede il concatenamento di `continuationToken` chiamate. | Eseguire query limitate utilizzando i filtri (nome, stato, specifica di connessione, intervallo di tempo) anziché enumerare l&#39;elenco completo. |
| **Il filtro dell&#39;esecuzione dell&#39;attivazione è basato solo sul tempo** | `Inspect Activation Runs` supporta il filtro per stato e timestamp di completamento (epoca ms UTC), ma non direttamente per tipo di errore o piattaforma di destinazione. | Filtra per `flowId` prima (ottenuto da `List Configured Destinations`) per eseguire l&#39;ambito in una destinazione specifica. |
| **È richiesta la configurazione dell&#39;area** | Se il gateway MCP non è configurato per l’area geografica dell’utente, le chiamate dello strumento avranno esito negativo e verrà visualizzato HTTP 403 &quot;Area geografica utente mancante&quot;. | Contatta il rappresentante Adobe per verificare che il gateway sia configurato per la tua area geografica prima del primo utilizzo. |

## Domande frequenti {#mcp-faq}

+++Quali client MCP sono supportati?

Il server MCP di Real-Time CDP funziona con client supportati che possono connettersi ai server MCP remoti o alle app MCP personalizzate, tra cui Claude, ChatGPT, Claude Code, Codex, Cursor e VS Code. Il flusso di installazione dipende dal client: i client basati sull’interfaccia utente in genere aggiungono il server dalle impostazioni, mentre i client tecnici come Claude Code e Codex possono aggiungerlo dalla riga di comando o dai file di configurazione.
+++

+++Come funziona l’autenticazione?

L&#39;autenticazione viene gestita tramite un accesso basato su **browser**. Quando il client MCP richiama uno strumento, apre il browser predefinito a una pagina di accesso di Adobe. Dopo aver autenticato e autorizzato il client, la sessione viene stabilita e le successive chiamate allo strumento lo riutilizzano. Non è necessario archiviare chiavi API o credenziali di lunga durata nella configurazione client.
+++

+++A quali oggetti Real-Time CDP è possibile accedere tramite MCP?

Puoi accedere a tipi di pubblico, tipi di destinazione, account di destinazione configurati, flussi di dati di destinazione, connessioni di origine e di destinazione e cronologia dell’esecuzione dell’attivazione. Le operazioni sono di sola lettura (recupero API); le operazioni di scrittura non sono supportate nella versione corrente.
+++

+++È necessario l&#39;accesso per sviluppatori per utilizzare il server Real-Time CDP MCP?

No. Il server MCP è progettato sia per utenti tecnici che di marketing. Gli addetti al marketing possono interagire con esso utilizzando prompt in linguaggio naturale in qualsiasi client MCP supportato, mentre i data engineer e gli sviluppatori possono utilizzarlo in strumenti per sviluppatori che supportano MCP.
+++

+++I dati vengono inviati al provider client MCP?

Quando si invia una richiesta, il client MCP può inviare il contesto pertinente (inclusi i dati Real-Time CDP restituiti dal server MCP) al proprio modello per l&#39;elaborazione. Rivedi le politiche sulla privacy e la gestione dei dati del provider client MCP prima di connetterti ai dati di produzione.
+++

+++Di quali autorizzazioni ho bisogno in Real-Time CDP?

Sono necessarie almeno le autorizzazioni **Visualizza** per gli oggetti di cui si desidera eseguire la query: tipi di pubblico, destinazioni ed entità del servizio di flusso. Non sono necessarie autorizzazioni di scrittura perché il server MCP esegue solo operazioni di lettura. Contattare l&#39;amministratore [!DNL Adobe Experience Platform] in caso di dubbi sul livello di accesso corrente.
+++

+++Posso utilizzare il server MCP in ambienti sandbox?

Sì. Ogni chiamata allo strumento richiede un parametro `sandboxName`, pertanto il server MCP rispetta sempre la configurazione sandbox [!DNL Adobe Experience Platform]. Puoi eseguire una query su qualsiasi sandbox a cui hai accesso specificandone il nome nella richiesta.
+++

+++Qual è la differenza tra Anteprima appartenenza al pubblico e Ricerca tipi di pubblico esistenti?

`Search Existing Audiences` restituisce tipi di pubblico che sono già stati creati e salvati nella sandbox. `Preview Audience Membership` prende un&#39;espressione di segmento PQL o SDD non elaborata e restituisce una stima delle dimensioni, utile per dimensionare una query *prima* che venga salvata come pubblico.
+++

+++È possibile eseguire query sui tipi di pubblico dell’account e sui tipi di pubblico del profilo?

Sì. Sia `Search Existing Audiences` che `Preview Audience Membership` supportano un parametro del tipo di entità. I tipi di pubblico di profilo possono essere espressi in PQL o SDD; i tipi di pubblico di account utilizzano sempre la sintassi SDD (relazionale).
+++
