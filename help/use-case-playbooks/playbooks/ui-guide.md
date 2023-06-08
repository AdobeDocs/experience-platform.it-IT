---
solution: Experience Platform
title: Guida all’interfaccia utente Playbook
description: Scopri come utilizzare l’interfaccia utente di Experience Platform per visualizzare e abilitare i playbook.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 1%

---


# (Beta) Come abilitare e riutilizzare un playbook

>[!AVAILABILITY]
>
>Questa funzionalità è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per utilizzare un playbook, passare a **[!UICONTROL Playbook di casi d’uso] > [!UICONTROL Playbook]**. Sfoglia e utilizza le varie opzioni di ricerca e filtro disponibili nella pagina per selezionare e iniziare a utilizzare un playbook specifico.

## Ricerca e filtro {#search-and-filter}

Utilizza la finestra di ricerca e i filtri disponibili nella pagina per trovare la playbook adatta al tuo caso d’uso.

Ad esempio, puoi filtrare i playbook che puoi utilizzare in base alla fase nel funnel di marketing di destinazione: conversione, coinvolgimento o fidelizzazione. Puoi anche filtrare i playbook visualizzati in base al settore di appartenenza o alla licenza del prodotto a cui hai accesso: Adobe Journey Optimizer o Real-time CDP.

![Filtrare i playbook per funnel di marketing, settore o prodotto](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

È inoltre possibile utilizzare la funzionalità di ricerca per trovare il playbook più adatto alle proprie esigenze. Di seguito trovi un esempio di come trovare un playbook che ti aiuti a interagire con gli utenti che potrebbero aver abbandonato il carrello.

![Contatta gli utenti che potrebbero aver abbandonato il carrello.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Oppure, puoi filtrare i playbook disponibili in base ai canali che intendi utilizzare per raggiungere i clienti, come puoi vedere di seguito:

![Filtra per canale](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Prova i filtri e l’opzione di ricerca per trovare la playbook che fa per te.

## Visualizza playbook e genera risorse {#view-playbook-generate-assets}

Prima di impostare un playbook e crearne istanze, è necessario esaminarlo per verificare che sia adatto alle proprie esigenze. Per aiutarti a comprendere meglio i casi d’uso che coprono, tutti i playbook contengono le sezioni elencate di seguito. Quando sei pronto a procedere e generare le risorse, seleziona **[!UICONTROL Crea istanza]**.

### Mindmap {#mindmap}

Utilizza la sezione mindmap in un playbook per comprendere i passaggi del flusso di lavoro che il playbook può aiutarti a risolvere. Visualizza il flusso di come tutti gli oggetti generati possono aiutarti a ottenere il caso d’uso, dal punto di vista dell’utente target del caso d’uso.

La mappa concettuale inizia con una definizione di chi viene raggiunto nel percorso di utenti e descrive in ogni passaggio se viene distribuito qualcosa per Adobe, come un nuovo messaggio o un promemoria, o se è qualcosa che l’utente target ha fatto che attiva il messaggio o l’evento successivo.

![Mappatura mentale playbook evidenziata.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Riepilogo {#summary}

Inspect include la sezione di riepilogo per capire quali risorse vengono generate una volta create le istanze dal playbook. Le risorse generate per ogni playbook sono personalizzate in base al caso d’uso abilitato dal playbook. Di seguito trovi ulteriori informazioni su tutti gli elementi nella sezione di riepilogo.

| Elemento | Descrizione |
---------|----------|
| **[!UICONTROL Pubblico di destinazione]** | Descrive gli utenti tipo a cui stai cercando di accedere tramite questo playbook di casi d’uso. |
| **[!UICONTROL Canali di marketing]** | Descrive i canali utilizzati per raggiungere gli utenti tipo target nel playbook. |
| **[!UICONTROL Risorse tecniche]** | Elenco delle risorse tecniche generate dopo la creazione delle istanze del playbook. Le risorse generate differiscono per playbook, a seconda del caso d’uso. Alcuni playbook possono generare schemi, segmenti e percorsi. Altri possono generare delle destinazioni. Consulta la sezione [Comprendere le risorse generate](#understand-assets) per ulteriori informazioni su come utilizzare e riutilizzare le risorse generate, consulta la sezione seguente. |

{style="table-layout:auto"}

![Riepilogo playbook evidenziato](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Istanze {#instances}

Scorri verso il basso fino alla sezione istanze per ottenere una panoramica delle istanze di questo playbook che tu o i membri del tuo team avete già creato. È possibile utilizzare vari controlli per ordinare e filtrare le istanze visualizzate, ad esempio per visualizzare solo quelle create dall&#39;utente. Puoi anche visualizzare varie informazioni su ciascuna istanza, come elencato di seguito.

| Elemento | Descrizione |
|---------|----------|
| **[!UICONTROL Nome]** | Il nome dell’istanza in base al playbook. Puoi personalizzare il nome e la descrizione di un’istanza. Leggi la sezione seguente su [come modificare i metadati di un’istanza](#edit-instance-metadata) per ulteriori informazioni. |
| **[!UICONTROL Stato]** | Indica lo stato dell’istanza. A **[!UICONTROL inviato]** l’istanza è pronta per l’uso. |
| **[!UICONTROL Creato]** | Indica quando è stata creata l’istanza. |
| **[!UICONTROL Creato da]** | Indica chi ha creato l’istanza. |
| **[!UICONTROL Ultima modifica]** | Indica quando è stata apportata l’ultima modifica all’istanza. |

{style="table-layout:auto"}

![Istanza playbook evidenziata.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Abilita playbook {#enable-playbook}

Quando sei pronto a procedere con un playbook e creare un’istanza, seleziona **[!UICONTROL Crea istanza]** per procedere con il playbook e generare risorse tecniche.

![Crea un&#39;istanza di un playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Questa azione genera diverse risorse da utilizzare per ottenere il caso d’uso descritto dal playbook.

![Visualizzazione playbook delle risorse generate dopo l’abilitazione.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilizzare i controlli di configurazione per modificare i nomi e le descrizioni delle istanze {#edit-instance-metadata}

Dopo aver creato un’istanza basata su un playbook, puoi personalizzarla per distinguerla dalle altre istanze create dallo stesso playbook. Selezionate il controllo di configurazione come mostrato di seguito. Modifica il nome, la descrizione e le note e seleziona **[!UICONTROL Salva]** quando hai finito.

![Modifica il nome e la descrizione di un’istanza.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Comprendere le risorse generate {#understand-assets}

>[!IMPORTANT]
>
>Non c&#39;è bisogno di preoccuparsi! Questo è uno spazio sicuro in cui sperimentare e non si può rompere nulla. Non sono ancora presenti dati associati alle risorse create. Devi innanzitutto acquisire i dati per poter ottenere i casi d’uso.

È importante comprendere che le risorse generate differiscono in base al caso d’uso che si sta abilitando:

* Vengono generate risorse diverse per diversi tipi di playbook. Queste risorse vengono create specificatamente per il caso d’uso ottenuto attraverso il playbook. Ad esempio, un playbook genera uno schema, un segmento, un percorso e dei messaggi. Un altro playbook genera uno schema, un segmento e una destinazione in cui attivare i dati.
* Le risorse stesse differiscono tra i playbook. Ad esempio, per **[!UICONTROL Invia Un Messaggio Di Compleanno Agli Ospiti]** playbook, il pubblico creato ha la regola `birthday=today AND year=any`.

Per illustrare un esempio, per **[!UICONTROL Carrello abbandonato: materiale promozionale]** playbook, puoi vedere che viene creato un percorso specifico che include i messaggi creati per questo caso d’uso.

![Percorso creato dal playbook del caso d’uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Utilizzare e modificare le risorse generate {#use-and-edit-assets}

Mentre esplori le risorse generate dopo aver creato un’istanza di un playbook, puoi modificare qualsiasi risorsa creata.

Se crei un’altra istanza del playbook, le risorse modificate vengono mantenute e vengono create nuove risorse per la nuova istanza del playbook.

Il comportamento descritto sopra è vero per tutte le risorse create, ad eccezione degli schemi. Nel caso degli schemi, quando viene creata una nuova istanza di un playbook non vengono creati nuovi schemi, pertanto nell’istanza appena creata utilizzerai lo schema modificato da un’altra istanza del playbook.

>[!TIP]
>
>Esegui il test nella sandbox di sviluppo e, quando è pronto, passa alla produzione.
>
>Una volta generati gli oggetti, puoi continuare a testarli nelle sandbox di sviluppo aggiungendo dati. Puoi testare le risorse per tutto il tempo che desideri nella sandbox di sviluppo e replicare la logica delle risorse (definizioni di segmenti, percorsi, schemi e così via) nella sandbox di produzione quando lo desideri.

### Riutilizzare i playbook {#reuse-playbooks}

Creando più istanze dello stesso playbook, puoi implementare lo stesso caso d’uso in un secondo momento, senza modificare i dettagli della precedente implementazione del caso d’uso.

### Condividere il playbook e le risorse generate con altri membri del team {#share-playbook}

Puoi condividere l’istanza e le risorse generate con altri membri del gruppo. A questo scopo, copia il collegamento URL dal browser e condividilo con il tuo team per offrire una panoramica delle risorse generate.

![URL evidenziato in una visualizzazione del playbook del caso d’uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Passaggi successivi {#next-steps}

Leggendo questa guida dell’interfaccia utente, ora sai come interpretare le varie sezioni di un playbook e come utilizzare le risorse generate dopo aver creato un’istanza di un playbook. Quindi, puoi sfogliare il catalogo dei playbook per trovare il playbook corretto per il tuo caso d’uso e leggere la guida alla risoluzione dei problemi in caso di errori.