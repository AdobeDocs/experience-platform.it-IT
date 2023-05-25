---
title: Guida end-to-end alla governance dei dati
description: Segui il processo completo per applicare i vincoli di utilizzo dei dati per campi e set di dati in Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: 9f3fa696ed60ce85fa93515e39716d89ec80f1ec
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 0%

---

# Guida end-to-end alla governance dei dati

Per controllare quali azioni di marketing possono essere eseguite su determinati set di dati e campi in Adobe Experience Platform, è necessario impostare quanto segue:

1. [Applica etichette](#labels) ai campi degli schemi o all’intero set di dati, di cui desideri limitare l’utilizzo.
1. [Configurare e abilitare i criteri di governance dei dati](#policy) che determinano quali tipi di dati con etichetta possono essere utilizzati per determinate azioni di marketing.
1. [Applicare azioni di marketing alle destinazioni](#destinations) per indicare quali criteri si applicano ai dati inviati a tali destinazioni.

Dopo aver completato la configurazione delle etichette, dei criteri di governance e delle azioni di marketing, puoi [verifica l’applicazione dei criteri](#test) per garantire che funzioni come previsto.

Questa guida illustra l’intero processo di configurazione e applicazione di un criterio di governance dei dati nell’interfaccia utente di Platform. Per informazioni più dettagliate sulle funzioni utilizzate in questa guida, consulta la documentazione di panoramica sui seguenti argomenti:

* [Governance dei dati Adobe Experience Platform](./home.md)
* [Etichette di utilizzo dati](./labels/overview.md)
* [Criteri di utilizzo dei dati](./policies/overview.md)
* [Applicazione dei criteri](./enforcement/overview.md)

>[!NOTE]
>
>Questa guida illustra come impostare e applicare i criteri per l’utilizzo o l’attivazione dei dati in Experience Platform. Se stai cercando di limitare **accesso** ai dati stessi per alcuni utenti di Platform all’interno della tua organizzazione, consulta la guida end-to-end su [controllo degli accessi basato su attributi](../access-control/abac/end-to-end-guide.md) invece. Anche il controllo dell’accesso basato su attributi utilizza etichette e criteri, ma per un caso d’uso diverso dalla governance dei dati.

## Applica etichette {#labels}

>[!IMPORTANT]
>
>Le etichette non possono più essere applicate ai singoli campi a livello di set di dati. Questo flusso di lavoro è stato dichiarato obsoleto a favore dell’applicazione di etichette a livello di schema. Tuttavia, puoi ancora etichettare un intero set di dati. Eventuali etichette applicate in precedenza ai singoli campi dei set di dati continueranno a essere supportate tramite l’interfaccia utente di Platform fino al 31 maggio 2024. Per garantire che le etichette siano coerenti in tutti gli schemi, tutte le etichette precedentemente associate ai campi a livello di set di dati devono essere migrate a livello di schema da te nel corso dell’anno successivo. Consulta la sezione su [migrazione di etichette applicate in precedenza](#migrate-labels) per istruzioni su come eseguire questa operazione.

È possibile [applicare etichette a uno schema](#schema-labels) in modo che tutti i set di dati basati su tale schema ereditino le stesse etichette. Questo consente di gestire le etichette per la governance dei dati, il consenso e il controllo degli accessi in un’unica posizione. Applicando vincoli di utilizzo dei dati a livello di schema, l’effetto si propaga a valle a tutti i set di dati basati su tale schema. Le etichette applicate a livello di campo dello schema supportano casi di utilizzo di governance dei dati e sono rilevabili nell’area di lavoro Set di dati [!UICONTROL Governance dei dati] sotto il [!UICONTROL Nome campo] come etichette di sola lettura.

Se è presente un set di dati specifico su cui desideri applicare vincoli di utilizzo dei dati, puoi [applica le etichette direttamente a tale set di dati](#dataset-labels) o campi specifici all’interno di tale set di dati.

In alternativa, è possibile: [applicare etichette a uno schema](#schema-labels) in modo che tutti i set di dati basati su tale schema ereditino le stesse etichette.

>[!NOTE]
>
>Per ulteriori informazioni sulle diverse etichette di utilizzo dei dati e sul loro utilizzo previsto, vedi [riferimento etichette utilizzo dati](./labels/reference.md). Se le etichette core disponibili non coprono tutti i casi d’uso desiderati, puoi [definire etichette personalizzate](./labels/user-guide.md#manage-custom-labels) anche.

### Applicare etichette a un intero set di dati {#dataset-labels}

Seleziona **[!UICONTROL Set di dati]** nella barra di navigazione a sinistra, seleziona il nome del set di dati a cui desideri applicare le etichette. Facoltativamente, puoi utilizzare il campo di ricerca per limitare l’elenco dei set di dati visualizzati.

![Scheda Sfoglia dell’area di lavoro Set di dati con Set di dati ed evidenziata una riga di set di dati.](./images/e2e/select-dataset.png)

Viene visualizzata la vista dei dettagli per il set di dati. Seleziona la **[!UICONTROL Governance dei dati]** per visualizzare un elenco dei campi del set di dati ed eventuali etichette già applicate. Seleziona l’icona a forma di matita per modificare le etichette dei set di dati.

![Scheda Governance dei dati per il set di dati Membri fedeltà con l’icona a forma di matita evidenziata.](./images/e2e/edit-dataset-labels.png)

Il [!UICONTROL Modifica etichette di governance] viene visualizzata. Seleziona l’etichetta di governance appropriata e seleziona **[!UICONTROL Salva]**.

![La finestra di dialogo Modifica etichette di governance con la casella di controllo dell’etichetta e Salva evidenziata.](./images/e2e/edit-dataset-governance-labels.png)

### Applicare le etichette a uno schema {#schema-labels}

Seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra, seleziona lo schema a cui desideri aggiungere le etichette dall’elenco.

>[!TIP]
>
>Se non sai quale schema si applica a un particolare set di dati, seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra, seleziona quindi il collegamento sotto al **[!UICONTROL Schema]** per il set di dati desiderato. Selezionare il nome dello schema nel popover visualizzato per aprire lo schema nell&#39;Editor schema.
>
>![Immagine che mostra un collegamento allo schema di un set di dati](./images/e2e/schema-from-dataset.png)

La struttura dello schema viene visualizzata nell&#39;Editor di schema. Da qui, seleziona la **[!UICONTROL Etichette]** per visualizzare una vista a elenco dei campi dello schema e delle etichette già applicate. Seleziona le caselle di controllo accanto ai campi a cui desideri aggiungere le etichette, quindi seleziona **[!UICONTROL Applica etichette di accesso e governance dei dati]** nella barra a destra.

![La scheda Etichette dell’area di lavoro Schema con un singolo campo schema selezionato ed evidenziate Applica etichette di accesso e governance dei dati.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Se desideri aggiungere etichette a tutti i campi dello schema, seleziona l’icona a forma di matita nella riga superiore.
>
>![Immagine che mostra l’icona della matita selezionata dalla vista etichette schema](./images/e2e/label-whole-schema.png)

Il [!UICONTROL Applica etichette di accesso e governance dei dati] viene visualizzata. Seleziona le etichette da applicare al campo schema selezionato. Al termine, seleziona **[!UICONTROL Salva]**.

![La finestra di dialogo Applica etichette di accesso e governance dei dati mostra più etichette aggiunte a un campo schema.](./images/e2e/save-schema-labels.png)

Continua a seguire i passaggi precedenti per applicare le etichette a campi diversi (o a schemi diversi), in base alle esigenze. Al termine, puoi continuare con il passaggio successivo di [abilitazione dei criteri di governance dei dati](#policy).

### Etichette di migrazione applicate in precedenza a livello di set di dati {#migrate-labels}

Seleziona **[!UICONTROL Set di dati]** nel menu di navigazione a sinistra, seleziona il nome del set di dati da cui desideri eseguire la migrazione delle etichette. Facoltativamente, puoi utilizzare il campo di ricerca per limitare l’elenco dei set di dati visualizzati.

![Scheda Sfoglia dell’area di lavoro Set di dati con il set di dati Membri fedeltà evidenziato.](./images/e2e/select-dataset.png)

Viene visualizzata la vista dei dettagli per il set di dati. Seleziona la **[!UICONTROL Governance dei dati]** per visualizzare un elenco dei campi del set di dati ed eventuali etichette già applicate. Seleziona l’icona Annulla accanto a qualsiasi etichetta che desideri rimuovere da un campo. Viene visualizzata una finestra di dialogo di conferma, seleziona [!UICONTROL Rimuovi etichetta] per confermare le scelte effettuate.

![Scheda Governance dei dati dell’area di lavoro Set di dati con un’etichetta per un campo evidenziato per la rimozione.](./images/e2e/remove-label.png)

Dopo aver rimosso l’etichetta dal campo del set di dati, passa all’Editor di schema per aggiungerla allo schema. Le istruzioni su come eseguire questa operazione, sono reperibili nella sezione [sezione sull’applicazione di etichette a uno schema](#schema-labels).

>[!TIP]
>
>Puoi selezionare il nome dello schema nella barra a destra, seguito dal collegamento nella finestra di dialogo che consente di passare allo schema appropriato.
>![Scheda Governance dei dati dell’area di lavoro Set di dati con il nome dello schema nella barra laterale e il collegamento della finestra di dialogo evidenziati.](./images/e2e/navigate-to-schema.png)

Dopo aver eseguito la migrazione delle etichette necessarie, assicurati di disporre della [criteri di governance dei dati abilitati](#policy).

## Abilitare i criteri di governance dei dati {#policy}

Dopo aver applicato le etichette agli schemi e/o ai set di dati, puoi creare criteri di governance dei dati che limitano le azioni di marketing per le quali è possibile utilizzare determinate etichette.

Seleziona **[!UICONTROL Criteri]** nella barra di navigazione a sinistra puoi visualizzare un elenco dei criteri di base definiti da Adobe, nonché di tutti i criteri personalizzati creati in precedenza dall’organizzazione.

A ogni etichetta core è associato un criterio core che, se attivato, applica i vincoli di attivazione appropriati ai dati che la contengono. Per abilitare un criterio principale, selezionalo dall’elenco, quindi seleziona il **[!UICONTROL Stato criterio]** passa a **[!UICONTROL Abilitato]**.

![Immagine che mostra un criterio principale attivato nell’interfaccia utente di](./images/e2e/enable-core-policy.png)

Se i criteri di base disponibili non coprono tutti i casi d’uso (ad esempio quando utilizzi etichette personalizzate definite nell’organizzazione), puoi definire un criterio personalizzato. Dalla sezione **[!UICONTROL Criteri]** workspace, seleziona **[!UICONTROL Crea criterio]**.

![Immagine che mostra [!UICONTROL Crea criterio] pulsante selezionato nell’interfaccia utente](./images/e2e/create-policy.png)

Viene visualizzato un messaggio che richiede di selezionare il tipo di criterio che si desidera creare. Seleziona **[!UICONTROL Criteri di governance dei dati]**, quindi seleziona **[!UICONTROL Continua]**.

![Immagine che mostra [!UICONTROL Criteri di governance dei dati] opzione selezionata](./images/e2e/governance-policy.png)

Nella schermata successiva, fornisci **[!UICONTROL Nome]** e opzionale **[!UICONTROL Descrizione]** per la politica. Nella tabella seguente, seleziona le etichette che desideri che vengano controllate da questo criterio. In altre parole, si tratta delle etichette che il criterio impedirà di utilizzare per le azioni di marketing specificate nel passaggio successivo.

Se selezioni più etichette, puoi utilizzare le opzioni nella barra a destra per determinare se tutte le etichette devono essere presenti affinché il criterio possa applicare restrizioni d’uso, o se solo una delle etichette deve essere presente. Al termine, seleziona **[!UICONTROL Successivo]**.

![Immagine che mostra la configurazione di base del criterio completata nell’interfaccia utente](./images/e2e/configure-policy.png)

Nella schermata successiva, seleziona le azioni di marketing per le quali questo criterio limiterà l’utilizzo delle etichette selezionate in precedenza. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![Immagine che mostra l’azione di marketing assegnata a un criterio nell’interfaccia utente](./images/e2e/select-marketing-action.png)

La schermata finale mostra un riepilogo dei dettagli del criterio e le azioni che limiterà per quali etichette. Seleziona **[!UICONTROL Fine]** per creare il criterio.

![Immagine che mostra la configurazione dei criteri da confermare nell’interfaccia utente](./images/e2e/confirm-policy.png)

Il criterio viene creato, ma è impostato su [!UICONTROL Disabilitato] per impostazione predefinita. Selezionare il criterio dall&#39;elenco e impostare **[!UICONTROL Stato criterio]** passa a **[!UICONTROL Abilitato]** per abilitare il criterio.

![Immagine che mostra il criterio creato abilitato nell’interfaccia utente](./images/e2e/enable-created-policy.png)

Continua a seguire i passaggi precedenti per creare e abilitare i criteri richiesti prima di passare al passaggio successivo.

## Gestire le azioni di marketing per le destinazioni {#destinations}

Affinché i criteri abilitati possano determinare con precisione quali dati possono essere attivati su una destinazione, devi assegnare a tale destinazione specifiche azioni di marketing.

Si consideri, ad esempio, un criterio abilitato che impedisca qualsiasi dato contenente un `C2` L’etichetta non può essere utilizzata per l’azione di marketing &quot;[!UICONTROL Esporta a terze parti]&quot;. Quando si attivano i dati in una destinazione, il criterio controlla quali azioni di marketing sono presenti nella destinazione. Se &quot;[!UICONTROL Esporta a terze parti]&quot;, tentativo di attivazione dei dati con un `C2` l’etichetta genera una violazione dei criteri. Se &quot;[!UICONTROL Esporta a terze parti]&quot; non è presente, il criterio non viene applicato per la destinazione e i dati con `C2` le etichette possono essere attivate liberamente.

Quando [connessione di una destinazione nell’interfaccia utente](../destinations/ui/connect-destination.md), il **[!UICONTROL Governance]** Questo passaggio nel flusso di lavoro consente di selezionare le azioni di marketing applicabili a questa destinazione, che alla fine determinano quali criteri di governance dei dati vengono applicati alla destinazione.

![Immagine che mostra le azioni di marketing selezionate per una destinazione](./images/e2e/destination-marketing-actions.png)

## Verifica applicazione dei criteri {#test}

Dopo aver assegnato i dati con l’etichetta, abilitato i criteri di governance dei dati e le azioni di marketing alle destinazioni, puoi verificare se i criteri vengono applicati come previsto.

Se si impostano correttamente le impostazioni, quando si tenta di attivare dati limitati dai criteri, l&#39;attivazione viene automaticamente negata e viene visualizzato un messaggio di violazione dei criteri, in cui vengono descritte informazioni dettagliate sulla derivazione dei dati relative alla causa della violazione.

Vedi il documento su [applicazione automatica delle policy](./enforcement/auto-enforcement.md) per informazioni dettagliate su come interpretare i messaggi di violazione dei criteri.

## Passaggi successivi

Questa guida descrive i passaggi necessari per configurare e applicare i criteri di governance dei dati nei flussi di lavoro di attivazione. Per informazioni più dettagliate sui componenti Governance dei dati coinvolti in questa guida, consulta la seguente documentazione:

* [Etichette di utilizzo dati](./labels/overview.md)
* [Criteri di utilizzo dei dati](./policies/overview.md)
* [Applicazione dei criteri](./enforcement/overview.md)
