---
title: Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti sandbox
description: Per ripristinare in modo sicuro le sandbox e aggiungere il supporto per il controllo delle versioni, esegui il backup delle configurazioni degli oggetti (o dei metadati) utilizzando pacchetti di strumenti sandbox. I pacchetti di backup impediscono la perdita di configurazioni critiche come schemi, set di dati e tipi di pubblico, soprattutto durante le iterazioni di sviluppo.
exl-id: cccbaaf1-ee68-4a00-9a44-aa5db4a83a14
source-git-commit: 2a700788d9b59bcdb4195e34d77eccd278803d42
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 3%

---

# Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti sandbox

Per ripristinare in modo sicuro le sandbox e aggiungere il supporto per il controllo delle versioni, esegui il backup delle configurazioni degli oggetti (o dei metadati) utilizzando pacchetti di strumenti sandbox. I pacchetti di backup impediscono la perdita di configurazioni critiche come schemi, set di dati e tipi di pubblico, soprattutto durante le iterazioni di sviluppo.

![Panoramica dei vantaggi offerti dagli strumenti sandbox](../images/use-cases/tooling-overview.png)

## Perché considerare questo caso d’uso {#why-this-use-case}

La creazione di un pacchetto di backup mediante gli strumenti sandbox garantisce l&#39;archiviazione e la protezione delle configurazioni degli oggetti. Le sandbox di sviluppo possono riempirsi rapidamente durante l’esperimento e la generazione, mentre la creazione di una sandbox da zero dopo il ripristino può richiedere tempo e lasciare spazio per gli errori. Con la potenza degli strumenti sandbox, puoi importare un pacchetto di backup in una sandbox appena reimpostata per restituire immediatamente le configurazioni ideali in modo da poter continuare a sviluppare.

I pacchetti di backup consentono inoltre di supportare il controllo delle versioni durante tutto il processo di sviluppo. Man mano che la sandbox cambia, crea pacchetti di backup aggiuntivi insieme ai pacchetti precedenti in modo da poter ripristinare facilmente la sandbox in qualsiasi configurazione.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Quando si prevede di creare un pacchetto di backup personalizzato all&#39;interno dell&#39;organizzazione, prendere in considerazione i seguenti prerequisiti nel processo di pianificazione:

- Valuta gli utilizzi correnti delle sandbox all’interno della tua organizzazione. Esistono sandbox non di produzione che si avvicinano o superano i diritti di licenza?
- Qual è l&#39;ambito dei metadati di cui si desidera eseguire il backup? A seconda del caso d’uso, potrebbe essere utile eseguire il backup di una sandbox completa o parziale.
- A seconda dei metadati dell&#39;ambito di cui si desidera eseguire il backup, assicurarsi di aver compreso come [aggiungere manualmente oggetti a un pacchetto](../ui/sandbox-tooling.md#add-object-to-a-new-package) o come [esportare un&#39;intera sandbox](../ui/sandbox-tooling.md#export-an-entire-sandbox).
- Assicurati di avere accesso agli strumenti sandbox nella tua organizzazione con le autorizzazioni corrette.

### Funzionalità dell’interfaccia utente, componenti della piattaforma e prodotti di Experience Cloud che utilizzerai {#ui-functionality-and-elements}

Per implementare correttamente questo caso d’uso, devi utilizzare più aree di Adobe Experience Platform. Assicurati di disporre delle [autorizzazioni di controllo dell&#39;accesso basate su attributi](../../access-control/abac/overview.md) necessarie per tutte queste aree, oppure chiedi all&#39;amministratore di sistema di concederti le autorizzazioni necessarie.

- [Strumenti sandbox](../ui/sandbox-tooling.md)
- [Gestione sandbox](../ui/user-guide.md)
- [Dashboard utilizzo licenze](../../landing/license-usage-and-guardrails/license-usage-dashboard.md)
- [Set di dati](../../catalog/datasets/overview.md)
- [Schemi](../../xdm//home.md)
- [Tipi di pubblico](../../segmentation/home.md)
- [Percorsi da Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

1. Definire l&#39;ambito dei metadati da sottoporre a backup.
2. Utilizza l’interfaccia utente degli strumenti sandbox per esportare gli oggetti desiderati in un pacchetto di backup.
3. Crea regolarmente nuove versioni del pacchetto di backup per garantire che le sandbox rimangano allineate alle configurazioni correnti.
4. Verifica l’utilizzo corrente nel dashboard utilizzo licenze in base ai diritti per le sandbox non di produzione.
5. Ripristina le sandbox non di produzione per rispettare i diritti o liberare risorse e dati non necessari.
6. Importa il pacchetto di backup nella sandbox dopo averlo reimpostato per ripristinare le configurazioni dell’oggetto.

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello precedente.

### Definire l’ambito dei metadati

Prima di iniziare a creare il pacchetto di backup, è necessario considerare il caso d’uso del pacchetto. A seconda delle tue esigenze, puoi eseguire il backup di una sandbox completa o selezionare oggetti specifici da aggiungere al pacchetto, come indicato nei [prerequisiti](#prerequisites-and-planning).

>[!NOTE]
>
> Se stai valutando di eseguire il backup della sandbox per ripristinarla, tieni presente le [limitazioni](../ui/user-guide.md#reset-a-sandbox) relative alla reimpostazione delle sandbox.

### Esportare i metadati scelti in un pacchetto

A questo punto, è possibile eseguire il backup della sandbox utilizzando l’interfaccia utente degli strumenti sandbox. Questo passaggio tratta sia il backup di un’intera sandbox che il backup di oggetti specifici.

>[!NOTE]
>
> Non tutti gli oggetti sono supportati per gli strumenti sandbox. Per un elenco completo degli oggetti consentiti, consulta la guida [oggetti supportati per gli strumenti sandbox](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling).

#### Esportare una sandbox completa

Per eseguire il backup completo della sandbox, segui la [guida agli strumenti della sandbox](../ui/sandbox-tooling.md#export-an-entire-sandbox) per creare e pubblicare un nuovo pacchetto contenente le configurazioni dell&#39;intera sandbox.

#### Esportare singoli oggetti

È possibile eseguire il backup di singoli oggetti in un pacchetto in uno dei modi seguenti. Mentre queste guide si concentrano sull’aggiunta di uno schema nel pacchetto, gli stessi passaggi si applicano ad altri oggetti, come set di dati, tipi di pubblico o percorsi.

- Aggiungi un singolo oggetto a un nuovo pacchetto seguendo la [guida all&#39;aggiunta di oggetti](../ui/sandbox-tooling.md#add-object-to-a-new-package) della guida degli strumenti sandbox.
- Aggiungi un singolo oggetto a un pacchetto di backup esistente seguendo la [guida agli strumenti sandbox](../ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish), assicurandoti di pubblicare le modifiche.
- Crea un pacchetto con più oggetti vuoto a cui aggiungere oggetti, seguendo la guida riportata di seguito.

##### Creazione di un pacchetto con più oggetti

Ad Experience Platform, seleziona **[!UICONTROL Sandbox]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Pacchetti]**. Per iniziare a creare un nuovo pacchetto, seleziona **[!UICONTROL Crea pacchetto]** dall&#39;angolo in alto a destra.

![Scheda Pacchetti nel dashboard delle sandbox con l&#39;opzione Crea pacchetto evidenziata.](../images/use-cases/create-package.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea pacchetto]**. Scegliere **[!UICONTROL Seleziona oggetti]**, quindi selezionare **[!UICONTROL Seleziona]**.

![Finestra di dialogo Crea pacchetto con gli oggetti Select e l&#39;opzione Select evidenziati.](../images/use-cases/create-package-select-objects.png)

Selezionare l&#39;opzione **[!UICONTROL Oggetti multipli]**. Ora devi fornire un nome per il nuovo pacchetto. Immetti il nome desiderato nel campo di testo **[!UICONTROL Nome pacchetto]**. Al termine, selezionare **[!UICONTROL Crea]**.

![La finestra di dialogo Crea pacchetto con più oggetti selezionati e il nome del pacchetto &quot;Backup&quot; compilato.](../images/use-cases/name-multi-object.png)

Il nuovo pacchetto con più oggetti è stato creato e disponibile nel dashboard [!UICONTROL Pacchetti]. Seleziona il pacchetto dall’elenco.

![Il dashboard Pacchetti con il pacchetto denominato Backup evidenziato.](../images/use-cases/package-created.png)

Vengono visualizzate le informazioni e il contenuto del pacchetto. Attualmente, non ci sono oggetti nel nostro nuovo pacchetto. Per iniziare ad aggiungere oggetti, seguire la guida in [aggiunta di oggetti a un pacchetto esistente](../ui/sandbox-tooling.md#add-object-to-a-new-package).

### Creare nuove versioni del pacchetto di backup in base alle esigenze

Dopo aver creato il primo pacchetto di backup per la sandbox, puoi crearne di nuove versioni man mano che cambiano le configurazioni della sandbox.

Anche se è possibile aggiungere nuovi oggetti al pacchetto di backup esistente, si consiglia di creare nuovi pacchetti per supportare il controllo delle versioni nella sandbox. In questo modo puoi reimpostare e importare facilmente qualsiasi versione precedente delle sandbox mentre continui a sviluppare.

### Verifica gli utilizzi correnti in base ai diritti di licenza

Ora che il pacchetto di backup è pronto, puoi reimpostare la sandbox per reimpostare l’utilizzo. È necessario monitorare regolarmente l’utilizzo in modo da poter regolare i diritti di licenza o ripristinare la sandbox in base alle esigenze. Per ulteriori informazioni sul dashboard utilizzo licenze, consultare la [guida utilizzo licenze](../../dashboards/guides/license-usage.md).

### Ripristina la sandbox

A questo punto, puoi ripristinare la sandbox in modo sicuro, supponendo che soddisfi i parametri necessari. Segui le [istruzioni per reimpostare una guida alla sandbox](../ui/user-guide.md#reset-a-sandbox) per iniziare a reimpostare la sandbox, assicurandoti di leggere i casi di avviso che potrebbero impedirti di reimpostare la sandbox.

### Importa il pacchetto di backup appena creato nella sandbox reimpostata

Ora che hai reimpostato la sandbox, puoi utilizzare il pacchetto di backup creato. Segui la [guida agli strumenti sandbox](../ui/sandbox-tooling.md#import-a-package-to-a-target-sandbox) per un processo dettagliato sull&#39;importazione di un pacchetto nella sandbox di destinazione.

## Altri casi d’uso raggiunti tramite gli strumenti sandbox: {#other-use-cases}

Esplora altri casi d’uso abilitati tramite gli strumenti sandbox:

- [Abilitare un centro di eccellenza utilizzando gli strumenti sandbox](./center-of-excellence.md)
