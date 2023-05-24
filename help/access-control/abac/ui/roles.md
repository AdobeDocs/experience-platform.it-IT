---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC
title: Creazione di un ruolo tramite il controllo degli accessi basato su attributi
description: Questo documento fornisce informazioni sulla gestione dei ruoli tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# Gestire i ruoli

I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario.

## Creare un nuovo ruolo

Per creare un nuovo ruolo, selezionare **[!UICONTROL Ruoli]** nella barra laterale e seleziona **[!UICONTROL Crea Ruolo]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

Il **[!UICONTROL Crea un nuovo ruolo]** viene visualizzata una finestra di dialogo che richiede di immettere un nome e una descrizione facoltativa.

Al termine, seleziona **[!UICONTROL Conferma]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Quindi, seleziona le autorizzazioni per le risorse da includere nel ruolo utilizzando il menu a discesa.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Per aggiungere altre risorse, seleziona **[!UICONTROL Adobe Experience Platform]** dal pannello di navigazione a sinistra, che mostra un elenco di risorse. In alternativa, immetti il nome della risorsa nella barra di ricerca nel pannello di navigazione a sinistra.

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Fai clic e trascina la risorsa pertinente nel pannello principale.

![flac-additional-resources-ADDED](../../images/flac-ui/flac-additional-resources-added.png)

Seleziona le autorizzazioni per le risorse da includere nel ruolo utilizzando il menu a discesa. Ripeti questa operazione per tutte le risorse da includere per il ruolo. Al termine, seleziona **[!UICONTROL Salva ed esci]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Il nuovo ruolo è stato creato e l&#39;utente viene reindirizzato al **[!UICONTROL Ruoli]** pagina, in cui verrà visualizzato il ruolo appena creato.

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

Consulta le sezioni relative a [gestione delle autorizzazioni per un ruolo](#manage-permissions-for-a-role) per ulteriori dettagli su come gestire le autorizzazioni dei ruoli dopo la loro creazione.

## Duplicare un ruolo

Per duplicare un ruolo esistente, selezionarlo dall&#39;elenco **[!UICONTROL Ruoli]** scheda. In alternativa, utilizza l’opzione di filtro per filtrare i risultati e individuare il ruolo da duplicare.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Quindi, seleziona **[!UICONTROL Duplica]** in alto a destra.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

Il **[!UICONTROL Ruolo duplicato]** viene visualizzata una finestra di dialogo che richiede di confermare la duplicazione.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Verrà quindi visualizzata la pagina dei dettagli del ruolo, in cui è possibile modificare il nome e le autorizzazioni per il ruolo. Dettagli, Etichette e Sandbox sono duplicati dal ruolo precedente. Gli utenti dovranno essere aggiunti tramite la scheda utenti. È possibile visualizzare [gestire le autorizzazioni per un ruolo](permissions.md) Per ulteriori informazioni sull’aggiunta di Dettagli, Etichette, Sandbox e Utenti a un ruolo, consulta il documento.

Fai clic sulla freccia a sinistra per tornare al **[!UICONTROL Ruoli]** scheda.

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

Il nuovo ruolo verrà visualizzato nell&#39;elenco in **[!UICONTROL Ruoli]** pagina.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminare una mansione

Seleziona i puntini di sospensione (`…`) accanto al nome di un ruolo e un menu a discesa visualizza i controlli per modificare, eliminare o duplicare il ruolo. Seleziona Elimina dal menu a discesa.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

Il **[!UICONTROL Elimina ruolo utente]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare l’eliminazione.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Verrai reindirizzato al **[!UICONTROL Ruoli]** scheda.

## Passaggi successivi

Dopo aver creato un nuovo ruolo, puoi procedere al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
