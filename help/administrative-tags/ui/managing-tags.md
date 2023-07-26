---
keywords: Experience Platform;gestione di tag;tag;
title: Gestione dei tag unificati
description: Questo documento fornisce informazioni sulla gestione dei tag unificati in Adobe Experience Cloud
exl-id: 179b0618-3bd3-435c-9d17-63681177ca47
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '1070'
ht-degree: 100%

---

# Guida alla gestione dei tag

I tag consentono di gestire le tassonomie dei metadati al fine di classificare gli oggetti aziendali per facilitarne l’individuazione e la classificazione. I tag possono aiutare a identificare importanti attributi tassonomici per i tipi di pubblico con cui i team lavoreranno, in modo che possano trovarli più rapidamente e anche raggruppare i tipi di pubblico comuni in un descrittore. È necessario identificare le categorie di tag comuni, ad esempio aree geografiche, unità aziendali, linee di prodotti, progetti, team, intervalli di tempo (trimestri, mesi, anni) o qualsiasi altra cosa che possa aiutare ad applicare un significato e facilitare l’individuazione del pubblico per il team. 

## Creare un tag {#create-tag}

Per creare un nuovo tag, seleziona **[!UICONTROL tag]** nel menu di navigazione a sinistra, quindi seleziona la categoria di tag desiderata.

![Seleziona una categoria di tag](./images/tag-selection.png)

Seleziona **[!UICONTROL Crea tag]** per creare un nuovo tag.

![Creare un nuovo tag](./images/new-tag.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea tag]** che richiede di inserire un nome di tag univoco. Al termine, seleziona **[!UICONTROL Salva]**.

![Finestra di dialogo Crea tag con un nuovo nome tag](./images/create-tag-dialog.png)

Il nuovo tag viene creato correttamente e si viene reindirizzati alla schermata dei tag, in cui il nuovo tag creato viene visualizzato nell’elenco.

![Nuovo tag creato per la categoria di tag](./images/new-tag-listed.png)

## Modificare un tag {#edit-tag}

La modifica di un tag è utile in caso di errori ortografici, aggiornamenti delle convenzioni di denominazione o della terminologia. La modifica di un tag mantiene l’associazione del tag con qualsiasi oggetto in cui è attualmente applicato.

Per modificare un tag esistente, seleziona i puntini di sospensione nell’elenco delle categorie di tag (`...`) accanto al nome del tag che desideri modificare. I controlli per modificare, spostare o archiviare il tag sono visualizzati in un menu a discesa. Seleziona **[!UICONTROL Modifica]** dal menu a discesa.

![Azione di modifica visualizzata nel menu a discesa](./images/edit-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Modifica tag]** che richiede di modificare il nome del tag. Al termine, seleziona **[!UICONTROL Salva]**.

![Finestra di dialogo Modifica tag con un nome tag aggiornato](./images/edit-dialog.png)

Il nome del tag è stato aggiornato e si viene reindirizzati alla schermata dei tag, in cui il tag aggiornato viene visualizzato nell’elenco.

![Tag aggiornato per la categoria di tag](./images/updated-tag-listed.png)

## Spostare un tag tra le categorie {#move-tag}

I tag possono essere spostati in altre categorie di tag. Lo spostamento di un tag, l’associazione del tag viene mantenuta con tutti gli oggetti a cui è attualmente applicato.

Per spostare un tag esistente, seleziona i puntini di sospensione nell’elenco delle categorie di tag (`...`) accanto al nome del tag che desideri spostare. I controlli per modificare, spostare o archiviare il tag sono visualizzati in un menu a discesa. Seleziona **[!UICONTROL Modifica]** dal menu a discesa.

![Azione di spostamento visualizzata nel menu a discesa](./images/move-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Sposta tag]** che richiede di selezionare la categoria di tag in cui spostare il tag selezionato.

Per inserire il nome della categoria, è possibile scorrere e selezionare dall’elenco oppure utilizzare la funzione di ricerca. Al termine, seleziona **[!UICONTROL Sposta]**.

![Finestra di dialogo Sposta tag con criteri di ricerca per trovare la categoria di tag](./images/move-dialog.png)

Il tag viene spostato correttamente e si viene reindirizzati alla schermata dei tag, in cui viene visualizzato l’elenco dei tag aggiornato, dove il tag non viene più visualizzato.

![Elenco di tag aggiornato per la categoria di tag corrente](./images/current-tag-category.png)

Il tag verrà ora visualizzato nella categoria di tag selezionata in precedenza.

![Elenco di tag per la categoria di tag selezionata per spostare il tag](./images/moved-to-tag-category.png)

## Archiviare un tag {#archive-tag}

Lo stato di un tag può essere cambiato da attivo a archiviato. I tag archiviati non vengono rimossi dagli oggetti a cui sono già stati applicati, ma non possono più essere applicati ai nuovi oggetti. Lo stesso stato si riflette in tutti gli oggetti per ogni tag. Questa funzione è particolarmente utile quando si desidera mantenere le associazioni tag-oggetto correnti ma non si desidera che il tag venga utilizzato in futuro.

Per archiviare un tag esistente, seleziona i puntini di sospensione (`...`) dall’elenco delle categorie di tag accanto al nome del tag che desideri archiviare. I controlli per modificare, spostare o archiviare il tag sono visualizzati in un menu a discesa. Seleziona **[!UICONTROL Archivia]** dal menu a discesa.

![Azione archivia visualizzata nel menu a discesa](./images/archive-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Archivia tag]** che richiede di confermare l’archiviazione del tag. Seleziona **[!UICONTROL Archivia]**.

![Finestra di dialogo di archiviazione dei tag con richiesta di conferma](./images/archive-dialog.png)

Il tag è stato archiviato correttamente e si viene reindirizzati alla schermata dei tag. Ora l’elenco dei tag aggiornato mostra lo stato del tag come `Archived`.

![Elenco dei tag aggiornato per la categoria di tag corrente che mostra il tag come archiviato](./images/archive-status.png)

## Ripristinare un tag archiviato {#restore-archived-tag}

Se desideri applicare un tag `Archived` ai nuovi oggetti, il tag deve trovarsi in uno stato `Active`. Il ripristino di un tag archiviato restituirà un tag al relativo stato `Active`.

Per ripristinare un tag archiviato, seleziona i puntini di sospensione nell’elenco delle categorie di tag (`...`) accanto al nome del tag che desideri ripristinare. I controlli per ripristinare o eliminare il tag sono visualizzati in un menu a discesa. Seleziona **[!UICONTROL Ripristina]** dal menu a discesa.

![Azione di ripristino visualizzata nel menu a discesa](./images/restore-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Ripristina tag]** che richiede di confermare il ripristino del tag. Seleziona **[!UICONTROL Ripristina]**.

![Finestra di dialogo per il ripristino del tag con richiesta di conferma](./images/restore-dialog.png)

Il tag è stato ripristinato e si viene reindirizzati alla schermata dei tag. Ora l’elenco dei tag aggiornato mostra lo stato del tag come `Active`.

![Elenco dei tag aggiornato per la categoria di tag corrente che mostra il tag come attivo](./images/restored-active-status.png)

## Eliminare un tag {#delete-tag}

>[!NOTE]
>
>Solo i tag inclusi in uno stato `Archived` e che non sono associati ad alcun oggetto possono essere eliminati.

Se si elimina un tag, questo viene rimosso completamente dal sistema.

Per eliminare un tag archiviato, seleziona i puntini di sospensione nell’elenco delle categorie di tag (`...`) accanto al nome del tag che desideri eliminare. I controlli per ripristinare o eliminare il tag sono visualizzati in un menu a discesa. Seleziona **[!UICONTROL Elimina]** dalla menu a discesa.

![Azione di eliminazione visualizzata nel menu a discesa](./images/delete-action.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Elimina tag]** che richiede di confermare l’eliminazione del tag. Seleziona **[!UICONTROL Elimina]**.

![Finestra di dialogo Elimina tag con richiesta di conferma](./images/delete-dialog.png)

Il tag viene eliminato correttamente e si viene reindirizzati alla schermata dei tag. Il tag non viene più visualizzato nell’elenco ed è stato completamente rimosso.

![Elenco dei tag aggiornato per la categoria di tag corrente con il tag che non viene più visualizzato nell’elenco](./images/deleted-updated-list.png)

## Visualizzazione di oggetti con tag {#view-tagged}

Ogni tag dispone di una pagina di dettagli accessibile dalla libreria di tag. Questa pagina elenca tutti gli oggetti a cui è attualmente applicato il tag, consentendo agli utenti di visualizzare oggetti correlati di app e funzionalità diverse in un’unica vista.

Per visualizzare l’elenco degli oggetti con tag, individua il tag all’interno di una categoria di tag e selezionalo.

![Selezione di tag all’interno della categoria di tag](./images/view-tag-selection.png)

Viene visualizzata la pagina [!UICONTROL Oggetti con tag] che mostra una libreria di oggetti con tag.

![Libreria degli oggetti con tag](./images/tagged-objects.png)

## Passaggi successivi

Ora hai imparato a gestire i tag. Per una panoramica di alto livello dei tag in Experience Platform, consulta la[documentazione della panoramica sui tag](../overview.md).
