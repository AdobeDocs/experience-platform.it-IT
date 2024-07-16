---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC
title: Creazione di un ruolo tramite il controllo degli accessi basato su attributi
description: Questo documento fornisce informazioni sulla gestione dei ruoli tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: d8f72bb5ae56daf5a41c763f821ca6306514bc48
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 7%

---

# Gestire i ruoli

I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario.

## Creare un nuovo ruolo

Per creare un nuovo ruolo, seleziona la scheda **[!UICONTROL Ruoli]** nella barra laterale e seleziona **[!UICONTROL Crea ruolo]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea un nuovo ruolo]**, in cui viene richiesto di immettere un nome e una descrizione facoltativa.

Al termine, selezionare **[!UICONTROL Conferma]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Quindi, seleziona le autorizzazioni per le risorse da includere nel ruolo utilizzando il menu a discesa.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Per aggiungere altre risorse, selezionare **[!UICONTROL Adobe Experience Platform]** dal pannello di navigazione a sinistra, che visualizza un elenco di risorse. In alternativa, immetti il nome della risorsa nella barra di ricerca nel pannello di navigazione a sinistra.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Fai clic e trascina la risorsa pertinente nel pannello principale.

![flac-additional-resources-ADDED](../../images/flac-ui/flac-additional-resources-added.png)

Seleziona le autorizzazioni per le risorse da includere nel ruolo utilizzando il menu a discesa. Ripeti questa operazione per tutte le risorse da includere per il ruolo. Al termine, selezionare **[!UICONTROL Salva ed esci]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Il nuovo ruolo è stato creato e si è reindirizzati alla pagina **[!UICONTROL Ruoli]**, in cui il nuovo ruolo creato verrà visualizzato nell&#39;elenco.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Per ulteriori informazioni su come gestire le autorizzazioni del ruolo dopo la creazione, vedere le sezioni relative alla gestione delle autorizzazioni per un ruolo [1.](#manage-permissions-for-a-role)

Il video seguente ha lo scopo di aiutare a comprendere come creare un nuovo ruolo e come gestire gli utenti per tale ruolo.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Duplicare un ruolo

Per duplicare un ruolo esistente, selezionarlo dalla scheda **[!UICONTROL Ruoli]**. In alternativa, utilizza l’opzione di filtro per filtrare i risultati e individuare il ruolo da duplicare.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Quindi, seleziona **[!UICONTROL Duplica]** dall&#39;alto a destra dello schermo.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Ruolo duplicato]**, in cui viene richiesto di confermare la duplicazione.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Verrà quindi visualizzata la pagina dei dettagli del ruolo, in cui è possibile modificare il nome e le autorizzazioni per il ruolo. Dettagli, Etichette e Sandbox sono duplicati dal ruolo precedente. Gli utenti dovranno essere aggiunti tramite la scheda utenti. Per ulteriori informazioni sull&#39;aggiunta di dettagli, etichette, sandbox e utenti a un ruolo, è possibile visualizzare il documento [Gestione delle autorizzazioni per un ruolo](permissions.md).

Fare clic sulla freccia sinistra per tornare alla scheda **[!UICONTROL Ruoli]**.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Il nuovo ruolo verrà visualizzato nell&#39;elenco nella pagina **[!UICONTROL Ruoli]**.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminare una mansione

Selezionare i puntini di sospensione (`…`) accanto al nome di un ruolo e un menu a discesa visualizza i controlli per modificare, eliminare o duplicare il ruolo. Seleziona Elimina dal menu a discesa.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Elimina ruolo utente]** in cui viene richiesto di confermare l&#39;eliminazione.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Verrai riportato alla scheda **[!UICONTROL Ruoli]**.

## Passaggi successivi

Dopo aver creato un nuovo ruolo, puoi passare al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
