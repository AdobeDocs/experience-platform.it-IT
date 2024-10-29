---
title: Condivisione di pacchetti tra organizzazioni tramite strumenti sandbox
description: Scopri come utilizzare gli strumenti Sandbox in Adobe Experience Platform per condividere pacchetti tra diverse organizzazioni.
source-git-commit: 77994c1cdd185cc8a2963c5aa2eb345c8702fe02
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# Condividere pacchetti tra organizzazioni utilizzando gli strumenti sandbox

Migliora la precisione della configurazione nelle sandbox ed esporta e importa facilmente le configurazioni sandbox tra sandbox di diverse organizzazioni con la funzione di strumenti sandbox. Questo documento illustra come utilizzare gli strumenti sandbox in Adobe Experience Platform per condividere pacchetti tra diverse organizzazioni. Esistono due tipi di pacchetti condivisi:

- **Pacchetto privato**

[I pacchetti privati](#private-packages) possono essere condivisi solo con organizzazioni che hanno approvato la richiesta di condivisione dall&#39;organizzazione di origine.

- **Pacchetto pubblico**

[I pacchetti pubblici](#public-packages) sono disponibili per l&#39;importazione senza alcuna approvazione aggiuntiva. Questi pacchetti possono essere condivisi sul sito web, sul blog o sulla piattaforma di un partner. Il payload del pacchetto consente di copiare e incollare i pacchetti da questi canali nell’organizzazione di destinazione.

## Pacchetti privati {#private-packages}

>[!NOTE]
>
>Per avviare e approvare una richiesta di condivisione e condividere pacchetti tra organizzazioni, è necessario disporre dell&#39;autorizzazione di controllo dell&#39;accesso basata su ruolo **condivisione pacchetti**.

Utilizza la funzione Strumenti sandbox per creare partnership, tenere traccia delle statistiche delle richieste di partnership, gestire le partnership esistenti e condividere pacchetti con le organizzazioni partner.

### Creare una richiesta di partnership organizzazione

Per creare una richiesta di partnership organizzazione, passa alla scheda **[!UICONTROL Sandbox]** **[!UICONTROL Organizzazioni partner]**. Selezionare **[!UICONTROL Gestisci organizzazioni partner]**.

![Interfaccia utente sandbox con le schede Organizzazioni partner e Gestisci organizzazioni partner evidenziate.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Nella finestra di dialogo [!UICONTROL Gestione partner pacchetti], immetti l&#39;ID organizzazione in **[!UICONTROL Immetti ID organizzazione]** e premi Invio (Windows) o Ritorno (Mac). L&#39;ID organizzazione viene visualizzato nella sezione **[!UICONTROL ID organizzazione selezionati]** di seguito. Dopo aver aggiunto gli ID, seleziona **[!UICONTROL Conferma]**.

>[!TIP]
>
>È possibile immettere più ID organizzazione alla volta utilizzando elenchi separati da virgole o immettendo ogni ID organizzazione seguito da INVIO.

![Finestra di dialogo Organizzazioni partner del pacchetto con immissione dell&#39;ID organizzazione, ID organizzazione selezionati e conferma evidenziati.](../images/ui/sandbox-tooling/private-enter-org-id.png)

La richiesta di condivisione è stata inviata all&#39;organizzazione partner e si è tornati alla scheda [!UICONTROL Sandbox] **[!UICONTROL Organizzazioni partner]**, in cui è visualizzata la **[!UICONTROL richiesta in uscita]**.

![Scheda Organizzazioni partner con richiesta in uscita evidenziata.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Autorizzare una richiesta di partnership {#authorize-request}

Per autorizzare una richiesta di partnership tra organizzazioni, passa alla scheda [!UICONTROL Sandbox] **[!UICONTROL Organizzazioni partner]**. Selezionare **[!UICONTROL Richiesta in ingresso]**.

![L&#39;interfaccia utente delle sandbox con la scheda Organizzazioni partner e la richiesta in ingresso evidenziata.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Il **[!UICONTROL Stato]** corrente per la richiesta in questa fase è **In sospeso**. Per approvare la richiesta, seleziona i puntini di sospensione (`...`) accanto alla richiesta selezionata, quindi seleziona **[!UICONTROL Approva]** dal menu a discesa.

![Elenco delle richieste in arrivo con il menu a discesa con Approva evidenziato.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Nella finestra di dialogo **[!UICONTROL Rivedi richiesta organizzazione partner]** sono visualizzati i dettagli relativi alla richiesta di partnership organizzazione. Immetti un [!UICONTROL motivo] per l&#39;approvazione, quindi seleziona **[!UICONTROL Approva]**.

![Finestra di dialogo per la richiesta dell&#39;organizzazione partner di revisione con Motivo e approvazione evidenziati.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

Si è tornati alla pagina [!UICONTROL Richiesta in ingresso] e lo stato della richiesta è stato aggiornato a **[!UICONTROL Approvato]**.

![Elenco delle richieste in arrivo con Approvato evidenziato.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Utilizza questo flusso di lavoro/processo per condividere i pacchetti tra la tua organizzazione e l’organizzazione di origine.

### Condividere pacchetti con le organizzazioni partner {#share-package}

>[!NOTE]
>
>Solo i pacchetti con lo stato **Pubblicato** possono essere condivisi.

Per condividere un pacchetto con un&#39;organizzazione partner approvata, passare alla scheda [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]**. Selezionare quindi i puntini di sospensione (`...`) accanto al pacchetto, quindi selezionare **[!UICONTROL Condividi pacchetto]** dal menu a discesa.

![Elenco di pacchetti che mostra il menu a discesa con Share package evidenziato.](../images/ui/sandbox-tooling/private-share-package.png)

Nella finestra di dialogo **[!UICONTROL Condividi pacchetto]**, seleziona il pacchetto da condividere dal menu a discesa **[!UICONTROL Condividi impostazioni]**, quindi seleziona **[!UICONTROL Conferma]**.

>[!TIP]
>
>È possibile selezionare più di un’organizzazione. Le organizzazioni selezionate verranno visualizzate sotto il menu a discesa [!UICONTROL Impostazioni condivisione].

![Finestra di dialogo Condividi pacchetto con impostazioni di condivisione e Conferma evidenziata.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

## Pacchetti pubblici {#public-packages}

Utilizza la funzione Strumenti sandbox per creare pacchetti pubblici condivisibili che non richiedono alcuna approvazione aggiuntiva e che vengono facilmente importati con l’utilizzo del payload del pacchetto.

### Aggiorna la disponibilità del pacchetto al pubblico {#update-package}

Per aggiornare il tipo di disponibilità di un pacchetto, passare alla scheda [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]**. Selezionare quindi i puntini di sospensione (`...`) accanto al pacchetto, quindi selezionare **[!UICONTROL Aggiorna al pacchetto pubblico]** dal menu a discesa.

![L&#39;interfaccia utente Sandbox con la scheda Pacchetti e il menu dell&#39;opzione a discesa con Aggiornamento al pacchetto pubblico evidenziato.](../images/ui/sandbox-tooling/update-to-public.png)

Nella finestra di dialogo **[!UICONTROL Modifica la disponibilità del pacchetto in pubblica]**, verifica che il nome del pacchetto sia corretto e seleziona **[!UICONTROL Conferma]**.

>[!IMPORTANT]
>
> Una volta reso pubblico, un pacchetto non può essere riconvertito in privato.

![Modifica la disponibilità del pacchetto nella finestra di dialogo pubblica con Conferma evidenziata.](../images/ui/sandbox-tooling/change-package-availability.png)

### Condividere pacchetti utilizzando il payload del pacchetto

Per condividere il pacchetto pubblico, selezionare i puntini di sospensione (`...`) accanto al pacchetto, quindi selezionare **[!UICONTROL Copia payload pacchetto]**.

![L&#39;interfaccia utente Sandbox mostra un menu a discesa dei singoli pacchetti con il payload del pacchetto Copy evidenziato.](../images/ui/sandbox-tooling/copy-package-payload.png)

Nella finestra di dialogo **[!UICONTROL Copia payload del pacchetto]** vengono visualizzati il nome e il payload del pacchetto. Seleziona **[!UICONTROL Copia payload del pacchetto]** per copiare il payload associato al pacchetto.

![Finestra di dialogo Copia payload pacchetto che mostra il payload JSON con il payload del pacchetto Copy evidenziato.](../images/ui/sandbox-tooling/confirm-payload-copy.png)

### Creare un nuovo pacchetto utilizzando un payload del pacchetto

Per creare un pacchetto utilizzando un payload, passa alla scheda [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]**. Selezionare **[!UICONTROL Crea pacchetto]**.

![L&#39;interfaccia utente delle sandbox mostra l&#39;evidenziazione di Crea pacchetto.](../images/ui/sandbox-tooling/create-package.png)

Nella finestra di dialogo **[!UICONTROL Crea pacchetto]**, seleziona l&#39;opzione per **[!UICONTROL Incolla payload pacchetto]**, quindi seleziona **[!UICONTROL Seleziona]**.

![Finestra di dialogo Crea pacchetto con payload del pacchetto selezionato e Seleziona evidenziato.](../images/ui/sandbox-tooling/create-package-options.png)

Incolla il payload del pacchetto copiato nel campo di testo e seleziona **[!UICONTROL Crea]**.

![Finestra di dialogo Crea pacchetto con il campo di testo vuoto ed Evidenzia Crea.](../images/ui/sandbox-tooling/paste-payload.png)

Per visualizzare lo stato corrente della richiesta di condivisione, passa allo stato **[!UICONTROL Condivisione]**. Lo stato corrente della richiesta è visualizzato nella colonna **[!UICONTROL Stato condivisione]**.

![La scheda dello stato di condivisione mostra una richiesta di payload in sospeso.](../images/ui/sandbox-tooling/sharing-status.png)

## Passaggi successivi {#next-steps}

Questo documento illustra come utilizzare la funzione Strumenti Sandbox per condividere i pacchetti tra diverse organizzazioni. Per ulteriori informazioni, consulta la [guida agli strumenti sandbox](../ui/sandbox-tooling.md).

Per informazioni su come eseguire diverse operazioni utilizzando l&#39;API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md). Per una panoramica di alto livello delle sandbox in Experience Platform, consulta la [documentazione sulla panoramica](../home.md).
