---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;ABAC
title: Controllo dell'accesso basato su attributi Crea un ruolo
description: Questo documento fornisce informazioni sulla gestione dei ruoli tramite l'interfaccia Autorizzazioni di Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: c31855bff9d87133252c43e2f2f2fe1960c7b144
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Gestire i ruoli

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

I ruoli definiscono l’accesso che un amministratore, uno specialista o un utente finale ha alle risorse dell’organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente viene raggruppato attraverso responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario.

## Creare un nuovo ruolo

Per creare un nuovo ruolo, seleziona la **[!UICONTROL Ruoli]** nella barra laterale e seleziona **[!UICONTROL Crea ruolo]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

La **[!UICONTROL Creare un nuovo ruolo]** viene visualizzata una finestra di dialogo in cui viene richiesto di immettere un nome e una descrizione facoltativa.

Al termine, seleziona **[!UICONTROL Conferma]**.

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Quindi, seleziona le autorizzazioni della risorsa che desideri includere nel ruolo utilizzando il menu a discesa .

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Per aggiungere altre risorse, seleziona **[!UICONTROL Adobe Experience Platform]** nel pannello di navigazione a sinistra viene visualizzato un elenco di risorse. In alternativa, immetti il nome della risorsa nella barra di ricerca nel pannello di navigazione a sinistra.

![flac-add-resources](../../images/flac-ui/flac-add-additional-resources.png)

Fai clic e trascina la risorsa pertinente e rilasciala nel pannello principale.

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

Seleziona le autorizzazioni della risorsa da includere nel ruolo utilizzando il menu a discesa . Ripeti questa operazione per tutte le risorse da includere per il ruolo. Al termine, seleziona **[!UICONTROL Salva e chiudi]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

Il nuovo ruolo viene creato correttamente e viene reindirizzato al **[!UICONTROL Ruoli]** , in cui verrà visualizzato il ruolo appena creato nell’elenco.

![salvato con un ruolo](../../images/flac-ui/flac-role-saved.png)

Consulta le sezioni [gestione delle autorizzazioni per un ruolo](#manage-permissions-for-a-role) per ulteriori dettagli su come gestire le autorizzazioni per i ruoli una volta create.

## Duplicare un ruolo

Per duplicare un ruolo esistente, seleziona il ruolo dal **[!UICONTROL Ruoli]** scheda . In alternativa, utilizza l’opzione filtro per filtrare i risultati e trovare il ruolo da duplicare.

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

Quindi, seleziona **[!UICONTROL Duplica]** dall&#39;alto a destra dello schermo.

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

La **[!UICONTROL Ruolo duplicato]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la duplicazione.

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Successivamente, passerai alla pagina dei dettagli del ruolo in cui puoi modificare il nome e le autorizzazioni per il ruolo. I dettagli, le etichette e le sandbox sono duplicati rispetto al ruolo precedente. Gli utenti dovranno essere aggiunti tramite la scheda utenti . È possibile visualizzare [gestire le autorizzazioni per un ruolo](permissions.md) per ulteriori informazioni sull’aggiunta di dettagli, etichette, sandbox e utenti a un ruolo.

Fai clic sulla freccia sinistra per tornare alla **[!UICONTROL Ruoli]** scheda .

![flac-return-to-role](../../images/flac-ui/flac-return-to-roles.png)

Il nuovo ruolo verrà visualizzato nell’elenco **[!UICONTROL Ruoli]** pagina.

![salvataggi flash-role-duplicate](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminare un ruolo

Seleziona i puntini di sospensione (`…`) accanto al nome di un ruolo e un elenco a discesa visualizza i controlli per modificare, eliminare o duplicare il ruolo. Seleziona Elimina dal menu a discesa.

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

La **[!UICONTROL Eliminare il ruolo utente]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare l’eliminazione.

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

Verrà restituito al **[!UICONTROL Ruoli]** scheda .

## Passaggi successivi

Con un nuovo ruolo creato, puoi passare al passaggio successivo a [gestire le autorizzazioni per un ruolo](permissions.md).
