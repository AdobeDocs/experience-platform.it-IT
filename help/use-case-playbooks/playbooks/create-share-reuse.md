---
solution: Experience Platform
title: Creare, condividere e riutilizzare le istanze del playbook
description: Scopri come creare, condividere e riutilizzare le istanze del playbook per eseguire il caso d’uso di marketing.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: c4be3864c680a569166d53f18ec0ee28a52c9ea7
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 81%

---

# Creare, condividere e riutilizzare le istanze del playbook

Per utilizzare un playbook, passa a **[!UICONTROL Playbook per casi d’uso] > [!UICONTROL Playbook]**. Sfoglia e utilizza le varie opzioni di ricerca e filtro disponibili nella pagina per selezionare e iniziare a utilizzare un playbook specifico.

## Creare un’istanza del playbook {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Crea istanza"
>abstract="Genera un elenco di risorse come percorsi, tipi di pubblico, schemi o destinazioni da utilizzare in scenari di percorso o attivazione."

Prima di creare un’istanza del playbook, esplora i playbook disponibili per [trovare il playbook adatto a te](/help/use-case-playbooks/playbooks/discover.md). Quando sei pronto a procedere con un playbook e creare un’istanza, seleziona **[!UICONTROL Crea istanza]** per procedere con il playbook e generare risorse tecniche.

![Crea un’istanza di un playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Questa azione genera diverse risorse da utilizzare per ottenere il caso d’uso descritto dal playbook.

![Vista playbook delle risorse generate dopo l’abilitazione.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Utilizzare i controlli di configurazione per modificare i nomi e le descrizioni delle istanze {#edit-instance-metadata}

Dopo aver creato un’istanza basata su un playbook, puoi personalizzarla per distinguerla dalle altre istanze create dallo stesso playbook. Seleziona il controllo di configurazione come mostrato di seguito. Modifica il nome, la descrizione e le note e seleziona **[!UICONTROL Salva]** quando hai finito.

![Modifica il nome e la descrizione di un’istanza.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### Comprendere le risorse generate {#understand-assets}

>[!IMPORTANT]
>
>Non devi preoccuparti! Questo è uno spazio sicuro in cui sperimentare e non puoi rompere nulla. Non sono ancora presenti dati associati alle risorse create. Innanzitutto, è necessario acquisire i dati per poter ottenere i casi d’uso.

È importante comprendere che le risorse generate differiscono in base al caso d’uso che si sta abilitando:

* Vengono generate risorse diverse per diversi tipi di playbook. Queste risorse vengono create specificatamente per il caso d’uso ottenuto attraverso il playbook. Un playbook, ad esempio, genera uno schema, un pubblico, un percorso e dei messaggi. Un altro playbook genera uno schema, un pubblico e una destinazione in cui attivare i dati.
* Le risorse stesse differiscono tra i playbook. Ad esempio, per il playbook **[!UICONTROL Invia un messaggio di auguri di compleanno agli ospiti]**, il pubblico creato ha la regola `birthday=today AND year=any`.

Per illustrare un esempio, per il playbook **[!UICONTROL Carrello abbandonato: merchandising]**, puoi vedere che viene creato un percorso specifico che include i messaggi creati per questo caso d’uso.

![Percorso creato dal playbook del caso d’uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### Utilizzare e modificare le risorse generate {#use-and-edit-assets}

Esplorando le risorse generate dopo aver creato un’istanza di un playbook, puoi modificare qualsiasi risorsa creata.

Se tu o qualcuno del tuo team create un’altra istanza del playbook, le risorse modificate vengono mantenute e vengono create nuove risorse per la nuova istanza del playbook.

Il comportamento descritto sopra vale per tutte le risorse create, ad eccezione degli schemi. Nel caso degli schemi, quando viene creata una nuova istanza di un playbook non vengono creati nuovi schemi, pertanto nell’istanza appena creata utilizzerai lo schema modificato da un’altra istanza del playbook.

>[!TIP]
>
>Esegui il test nella sandbox di sviluppo e, quando è pronto, passa alla produzione.
>
>Una volta generati gli oggetti, puoi continuare a testarli nelle sandbox di sviluppo aggiungendo dati. Puoi testare le risorse per tutto il tempo desiderato nella sandbox di sviluppo e replicare la logica delle risorse (definizioni di pubblico, percorsi, schemi e così via) nella sandbox di produzione quando lo desideri. Puoi passare alla sandbox di sviluppo e quindi alla sandbox di produzione utilizzando [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md).

## Riutilizzare i playbook {#reuse-playbooks}

Creando più istanze dello stesso playbook, puoi implementare lo stesso caso d’uso in un secondo momento, senza modificare i dettagli dell’implementazione precedente.

## Condividere il playbook e le risorse generate con altri membri del team {#share-playbook}

Puoi condividere l’istanza e le risorse generate con altri membri del team. A questo scopo, copia il collegamento URL dal browser e condividilo con il tuo team per offrire una panoramica delle risorse generate.

![URL evidenziato in una vista del playbook del caso d’uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Video introduttivo sul processo del playbook completo

Guarda questo video per scoprire come individuare, creare, pubblicare e risolvere problemi relativi a istanze di un playbook con casi d’uso end-to-end, nonché come copiare le risorse generate dal playbook in altre sandbox configurate nella tua organizzazione.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Passaggi successivi {#next-steps}

Consultando questa guida e quella per trovare il playbook adatto a te, ora sai come interpretare le varie sezioni di un playbook e come utilizzare le risorse generate dopo aver creato un’istanza di un playbook.

Successivamente, è possibile sfogliare il catalogo dei playbook per trovare il playbook adatto per il proprio caso d’uso e, se riscontri problemi, consultare la [guida alla risoluzione dei problemi](/help/use-case-playbooks/playbooks/troubleshooting.md).
