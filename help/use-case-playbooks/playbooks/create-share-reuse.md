---
solution: Experience Platform
title: Creare, condividere e riutilizzare le istanze del playbook
description: Scopri come creare, condividere e riutilizzare le istanze del playbook per eseguire il caso di utilizzo di marketing.
badgeBeta: label="Beta" type="Informative"
source-git-commit: e61e200b148e4d17041b3711bd63c796a44b05c8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# (Beta) Creare, condividere e riutilizzare le istanze del playbook

>[!AVAILABILITY]
>
>Questa funzionalità è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per utilizzare un playbook, passare a **[!UICONTROL Playbook di casi d’uso] > [!UICONTROL Playbook]**. Sfoglia e utilizza le varie opzioni di ricerca e filtro disponibili nella pagina per selezionare e iniziare a utilizzare un playbook specifico.

## Creare un’istanza del playbook {#create-playbook-instance}

Prima di creare un’istanza del playbook, esplora i playbook disponibili per [scopri il playbook adatto a te](/help/use-case-playbooks/playbooks/discover.md). Quando sei pronto a procedere con un playbook e creare un’istanza, seleziona **[!UICONTROL Crea istanza]** per procedere con il playbook e generare risorse tecniche.

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

## Riutilizzare i playbook {#reuse-playbooks}

Creando più istanze dello stesso playbook, puoi implementare lo stesso caso d’uso in un secondo momento, senza modificare i dettagli della precedente implementazione del caso d’uso.

## Condividere il playbook e le risorse generate con altri membri del team {#share-playbook}

Puoi condividere l’istanza e le risorse generate con altri membri del gruppo. A questo scopo, copia il collegamento URL dal browser e condividilo con il tuo team per offrire una panoramica delle risorse generate.

![URL evidenziato in una visualizzazione del playbook del caso d’uso.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Passaggi successivi {#next-steps}

Leggendo questa guida e quella sulla scoperta del playbook adatto a te, ora sai come interpretare le varie sezioni di un playbook e come utilizzare le risorse generate dopo aver creato un’istanza di un playbook.

Quindi, è possibile sfogliare il catalogo dei playbook per trovare il playbook corretto per il proprio caso d’uso e leggere [guida alla risoluzione dei problemi](/help/use-case-playbooks/playbooks/troubleshooting.md) in caso di problemi.