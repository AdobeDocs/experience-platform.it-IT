---
title: Flusso di pubblicazione
description: Scopri come creare librerie, testare le build e approvarle per la produzione in Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 96%

---

# Flusso di pubblicazione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Il flusso di pubblicazione dei tag in Adobe Experience Platform si riferisce al processo di creazione delle librerie, test delle build e approvazione per la produzione.

Le azioni che puoi eseguire su una libreria dipendono dallo stato della libreria e dal livello di autorizzazione. Inoltre, lo stato di una libreria influenza anche le risorse che contiene (regole, elementi dati ed estensioni) a seconda di ciò che è a monte nel flusso di pubblicazione.

Le sezioni riportate di seguito descrivono i dettagli relativi ad autorizzazioni, stato della libreria e ciò che sta a monte in relazione al flusso di pubblicazione.

## Autorizzazioni {#permissions}

Esistono diversi livelli di autorizzazioni utente importanti per il flusso di pubblicazione; in particolare, le autorizzazioni di proprietà per [!UICONTROL sviluppare], [!UICONTROL approvare] e [!UICONTROL pubblicare]:

* **[!UICONTROL Sviluppare]**: include la possibilità di creare librerie, sviluppare le build e inviarle per l’approvazione.
* **[!UICONTROL Approvare]**: include la possibilità di creare build per staging e di approvare le build pronte.
* **[!UICONTROL Pubblicare]**: include la possibilità di pubblicare una libreria approvata.

Queste autorizzazioni non sono inclusive. Affinché un singolo utente possa eseguire il flusso di lavoro dall’inizio alla fine, è necessario concedere a tale persona tutte e tre le autorizzazioni all’interno di una determinata proprietà.

Per ulteriori informazioni sulla gestione delle autorizzazioni per i tag, consulta la [guida alle autorizzazioni utente](../administration/user-permissions.md).

## Stato della libreria {#state}

Per quanto riguarda il flusso di pubblicazione, sono disponibili quattro stati di base in cui una libreria può trovarsi:

* [[!UICONTROL Sviluppo]](#development)
* [[!UICONTROL Inviato]](#submitted)
* [[!UICONTROL Approvato]](#approved)
* [[!UICONTROL Pubblicato]](#published)

Questi quattro stati sono rappresentati come colonne all&#39;interno di **[!UICONTROL Flusso di pubblicazione]** scheda .

![](./images/approval-workflow/flow-ui.png)

Per spostare una libreria tra questi stati, è necessario eseguire azioni specifiche. Il diagramma seguente illustra ogni azione che fa avanzare una libreria da uno stato all’altro:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Sviluppo] {#development}

Quando vengono create nuove librerie, queste sono inizialmente nello stato [!UICONTROL Sviluppo]. Eventuali modifiche apportate a una libreria devono essere effettuate mentre la libreria si trova in [!UICONTROL Sviluppo]. Una volta completati lo sviluppo e il test, la libreria può essere inviata per l’approvazione.

La tabella seguente illustra le azioni disponibili per una libreria in stato di [!UICONTROL Sviluppo]:

| Azione | Descrizione |
| --- | --- |
| [!UICONTROL Modifica] | Utilizza la schermata [!UICONTROL Modifica libreria] per aggiungere o rimuovere componenti da una libreria. |
| [!UICONTROL Build to Development] | Crea una build per la libreria. La build viene compilata e implementata nell’ambiente a cui è assegnata la libreria. Questo passaggio non riesce se la libreria non è stata assegnata a un ambiente o se contiene una modifica già definita nel flusso a monte. |
| [!UICONTROL Invia per approvazione] | Annulla l’assegnazione della libreria all’ambiente di sviluppo e spostala nella colonna [!UICONTROL Inviata] per consentire l’intervento di un utente con autorizzazioni di approvazione. Questa opzione è abilitata solo se l’ultima build della libreria ha avuto esito positivo. |
| [!UICONTROL Submit &amp; Build to Staging] | Questa operazione può essere eseguita solo da un utente con autorizzazioni per sviluppo e approvazione. Questa azione annulla l’assegnazione della libreria dall’ambiente di sviluppo, sposta la libreria nello stato [!UICONTROL Inviato] e crea la libreria nell’ambiente di staging. Questa opzione è abilitata solo se l’ultima build della libreria ha avuto esito positivo. |
| [!UICONTROL Approva per la Pubblicazione] | Questa operazione può essere eseguita solo da un utente con autorizzazioni per sviluppo e approvazione. Questa azione annulla l’assegnazione della libreria dall’ambiente di sviluppo e la sposta nello stato [!UICONTROL Approvato], saltando completamente l’ambiente di staging e lo stato [!UICONTROL Inviato]. Questa opzione è abilitata solo se l’ultima build della libreria ha avuto esito positivo. |
| [!UICONTROL Approve &amp; Publish to Production] | Questa operazione può essere eseguita solo da un utente con autorizzazioni per sviluppo, approvazione e pubblicazione. Questa azione annulla l’assegnazione della libreria dall’ambiente di sviluppo, la sposta nello stato [!UICONTROL Approvato] e la pubblica in produzione. Al termine della build di produzione, la libreria passerà allo stato [!UICONTROL Pubblicato]. Questa opzione è abilitata solo se l’ultima build della libreria ha avuto esito positivo. |
| [!UICONTROL Elimina] | Rimuovi la libreria dal sistema. Questa azione non rimuove la build dall’ambiente. |

### [!UICONTROL Inviato] {#submitted}

Quando una libreria è nello stato [!UICONTROL Inviata], un utente con autorizzazioni di approvazione può testarla nell’ambiente di staging. Al termine del test, la libreria può essere approvata o rifiutata. Le build rifiutate tornano in [!UICONTROL Sviluppo], in modo da consentire ulteriori modifiche prima di riavviare il flusso di pubblicazione.

La tabella seguente illustra le azioni disponibili per una libreria nello stato [!UICONTROL Inviata]:

| Azione | Descrizione |
| --- | --- |
| [!UICONTROL Open] | Visualizza il contenuto della libreria. Non è possibile modificare le librerie che non rientrano nella colonna [!UICONTROL Sviluppo]. Se sono necessarie modifiche, la libreria deve essere rifiutata in modo da poter apportare modifiche nell’ambiente [!UICONTROL Sviluppo]. |
| [!UICONTROL Generazione per staging] | Crea la libreria nell’ambiente di staging per l’implementazione. |
| [!UICONTROL Approva per la Pubblicazione] | Sposta la libreria nella colonna [!UICONTROL Approvato] per consentire l’intervento di un utente con autorizzazioni di pubblicazione. |
| [!UICONTROL Approvare e pubblicare in produzione] | Questa operazione può essere eseguita solo da un utente con autorizzazioni per approvazione e pubblicazione. Questa azione annulla l’assegnazione della libreria dall’ambiente di staging, la sposta nello stato [!UICONTROL Approvato] e la pubblica in produzione. Al termine della build di produzione, la libreria passerà allo stato [!UICONTROL Pubblicato]. Questa operazione può essere eseguita con o senza una build corretta nell’ambiente di staging. |
| [!UICONTROL Rifiuta] | Per ulteriori modifiche, è necessario annullare l’assegnazione della libreria all’ambiente di staging e riportarla nella colonna [!UICONTROL Sviluppo]. |

### [!UICONTROL Approvato] {#approved}

Dopo l’approvazione di una libreria, un utente con autorizzazioni di pubblicazione può pubblicarla o rifiutarla. Le build rifiutate tornano in [!UICONTROL Sviluppo] in modo da poter apportare modifiche prima di riavviare il flusso di pubblicazione.

La tabella seguente illustra le azioni disponibili per una libreria nello stato [!UICONTROL Approvato].

| Azione | Descrizione |
| --- | --- |
| [!UICONTROL Apri] | Visualizza il contenuto della libreria. Non è possibile modificare le librerie che non rientrano nella colonna [!UICONTROL Sviluppo]. Se sono necessarie modifiche, la libreria deve essere rifiutata in modo da poter apportare modifiche in [!UICONTROL Sviluppo]. |
| [!UICONTROL Creare e pubblicare su Produzione] | Annulla l’assegnazione della libreria all’ambiente di staging, assegna la libreria all’ambiente di produzione e la implementa.<br><br>**Importante**: quando questa opzione è selezionata, la libreria diventa live nell’ambiente di produzione. Prima di selezionare questa opzione, verifica che la libreria contenga le modifiche desiderate. |
| [!UICONTROL Rifiuta] | Annulla l’assegnazione della libreria all’ambiente di staging e spostala nella colonna [!UICONTROL Sviluppo] per ulteriori modifiche. |

### [!UICONTROL Pubblicato] {#published}

La colonna [!UICONTROL Pubblicato] mostra quali librerie sono state pubblicate e le rispettive date di pubblicazione. La libreria attualmente pubblicata è contrassegnata da un punto verde. A meno che non sia stata eseguita una ripubblicazione su una libreria precedente, questa sarà sempre la libreria visualizzata all’inizio della colonna.

| Azione | Descrizione |
| --- | --- |
| [!UICONTROL Apri] | Visualizza il contenuto della libreria. Non è possibile modificare le librerie che non rientrano nella colonna [!UICONTROL Sviluppo]. Se desideri modificare gli elementi presenti nell’ambiente di produzione, devi creare una nuova libreria e spostarla lungo l’intero processo di pubblicazione. |
| [!UICONTROL Republish] | Questa azione è disponibile solo per le ultime cinque librerie pubblicate e solo se l’ambiente di produzione è (a) configurato con l’opzione Archivia disattivata e (b) utilizza un host [!UICONTROL Gestito da Adobe] al momento della compilazione. |
| [!UICONTROL Scarica] | Questa azione è disponibile solo per le ultime cinque librerie pubblicate e solo se l’ambiente di produzione è (a) configurato con l’opzione Archivia attivata e (b) utilizza un host [!UICONTROL Gestito da Adobe] al momento della compilazione. |

## A monte {#upstream}

Dopo aver pubblicato la prima libreria, diventa importante comprendere il ruolo di ciò che sta a monte durante lo spostamento di nuove librerie attraverso il flusso di pubblicazione.

Se una libreria si trova attualmente in fase di [!UICONTROL Sviluppo], [!UICONTROL Inviata], o [!UICONTROL Approvata], tale libreria erediterà le regole, gli elementi di dati e le estensioni delle librerie a monte. Queste risorse ereditate costituiscono una “linea di base” per ciascuna libreria durante l’avanzamento nel flusso di pubblicazione. In sostanza, ogni nuova libreria può essere considerata semplicemente una serie di modifiche alla linea di base stabilita dalla parte a monte. In questo modo, quando viene pubblicata una nuova iterazione, si evitano sovrascritture impreviste da una libreria precedente.

Ciò che è incluso a monte dipende dalla fase corrente della libreria. Ad esempio, le librerie nella colonna [!UICONTROL Approvato] ereditano solo le risorse dalla libreria [!UICONTROL Pubblicata], mentre le librerie in [!UICONTROL Sviluppo] ereditano le risorse da tutte le altre colonne.

![](./images/approval-workflow/upstream.png)

Quando modifichi una libreria nell’interfaccia utente, tutte le risorse ereditate da a monte sono rappresentate nel **[!UICONTROL Risorse a monte]** sezione . Per visualizzare queste risorse, seleziona l’opzione per espandere la scheda, sotto l’intestazione della sezione.

![](./images/approval-workflow/upstream-collapse.png)

La sezione si espande per mostrare le singole risorse ereditate dalle fasi a monte. Puoi utilizzare la barra a sinistra per filtrare tra [!UICONTROL Regole], [!UICONTROL Elementi dati] ed [!UICONTROL Estensioni], oppure la barra di ricerca per cercare una risorsa specifica per nome.

![](./images/approval-workflow/upstream-resources.png)

## Passaggi successivi

Questa guida fornisce una panoramica di alto livello del flusso di pubblicazione di librerie in Adobe Experience Platform. Per ulteriori informazioni su come pubblicare le librerie, consulta la [panoramica sulla pubblicazione](./overview.md).
