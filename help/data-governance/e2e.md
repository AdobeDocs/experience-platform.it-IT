---
title: Guida end-to-end alla governance dei dati
description: Segui il processo completo per applicare i vincoli di utilizzo dei dati per campi e set di dati in Adobe Experience Platform.
exl-id: f18ae032-027a-4c97-868b-e04753237c81
source-git-commit: 9f3fa696ed60ce85fa93515e39716d89ec80f1ec
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 1%

---

# Guida end-to-end alla governance dei dati

Per controllare quali azioni di marketing possono essere eseguite su determinati set di dati e campi in Adobe Experience Platform, è necessario impostare quanto segue:

1. [Applica etichette](#labels) ai campi degli schemi o a interi set di dati di cui vuoi limitare l&#39;utilizzo.
1. [Configura e abilita i criteri di governance dei dati](#policy) che determinano quali tipi di dati con etichetta possono essere utilizzati per determinate azioni di marketing.
1. [Applica azioni di marketing alle destinazioni](#destinations) per indicare i criteri applicabili ai dati inviati a tali destinazioni.

Dopo aver completato la configurazione delle etichette, dei criteri di governance e delle azioni di marketing, puoi [verificare l&#39;applicazione dei criteri](#test) per assicurarti che funzioni come previsto.

Questa guida illustra l’intero processo di configurazione e applicazione di un criterio di governance dei dati nell’interfaccia utente di Platform. Per informazioni più dettagliate sulle funzioni utilizzate in questa guida, consulta la documentazione di panoramica sui seguenti argomenti:

* [Governance dei dati Adobe Experience Platform](./home.md)
* [Etichette di utilizzo dei dati](./labels/overview.md)
* [Criteri di utilizzo dei dati](./policies/overview.md)
* [Applicazione dei criteri](./enforcement/overview.md)

>[!NOTE]
>
>Questa guida illustra come impostare e applicare i criteri per l’utilizzo o l’attivazione dei dati in Experience Platform. Se stai tentando di limitare l&#39;**accesso** ai dati stessi per alcuni utenti di Platform all&#39;interno della tua organizzazione, consulta invece la guida end-to-end sul [controllo dell&#39;accesso basato su attributi](../access-control/abac/end-to-end-guide.md). Anche il controllo dell’accesso basato su attributi utilizza etichette e criteri, ma per un caso d’uso diverso dalla governance dei dati.

## Applica etichette {#labels}

>[!IMPORTANT]
>
>Le etichette non possono più essere applicate ai singoli campi a livello di set di dati. Questo flusso di lavoro è stato dichiarato obsoleto a favore dell’applicazione di etichette a livello di schema. Tuttavia, puoi ancora etichettare un intero set di dati. Eventuali etichette applicate in precedenza ai singoli campi dei set di dati continueranno a essere supportate tramite l’interfaccia utente di Platform fino al 31 maggio 2024. Per garantire che le etichette siano coerenti in tutti gli schemi, tutte le etichette precedentemente associate ai campi a livello di set di dati devono essere migrate a livello di schema da te nel corso dell’anno successivo. Per istruzioni su come eseguire questa operazione, consulta la sezione sulla [migrazione delle etichette applicate in precedenza](#migrate-labels).

È possibile [applicare etichette a uno schema](#schema-labels) in modo che tutti i set di dati basati su tale schema ereditino le stesse etichette. Questo consente di gestire le etichette per la governance dei dati, il consenso e il controllo degli accessi in un’unica posizione. Applicando vincoli di utilizzo dei dati a livello di schema, l’effetto si propaga a valle a tutti i set di dati basati su tale schema. Le etichette applicate a livello di campo dello schema supportano casi di utilizzo di governance dei dati e sono individuabili nell&#39;area di lavoro Set di dati [!UICONTROL Scheda Governance dei dati] nella colonna [!UICONTROL Nome campo] come etichette di sola lettura.

Se è presente un set di dati specifico su cui si desidera applicare vincoli di utilizzo dei dati, è possibile [applicare etichette direttamente a tale set di dati](#dataset-labels) o a campi specifici all&#39;interno di tale set di dati.

In alternativa, è possibile [applicare etichette a uno schema](#schema-labels) in modo che tutti i set di dati basati su tale schema ereditino le stesse etichette.

>[!NOTE]
>
>Per ulteriori informazioni sulle diverse etichette di utilizzo dei dati e sull&#39;uso previsto, vedere il [riferimento etichette di utilizzo dei dati](./labels/reference.md). Se le etichette di base disponibili non coprono tutti i casi d&#39;uso desiderati, puoi [definire anche etichette personalizzate](./labels/user-guide.md#manage-custom-labels).

### Applicare etichette a un intero set di dati {#dataset-labels}

Seleziona **[!UICONTROL Set di dati]** nell&#39;area di navigazione a sinistra, quindi seleziona il nome del set di dati a cui desideri applicare le etichette. Facoltativamente, puoi utilizzare il campo di ricerca per limitare l’elenco dei set di dati visualizzati.

![Scheda Sfoglia dell&#39;area di lavoro Set di dati con Set di dati ed evidenziata una riga di set di dati.](./images/e2e/select-dataset.png)

Viene visualizzata la vista dei dettagli per il set di dati. Seleziona la scheda **[!UICONTROL Governance dei dati]** per visualizzare un elenco dei campi del set di dati ed eventuali etichette già applicate. Seleziona l’icona a forma di matita per modificare le etichette dei set di dati.

![Scheda Governance dei dati per il set di dati Membri fedeltà con l&#39;icona a forma di matita evidenziata.](./images/e2e/edit-dataset-labels.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Modifica etichette di governance]. Seleziona l&#39;etichetta di governance appropriata e seleziona **[!UICONTROL Salva]**.

![La finestra di dialogo Modifica etichette di governance con la casella di controllo dell&#39;etichetta e Salva evidenziato.](./images/e2e/edit-dataset-governance-labels.png)

### Applicare le etichette a uno schema {#schema-labels}

Seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra, quindi seleziona dall&#39;elenco lo schema a cui desideri aggiungere le etichette.

>[!TIP]
>
>Se non si è sicuri di quale schema si applichi a un particolare set di dati, selezionare **[!UICONTROL Set di dati]** nell&#39;area di navigazione a sinistra, quindi selezionare il collegamento nella colonna **[!UICONTROL Schema]** per il set di dati desiderato. Selezionare il nome dello schema nel popover visualizzato per aprire lo schema nell&#39;Editor schema.
>
>![Immagine che mostra un collegamento allo schema di un set di dati](./images/e2e/schema-from-dataset.png)

La struttura dello schema viene visualizzata nell&#39;Editor di schema. Da qui, seleziona la scheda **[!UICONTROL Etichette]** per visualizzare una vista a elenco dei campi dello schema e delle etichette già applicate. Seleziona le caselle di controllo accanto ai campi a cui desideri aggiungere le etichette, quindi seleziona **[!UICONTROL Applica etichette di accesso e governance dei dati]** nella barra a destra.

![La scheda Etichette dell&#39;area di lavoro dello schema con un singolo campo dello schema selezionato ed evidenziate Applica etichette di accesso e governance dei dati.](./images/e2e/schema-field-label.png)

>[!NOTE]
>
>Se desideri aggiungere etichette a tutti i campi dello schema, seleziona l’icona a forma di matita nella riga superiore.
>
>![Immagine che mostra l&#39;icona della matita selezionata dalla vista delle etichette dello schema](./images/e2e/label-whole-schema.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Applica etichette di accesso e governance dei dati]. Seleziona le etichette da applicare al campo schema selezionato. Al termine, selezionare **[!UICONTROL Salva]**.

![La finestra di dialogo Applica etichette di accesso e governance dei dati mostra più etichette aggiunte a un campo schema.](./images/e2e/save-schema-labels.png)

Continua a seguire i passaggi precedenti per applicare le etichette a campi diversi (o a schemi diversi), in base alle esigenze. Al termine, puoi continuare con il passaggio successivo di [abilitazione dei criteri di governance dei dati](#policy).

### Etichette di migrazione applicate in precedenza a livello di set di dati {#migrate-labels}

Seleziona **[!UICONTROL Set di dati]** nell&#39;area di navigazione a sinistra, quindi seleziona il nome del set di dati da cui desideri eseguire la migrazione delle etichette. Facoltativamente, puoi utilizzare il campo di ricerca per limitare l’elenco dei set di dati visualizzati.

![Scheda Sfoglia dell&#39;area di lavoro Set di dati con il set di dati Membri fedeltà evidenziato.](./images/e2e/select-dataset.png)

Viene visualizzata la vista dei dettagli per il set di dati. Seleziona la scheda **[!UICONTROL Governance dei dati]** per visualizzare un elenco dei campi del set di dati ed eventuali etichette già applicate. Seleziona l’icona Annulla accanto a qualsiasi etichetta che desideri rimuovere da un campo. Viene visualizzata una finestra di dialogo di conferma. Selezionare [!UICONTROL Rimuovi etichetta] per confermare le scelte.

![Scheda Governance dei dati dell&#39;area di lavoro Set di dati con un&#39;etichetta per un campo evidenziato per la rimozione.](./images/e2e/remove-label.png)

Dopo aver rimosso l’etichetta dal campo del set di dati, passa all’Editor di schema per aggiungerla allo schema. Le istruzioni su come eseguire questa operazione sono disponibili nella sezione [sull&#39;applicazione di etichette a uno schema](#schema-labels).

>[!TIP]
>
>Puoi selezionare il nome dello schema nella barra a destra, seguito dal collegamento nella finestra di dialogo che consente di passare allo schema appropriato.
>![Scheda Governance dei dati dell&#39;area di lavoro Set di dati con il nome dello schema nella barra laterale e il collegamento della finestra di dialogo evidenziati.](./images/e2e/navigate-to-schema.png)

Dopo aver eseguito la migrazione delle etichette necessarie, verificare di aver abilitato [criteri di governance dei dati corretti](#policy).

## Abilitare i criteri di governance dei dati {#policy}

Dopo aver applicato le etichette agli schemi e/o ai set di dati, puoi creare criteri di governance dei dati che limitano le azioni di marketing per le quali è possibile utilizzare determinate etichette.

Seleziona **[!UICONTROL Criteri]** nella barra di navigazione a sinistra per visualizzare un elenco dei criteri di base definiti da Adobe, nonché di eventuali criteri personalizzati creati in precedenza dall&#39;organizzazione.

A ogni etichetta core è associato un criterio core che, se attivato, applica i vincoli di attivazione appropriati ai dati che la contengono. Per abilitare un criterio di base, selezionalo dall&#39;elenco, quindi seleziona lo stato **[!UICONTROL Criterio]** per passare a **[!UICONTROL Abilitato]**.

![Immagine che mostra un criterio di base abilitato nell&#39;interfaccia utente](./images/e2e/enable-core-policy.png)

Se i criteri di base disponibili non coprono tutti i casi d’uso (ad esempio quando utilizzi etichette personalizzate definite nell’organizzazione), puoi definire un criterio personalizzato. Dall&#39;area di lavoro **[!UICONTROL Criteri]**, selezionare **[!UICONTROL Crea criterio]**.

![Immagine che mostra il pulsante [!UICONTROL Crea criterio] selezionato nell&#39;interfaccia utente](./images/e2e/create-policy.png)

Viene visualizzato un messaggio che richiede di selezionare il tipo di criterio che si desidera creare. Seleziona **[!UICONTROL Criteri di governance dei dati]**, quindi seleziona **[!UICONTROL Continua]**.

![Immagine che mostra l&#39;opzione [!UICONTROL Criteri di governance dei dati] selezionata](./images/e2e/governance-policy.png)

Nella schermata successiva, fornisci **[!UICONTROL Nome]** e **[!UICONTROL Descrizione]** facoltativi per il criterio. Nella tabella seguente, seleziona le etichette che desideri che vengano controllate da questo criterio. In altre parole, si tratta delle etichette che il criterio impedirà di utilizzare per le azioni di marketing specificate nel passaggio successivo.

Se selezioni più etichette, puoi utilizzare le opzioni nella barra a destra per determinare se tutte le etichette devono essere presenti affinché il criterio possa applicare restrizioni d’uso, o se solo una delle etichette deve essere presente. Al termine, selezionare **[!UICONTROL Avanti]**.

![Immagine che mostra la configurazione di base del criterio completata nell&#39;interfaccia utente](./images/e2e/configure-policy.png)

Nella schermata successiva, seleziona le azioni di marketing per le quali questo criterio limiterà l’utilizzo delle etichette selezionate in precedenza. Seleziona **[!UICONTROL Avanti]** per continuare.

![Immagine che mostra un&#39;azione di marketing assegnata a un criterio nell&#39;interfaccia utente](./images/e2e/select-marketing-action.png)

La schermata finale mostra un riepilogo dei dettagli del criterio e le azioni che limiterà per quali etichette. Selezionare **[!UICONTROL Fine]** per creare il criterio.

![Immagine che mostra la configurazione dei criteri da confermare nell&#39;interfaccia utente](./images/e2e/confirm-policy.png)

Il criterio è stato creato, ma è impostato su [!UICONTROL Disabilitato] per impostazione predefinita. Selezionare il criterio dall&#39;elenco e impostare lo stato **[!UICONTROL Criterio]** su **[!UICONTROL Abilitato]** per abilitare il criterio.

![Immagine che mostra il criterio creato abilitato nell&#39;interfaccia utente](./images/e2e/enable-created-policy.png)

Continua a seguire i passaggi precedenti per creare e abilitare i criteri richiesti prima di passare al passaggio successivo.

## Gestire le azioni di marketing per le destinazioni {#destinations}

Affinché i criteri abilitati possano determinare con precisione quali dati possono essere attivati su una destinazione, devi assegnare a tale destinazione specifiche azioni di marketing.

Consideriamo ad esempio un criterio abilitato che impedisce l&#39;utilizzo di dati contenenti un&#39;etichetta `C2` per l&#39;azione di marketing &quot;[!UICONTROL Esporta a terze parti]&quot;. Quando si attivano i dati in una destinazione, il criterio controlla quali azioni di marketing sono presenti nella destinazione. Se &quot;[!UICONTROL Esporta in terze parti]&quot; è presente, il tentativo di attivare i dati con un&#39;etichetta `C2` genera una violazione dei criteri. Se &quot;[!UICONTROL Esporta in terze parti]&quot; non è presente, il criterio non viene applicato per la destinazione e i dati con etichette `C2` possono essere attivati liberamente.

Quando [connetti una destinazione nell&#39;interfaccia utente](../destinations/ui/connect-destination.md), il passaggio **[!UICONTROL Governance]** nel flusso di lavoro ti consente di selezionare le azioni di marketing applicabili a questa destinazione, che alla fine determinano quali criteri di governance dei dati vengono applicati alla destinazione.

![Immagine che mostra le azioni di marketing selezionate per una destinazione](./images/e2e/destination-marketing-actions.png)

## Verifica applicazione dei criteri {#test}

Dopo aver assegnato i dati con l’etichetta, abilitato i criteri di governance dei dati e le azioni di marketing alle destinazioni, puoi verificare se i criteri vengono applicati come previsto.

Se si impostano correttamente le impostazioni, quando si tenta di attivare dati limitati dai criteri, l&#39;attivazione viene automaticamente negata e viene visualizzato un messaggio di violazione dei criteri, in cui vengono descritte informazioni dettagliate sulla derivazione dei dati relative alla causa della violazione.

Per informazioni dettagliate su come interpretare i messaggi di violazione dei criteri, consulta il documento su [applicazione automatica dei criteri](./enforcement/auto-enforcement.md).

## Passaggi successivi

Questa guida descrive i passaggi necessari per configurare e applicare i criteri di governance dei dati nei flussi di lavoro di attivazione. Per informazioni più dettagliate sui componenti Governance dei dati coinvolti in questa guida, consulta la seguente documentazione:

* [Etichette di utilizzo dei dati](./labels/overview.md)
* [Criteri di utilizzo dei dati](./policies/overview.md)
* [Applicazione dei criteri](./enforcement/overview.md)
