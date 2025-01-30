---
title: Abilitare un centro di eccellenza utilizzando gli strumenti sandbox
description: Abilita un centro di eccellenza utilizzando gli strumenti sandbox creando un pacchetto "sandbox d’oro" per standardizzare le best practice su più sandbox.
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: d4df5606228347b5fb69fdaa24c637c329099895
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Abilitare un centro di eccellenza utilizzando gli strumenti sandbox

Abilita un centro di eccellenza utilizzando gli strumenti sandbox creando un pacchetto &quot;sandbox d’oro&quot; per standardizzare le best practice su più sandbox.

![Panoramica sull&#39;esportazione di pacchetti tra organizzazioni diverse](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## Perché considerare questo caso d’uso {#why-this-use-case}

Molte grandi aziende o aziende utilizzano più sandbox per diverse organizzazioni, team, aree geografiche o ambienti di sviluppo. Grazie alla potenza di [strumenti sandbox](../ui/sandbox-tooling.md), puoi creare un pacchetto sandbox avanzato per garantire la coerenza, la conformità e l&#39;allineamento degli standard della tua organizzazione su più sandbox.

Questo pacchetto sandbox dorato crea un centro di eccellenza per condividere in modo efficiente le configurazioni chiave. Utilizzando gli strumenti sandbox, puoi importare facilmente il pacchetto tra più sandbox. Puoi anche condividere il pacchetto con altre organizzazioni per garantire una coerenza diffusa.

Per creare un pacchetto sandbox personalizzato, segui i passaggi descritti in questo caso d’uso.

## Esempio di settore {#industry-example}

Si consideri, ad esempio, una banca che opera in diverse regioni, come il Nord America, l&#39;Europa e l&#39;Africa. Ogni mercato o area geografica dispone di una propria istanza di Adobe Experience Platform. Questa banca vuole mantenere un modello di dati centralizzato gestito da un team globale di architetti, in cui è possibile distribuire una singola versione del modello di dati in tutti i mercati.

Questa banca sceglie di sfruttare gli strumenti sandbox per creare e mantenere un pacchetto sandbox dorato. Ciò contribuisce all’efficienza dello sviluppo, consente modelli di dati coerenti e garantisce la coerenza in tutte le aree geografiche.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Quando prevedi di creare un centro di eccellenza all’interno della tua organizzazione, considera i seguenti prerequisiti nel processo di pianificazione:

- Identifica le best practice e le configurazioni da includere nel pacchetto.
- Crea una sandbox con tutte le configurazioni rilevanti e convalidate da impostare come sandbox d’oro.
- Se necessario, ottieni l’input delle parti interessate e il consenso sugli standard di base.

### Funzionalità dell’interfaccia utente, componenti della piattaforma e prodotti di Experience Cloud che utilizzerai {#ui-functionality-and-elements}

Per implementare correttamente questo caso d’uso, devi utilizzare più aree di Adobe Experience Platform. Assicurati di disporre delle [autorizzazioni di controllo dell&#39;accesso basate su attributi](../../access-control/abac/overview.md) necessarie per tutte queste aree, oppure chiedi all&#39;amministratore di sistema di concederti le autorizzazioni necessarie.

- [Strumenti sandbox](../ui/sandbox-tooling.md)
- [Gestione sandbox](../ui/user-guide.md)
- [Set di dati](../../catalog/datasets/overview.md)
- [Schemi](../../xdm//home.md)
- [Tipi di pubblico](../../segmentation/home.md)
- [Percorsi da Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

1. Crea la configurazione di base che rappresenta le best practice in una sandbox d’oro. Questo può includere oggetti come set di dati, schemi, tipi di pubblico o percorsi.
2. Utilizzando gli strumenti sandbox, esporta la configurazione in un pacchetto.
3. Importa questo pacchetto in tutte le sandbox pertinenti.
4. Se hai più organizzazioni, condividi questo pacchetto tra le tue organizzazioni.
5. Monitora le importazioni e le esportazioni e tieni traccia delle modifiche tramite i registri di audit.
6. Aggiorna regolarmente la sandbox d’oro con l’evolversi degli standard per garantire che tutte le sandbox rimangano allineate alle best practice.

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a un ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello qui sopra.

### Crea la tua sandbox d’oro

Il primo passo per rendere possibile il centro di eccellenza è creare una sandbox d’oro. Questa sandbox deve contenere le configurazioni della linea di base che rappresentano le best practice. Per creare questa sandbox d&#39;oro, segui la guida su [creazione di una nuova sandbox](../ui/user-guide.md#create-a-new-sandbox) in Experience Platform.

Una volta creata la sandbox, inizia a creare le configurazioni degli oggetti della linea di base, ad esempio [schemi](../../xdm/ui/resources/schemas.md#create-a-new-schema), [set di dati](../../catalog/datasets/user-guide.md#create-a-dataset) o [tipi di pubblico](../../segmentation/ui/segment-builder.md). Prima di continuare, controlla le configurazioni.

### Esportare la sandbox in un pacchetto

Ora che la sandbox contiene le configurazioni degli oggetti della linea di base, può essere esportata in un pacchetto utilizzando gli strumenti della sandbox. Segui la guida sull&#39;[esportazione di un&#39;intera sandbox](../ui/sandbox-tooling.md#export-an-entire-sandbox) per creare il tuo pacchetto sandbox d&#39;oro.

### Importare il pacchetto nelle sandbox pertinenti

Una volta creato il pacchetto, puoi importarlo nelle sandbox pertinenti. La best practice prevede di importare un pacchetto contenente un’intera sandbox in una sandbox vuota. Utilizzando gli strumenti sandbox, puoi [importare facilmente un intero pacchetto sandbox](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) in una sandbox direttamente all&#39;interno di Experience Platform.

### Condivisione di pacchetti tra organizzazioni

Gli strumenti sandbox consentono di condividere i pacchetti creati tra organizzazioni diverse. Segui la [guida alla condivisione dei pacchetti](../../sandboxes/ui/sharing-packages-across-orgs.md) per condividere il tuo pacchetto sandbox d&#39;oro.

### Monitorare le importazioni e le esportazioni tramite i registri di audit

Durante l&#39;importazione o l&#39;esportazione del pacchetto, è possibile monitorare lo stato dei processi utilizzando il dashboard **[!UICONTROL Processi]** in Experience Platform. Per ulteriori informazioni sui processi di monitoraggio, leggere la guida in [monitoraggio dei dettagli di importazione](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### Aggiorna regolarmente la sandbox dorata

Ora che il tuo pacchetto sandbox d’oro è pronto, hai creato un centro di eccellenza standardizzato che puoi continuare a importare in sandbox o a condividere tra le organizzazioni. Man mano che le best practice cambiano e si sviluppano, è importante aggiornare regolarmente le configurazioni degli oggetti della linea di base nella sandbox d’oro. Quando apporti aggiornamenti alla sandbox, puoi creare nuove iterazioni del pacchetto sandbox d’oro seguendo lo stesso processo.

>[!NOTE]
>
> I passaggi precedenti seguono la procedura descritta nell’interfaccia utente di Experience Platform. È possibile seguire gli stessi passaggi utilizzando l’API attraverso vari endpoint. Per informazioni su come effettuare ogni richiesta tramite l&#39;API, consultare la `sandboxes` [guida dell&#39;endpoint](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create) e la `packages` [guida dell&#39;endpoint](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages).

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite gli strumenti sandbox:

- [Eseguire il backup delle configurazioni degli oggetti utilizzando gli strumenti sandbox](./backup-object-configuration.md)
