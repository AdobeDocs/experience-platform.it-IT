---
title: Autorizzazioni utente per i tag
description: Scopri i diversi tipi di autorizzazioni disponibili per i tag e alcune strategie di implementazione di base per diversi casi d’uso aziendali.
exl-id: 9b48847a-6133-4dbd-b17d-e7b88152ad7d
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 23%

---

# Autorizzazioni utente per i tag

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Le autorizzazioni utente per i tag in Adobe Experience Platform vengono assegnate agli utenti tramite Adobe Admin Console. Anziché essere assegnati a singoli utenti, diversi set di autorizzazioni vengono configurati separatamente come profili di prodotto. Gli utenti vengono quindi assegnati a questi profili di prodotto per ottenere le autorizzazioni per le quali sono stati configurati.

Questa guida fornisce una panoramica dei diversi tipi di autorizzazioni disponibili per i tag, delle funzionalità a cui concedono l’accesso e di alcune strategie di implementazione di base per diversi casi d’uso aziendali.

>[!NOTE]
>
>Per i passaggi su come configurare le autorizzazioni per gli utenti che utilizzano Admin Console, consulta l’esercitazione su [gestione delle autorizzazioni per la raccolta dati](../../../collection/permissions.md).

## Tipi di autorizzazione

All’interno di un profilo di prodotto, le autorizzazioni per i tag sono suddivise in quattro categorie:

1. Piattaforme
1. Proprietà
1. Diritti di proprietà
1. Diritti aziendali

### Piattaforme

Ogni proprietà tag dispone di una piattaforma. Al momento esistono due piattaforme utilizzabili per i tag: Web e Mobile. Puoi utilizzare questo tipo di autorizzazione per limitare o concedere l’accesso a un particolare tipo di proprietà. Questa funzione può essere utile quando il team che gestisce le app mobili è diverso da quello che gestisce i siti web.

### Proprietà

Per impostazione predefinita, i profili di prodotto consentono l’accesso a tutte le proprietà esistenti all’interno dell’azienda, sia attualmente che in futuro. Utilizzando questo tipo di autorizzazione, puoi limitare o concedere l’accesso a specifiche proprietà esistenti per nome.

### Diritti di proprietà {#property-rights}

Qualsiasi proprietà tag creata nell’interfaccia utente diventa disponibile in Admin Console e consente di raggruppare la proprietà con diritti di proprietà specifici nello stesso profilo di prodotto.

Ad esempio, se un determinato profilo di prodotto non ha accesso alla proprietà A1, gli utenti che appartengono a tale profilo non possono visualizzare o modificare le impostazioni all’interno della proprietà A1.

Se un utente appartiene a un profilo che ha accesso alla proprietà A1, le azioni che può eseguire all&#39;interno della proprietà A1 sono determinate dai diritti concessi da questo profilo. Se un utente dispone delle autorizzazioni per la proprietà A1 ma non dispone di diritti assegnati, ha accesso in sola lettura a tale proprietà.

La tabella seguente illustra i diritti di proprietà disponibili e le funzionalità a cui danno accesso:

| Diritto di proprietà | Descrizione |
| --- | --- |
| **Sviluppa** | Questo consente di eseguire le azioni seguenti:<ul><li>Creare regole ed elementi dati</li><li>Creare librerie e generarle negli ambienti di sviluppo esistenti</li><li>Inviare una libreria per l’approvazione</li></ul>La maggior parte delle attività quotidiane nell’interfaccia utente di richiede questo diritto. |
| **Approvazione** | Questo consente di trasferire nell’ambiente di staging una libreria e una build inviate. Puoi inoltre approvare una libreria per la pubblicazione dopo aver completato i test. |
| **Pubblica** | Questo consente di pubblicare librerie approvate nell’ambiente di produzione. |
| **Gestire le estensioni** | Questo consente di eseguire le azioni seguenti: <ul><li>Installare nuove estensioni in una proprietà</li><li>Modificare la configurazione per un&#39;estensione già installata</li><li>Eliminare un’estensione</li></ul>Per ulteriori informazioni sulle estensioni, consulta la [panoramica sulle estensioni](../managing-resources/extensions/overview.md). In genere questo ruolo appartiene al reparto IT o Marketing, a seconda dell&#39;organizzazione. |
| **Gestisci ambienti** | Questo consente di creare e modificare gli ambienti. Per ulteriori informazioni, consulta la [documentazione degli ambienti](../publishing/environments.md). Generalmente, questo ruolo appartiene al reparto IT. |

{style="table-layout:auto"}

### Diritti aziendali

I diritti aziendali si applicano ad autorizzazioni che si estendono su più proprietà. Questi sono descritti nella tabella seguente:

| Diritto dell’azienda | Descrizione |
| --- | --- |
| **Gestisci proprietà** | Questo consente di eseguire le azioni seguenti:<ul><li>Creare nuove proprietà</li><li>Modificare i metadati e le impostazioni a livello di proprietà</li><li>Elimina proprietà</li></ul>Generalmente, gli amministratori eseguono questo ruolo. Consulta la [documentazione sulle proprietà](companies-and-properties.md) per ulteriori informazioni. |
| **Sviluppare estensioni** | Consente di creare e modificare pacchetti di estensione di proprietà dell’azienda, incluse versioni private e richieste di versioni pubbliche. |
| **Gestire le configurazioni dell’app** | Questa opzione è disponibile solo per chi dispone di una licenza per Adobe Journey Optimizer o di un’altra soluzione che consente l’accesso a messaggi mobili in-app e push.  Questo consente di gestire le app conosciute da Experience Cloud insieme alle credenziali push necessarie per comunicare con il servizio di messaggistica Firebase Cloud e il servizio Apple Push Notification. |

{style="table-layout:auto"}

## Autorizzazioni utente totali

Le autorizzazioni totali di un singolo utente sono determinate dall’iscrizione totale in profili di prodotto diversi. Se un utente appartiene a più profili di prodotto, le autorizzazioni di ciascun profilo vengono aggiunte insieme anziché moltiplicate.

Ad esempio, il profilo di prodotto A ti concede il diritto Develop per la proprietà 1. Il profilo di prodotto B ti concede il diritto Publish per la proprietà 2. In questo caso, è possibile sviluppare nella proprietà 1 e pubblicare nella proprietà 2, ma non è possibile pubblicare nella proprietà 1 o sviluppare nella proprietà 2 perché non si dispone dei diritti espliciti per farlo.

## Scenari di diritti

Diverse aziende hanno esigenze diverse per la creazione di nuovi profili di prodotto. Queste esigenze variano in base alle dimensioni dell’azienda, alla struttura organizzativa, al numero di siti, al numero di persone coinvolte nella gestione dei tag e così via.

Di seguito sono riportati alcuni scenari comuni e un punto di partenza consigliato per la creazione di profili di prodotto e l’aggiunta di utenti.

### Un solo protagonista

Se gestisci una piccola azienda che ha una sola persona responsabile di tutto, concedi a questo utente le autorizzazioni per tutte le proprietà e assegnagli tutti i diritti elencati sopra.

### Separazione dei compiti

Considera una situazione in cui molte persone dell’organizzazione sono coinvolte nell’assegnazione di tag. Hai un gruppo di persone (ad esempio un consulente esterno) che crea regole ed elementi di dati, ma non vuoi che abbiano accesso all&#39;ambiente di produzione. In questo caso, assicurati che nessuno distribuisca in produzione ad eccezione del team IT.

Per eseguire questa operazione:

1. Crea un account per i tuoi consulenti e concedi loro solo il diritto di sviluppo.
1. Il consulente genera ed esegue test all&#39;interno dei confini impostati.
1. Se il consulente desidera una nuova estensione o è pronto per andare live, un rappresentante della tua organizzazione (con i diritti appropriati) esegue tali azioni.

### Enterprise

Un&#39;azienda di livello Enterprise potrebbe avere più siti divisi geograficamente, con team diversi responsabili di ogni area geografica. All&#39;interno di questi team, i vari utenti possono sviluppare e pubblicare.

È simile al precedente scenario &quot;Separazione dei compiti&quot;, ma organizzato per aree geografiche. Ad esempio, puoi creare un profilo &quot;Develop&quot; (Sviluppa) e un profilo &quot;Publish&quot; (Pubblica) per il Nord America e creare gruppi separati &quot;Develop&quot; (Sviluppa) e &quot;Publish&quot; (Pubblica) per l’Europa.

## Ruoli di esempio

Nella tabella seguente vengono forniti alcuni esempi dei tipi di ruoli che è possibile avere nell&#39;organizzazione e delle autorizzazioni da assegnare:

| Ruolo | Descrizione | Proprietà | Diritti di proprietà | Diritti aziendali |
| --- | --- | --- | --- | --- |
| Manager | Vuole vedere cosa sta succedendo nel sistema, ma non dovrebbe essere in grado di apportare modifiche. | Inclusione automatica | (Nessuna) | (Nessuna) |
| Addetto al marketing | Può installare estensioni e impostare nuovi tag per le proprietà esistenti, ma non può pubblicare negli ambienti di staging o produzione. | Inclusione automatica | <ul><li>Sviluppa</li><li>Gestire le estensioni</li></ul> | <ul><li>Gestisci proprietà</li></ul> |
| Sviluppatore app mobili | È responsabile dell’implementazione di soluzioni Adobe e di terze parti all’interno di un’app mobile nativa. | Inclusione automatica | <ul><li>Sviluppa</li><li>Gestire le estensioni</li></ul> | <li>Gestisci proprietà</li><li>Gestire le configurazioni dell’app</li> |
| Team IT | Non modifica effettivamente alcun tag, ma ha il pieno controllo sugli ambienti di staging e produzione e su ciò che contiene. | Inclusione automatica | (Nessuna) | <ul><li>Approvazione</li><li>Pubblica</li><li>Gestisci ambienti</li></ul> |
| Sviluppatore di estensioni | Sviluppa le estensioni e può inviarle per l&#39;approvazione, ma non può pubblicarle o aggiungerle alle proprietà esistenti. | Inclusione automatica | <ul><li>Sviluppa</li></ul> | <ul><li>Gestisci proprietà</li><li>Sviluppare estensioni</li></ul> |
| Utente privilegiato | Fa tutto. | Inclusione automatica | <ul><li>Sviluppa</li><li>Approvazione</li><li>Pubblica</li><li>Gestire le estensioni</li><li>Gestisci ambienti</li></ul> | <ul><li>Gestisci proprietà</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi

In questo documento è stata fornita una panoramica delle autorizzazioni disponibili per i tag nell’Experience Platform. Per i passaggi su come configurare i profili di prodotto per i tag in Adobe Admin Console, consulta la guida su [gestione delle autorizzazioni utente per la raccolta dati](../../../collection/permissions.md).
