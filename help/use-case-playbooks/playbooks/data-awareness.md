---
solution: Experience Platform
title: Panoramica della consapevolezza dei dati nei playbook dei casi d’uso
description: Scopri come accelerare il time-to-value copiando le risorse generate nella sandbox end inspirational in altre sandbox.
role: Developer
exl-id: 537eff13-f5fe-4cc9-9769-ab47b3cecda7
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Pubblicare risorse generate dal playbook in altre sandbox {#publish-to-other-sandboxes}

I playbook per casi d’uso sono modelli di marketing progettati per generare risorse come tipi di pubblico, schemi o percorsi per i casi d’uso di marketing comuni. Puoi testare le risorse create dai playbook nella sandbox ispiratrice e, quando sei pronto, puoi importare le risorse in altre sandbox di sviluppo per ulteriori test con i dati disponibili in tali sandbox. Una volta superato il test, puoi spostare le risorse dalle sandbox di sviluppo a quelle di produzione.

Tuttavia, in alcuni casi, è possibile che siano già stati impostati schemi, campi e gruppi di campi personalizzati in altre sandbox di sviluppo. In questo modo alcune delle risorse generate dai modelli del caso d’uso, ad esempio i percorsi, potrebbero risultare incompatibili con i dati. Per informazioni su come utilizzare la funzionalità di riconoscimento dei dati per allineare e integrare meglio le risorse generate con le risorse esistenti, leggi questa esercitazione.

## Prerequisiti {#prerequisites}

Prima di leggere questa esercitazione, sfoglia [modelli di playbook per casi d’uso disponibili](/help/use-case-playbooks/playbooks/discover.md#search-and-filter) e [creare un’istanza](/help/use-case-playbooks/playbooks/create-share-reuse.md) di un playbook preferito.

La creazione di un’istanza genera un set di risorse come percorsi, segmenti, schemi e messaggi nella sandbox ispiratrice. Continua a leggere per scoprire come copiare queste risorse in altre sandbox.

### Creare e pubblicare un pacchetto {#create-publish-package}

>[!NOTE]
>
> Puoi importare i pacchetti solo in altre sandbox di sviluppo. Dopo aver apportato tutte le modifiche o gli aggiornamenti necessari, puoi importare le risorse o i pacchetti da tali sandbox di sviluppo in produzione. Non è possibile importare direttamente dalle sandbox di Playbook di casi d’uso in produzione.

1. Per importare oggetti dalla sandbox di ispirazione in un’altra sandbox, individua l’istanza desiderata di un playbook con casi d’uso e seleziona **[!UICONTROL Pubblica in un’altra sandbox]** per esportare gli artefatti come pacchetto.

   ![GIF che mostra le diverse istanze del caso d’uso](/help/use-case-playbooks/assets/playbooks/data-awareness/browse-to-existing-instances-of-playbook.gif)

2. Dopo aver selezionato **[!UICONTROL Pubblica in un’altra sandbox]** viene visualizzato un modale. Inserisci il nome e la descrizione facoltativa e seleziona **[!UICONTROL Crea]**. Questo passaggio raggruppa le risorse generate in un pacchetto che può essere importato in una sandbox diversa.

   ![Una finestra modale per la creazione di un pacchetto](/help/use-case-playbooks/assets/playbooks/data-awareness/create-package-modal.png)

3. Accedi a **Sandbox** nella barra di navigazione a sinistra e seleziona la **Pacchetti** , trovare il pacchetto e pubblicarlo. Per pubblicare un pacchetto in stato di bozza, segui i passaggi descritti in [strumenti sandbox](/help/sandboxes/ui/sandbox-tooling.md#add-an-object-to-an-existing-package-and-publish) documento.

   ![Pacchetto in stato bozza o non pubblicato](/help/use-case-playbooks/assets/playbooks/data-awareness/draft-mode.png)

   ![Pubblicazione del pacchetto](/help/use-case-playbooks/assets/playbooks/data-awareness/publish-draft.png)

4. Una volta completata la pubblicazione, nella pagina di navigazione dei pacchetti dovresti trovare **+** accanto al nome.

   ![Scheda Pacchetti nella pagina Sandbox](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

   >[!NOTE]
   >
   > Poiché non è possibile importare il pacchetto mentre è ancora in modalità bozza, aprire la pagina dei dettagli del pacchetto e pubblicare il pacchetto.

5. Seleziona la **+** controllare e avviare il flusso di lavoro per importare in **[!UICONTROL Sandbox di Target]**. Seleziona una sandbox di destinazione e conferma il nome del pacchetto da importare utilizzando il menu a discesa. Aggiungere i dettagli del job, ad esempio il nome e la descrizione, prima di procedere al passaggio successivo.

   ![Avvia il flusso di lavoro di importazione, seleziona la destinazione, conferma il pacchetto, aggiungi i dettagli del processo.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-import-settings.png)

6. In **[!UICONTROL Visualizza dipendenze]** fase, puoi mappare gli schemi e copiare altre risorse dalla sandbox inspirational alla sandbox target. Il **[!UICONTROL Fine]** è disattivato finché non mappi ogni schema.

   ![Mappa gli schemi nel passaggio &quot;Visualizza dipendenze&quot;, abilitando il pulsante Fine.](/help/use-case-playbooks/assets/playbooks/data-awareness/import-package-view-dependencies.png)

### Mappare gli schemi {#map-schemas}

1. Mappa il primo schema. La finestra di dialogo di mappatura dello schema visualizza un elenco a discesa per selezionare lo schema di destinazione. Se lo schema di origine è uno schema di profilo, non vi sono altre opzioni dello schema di destinazione oltre a [schema del profilo di unione individuale](/help/xdm/classes/individual-profile.md). Puoi vedere i consigli di mappatura generati automaticamente tra i dati di origine e i campi di destinazione quando la pagina viene visualizzata per la prima volta. Puoi modificare le mappature selezionando il campo di destinazione e quindi un nuovo campo. Se modifichi le mappature suggerite, utilizza **Convalida** per convalidare le nuove mappature e visualizzare gli eventuali errori collegati alle nuove mappature. Seleziona **Salva** una volta completata la mappatura.

   ![Finestra di dialogo di mappatura dello schema con un menu a discesa per selezionare uno schema di destinazione.](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-fields.png)

2. Continua a mappare tutti i campi negli schemi. Se lo schema è un [schema evento](/help/xdm/classes/experienceevent.md), la finestra di dialogo mostra un elenco a discesa in cui puoi visualizzare tutti gli schemi dell’evento nella sandbox di target.

   ![Seleziona uno schema di destinazione dal menu a discesa](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-event-schema.png)

3. Seleziona uno schema dagli schemi disponibili nel **Sandbox di Target**.

   ![Seleziona uno schema](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-available-schemas.png)

4. Completa la mappatura e seleziona **Salva**.

   ![Salva mappatura](/help/use-case-playbooks/assets/playbooks/data-awareness/map-to-existing-modal.png)

5. Dopo aver completato la mappatura di tutti i campi negli schemi, seleziona **Fine** per completare il flusso di lavoro di importazione

   ![Completare il flusso](/help/use-case-playbooks/assets/playbooks/data-awareness/complete-flow.png)

   >[!NOTE]
   >
   > Non puoi modificare le risorse a eccezione degli schemi, in quanto si tratta di una sandbox illuminante, ma vengono visualizzati in quanto dipendenze del pacchetto.

### Stato importazione {#import-status}

1. Viene automaticamente reindirizzato al [**Importazioni**](/help/sandboxes/ui/sandbox-tooling.md#view-import-details) pagina in cui puoi visualizzare l’avanzamento dell’importazione.

   ![Pagina che mostra l’avanzamento dell’importazione](/help/use-case-playbooks/assets/playbooks/data-awareness/import-progress.png)

2. Durante l’importazione del pacchetto, le relative risorse vengono create nella sandbox di destinazione. Una volta completati, fanno riferimento ai campi mappati durante il processo di importazione. Il processo è ora completo e le risorse della sandbox che ispira sono ora presenti anche nella sandbox di destinazione per il test.

   ![Risorse generate nella sandbox di destinazione](/help/use-case-playbooks/assets/playbooks/data-awareness/packages.png)

## Passaggi successivi

Dopo aver letto questa guida, ora hai una migliore comprensione di come sfruttare i playbook dei casi d’uso insieme a [strumenti sandbox](/help/sandboxes/ui/sandbox-tooling.md#monitor-import-jobs-and-view-import-objects-details) per creare percorsi eseguibili che fanno riferimento agli schemi. Ulteriori informazioni sulla [Casi d’uso di Real-Time CDP](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md).
