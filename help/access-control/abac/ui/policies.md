---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;ABAC
title: Controllo di accesso basato su attributi Crea un criterio
description: Questo documento fornisce informazioni sulla gestione dei criteri tramite l'interfaccia Autorizzazioni di Adobe Experience Cloud
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 97b4b98a2f14e36e8e8c71bd2ab9631782bc333f
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Gestire i criteri

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono sostituire altri criteri.

## Crea un nuovo criterio

Per creare un nuovo criterio, seleziona la **[!UICONTROL Criteri]** nella barra laterale e seleziona **[!UICONTROL Crea criterio]**.

![nuova politica](../../images/flac-ui/flac-new-policy.png)

La **[!UICONTROL Crea un nuovo criterio]** viene visualizzata una finestra di dialogo in cui viene richiesto di immettere un nome e una descrizione facoltativa. Al termine, seleziona **[!UICONTROL Conferma]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Utilizzando la freccia a discesa seleziona se desideri **Autorizzare l&#39;accesso a** (![permesso-vuoto-accesso-a](../../images/flac-ui/flac-permit-access-to.png)) una risorsa o **Nega l&#39;accesso a** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) una risorsa.

Quindi, seleziona la risorsa da includere nel criterio utilizzando il menu a discesa e il tipo di accesso alla ricerca, lettura o scrittura.

![flac-flac-policy-resource-menu a discesa](../../images/flac-ui/flac-policy-resource-dropdown.png)

Quindi, utilizzando la freccia a discesa, seleziona la condizione che desideri applicare a questo criterio, **Il seguente è vero** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) o **Il seguente è falso** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Seleziona l’icona più a **Aggiungi espressione corrisponde** o **Aggiungi gruppo di espressioni** per la risorsa .

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Utilizzando il menu a discesa , seleziona la **Risorsa**.

![elenco a discesa flac-policy-resource](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Quindi, seleziona il menu a discesa **Corrisponde**.

![flac-policy-match-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Quindi, seleziona il menu a discesa **Utente**.

![elenco a discesa flac-policy-user](../../images/flac-ui/flac-policy-user-dropdown.png)

Infine, seleziona la **Sandbox** a cui si desidera applicare le condizioni dei criteri, utilizzando il menu a discesa.

![flac-policy-sandboxes-menu a discesa](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Seleziona **Aggiungi risorsa** per aggiungere altre risorse. Al termine, seleziona **[!UICONTROL Salva e chiudi]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Il nuovo criterio viene creato correttamente e viene reindirizzato al **[!UICONTROL Criteri]** , in cui verrà visualizzato il criterio appena creato nell’elenco.

![salvato in base a criteri non validi](../../images/flac-ui/flac-policy-saved.png)

## Modificare un criterio

Per modificare un criterio esistente, selezionalo nella **[!UICONTROL Criteri]** scheda . In alternativa, utilizza l’opzione filtro per filtrare i risultati e trovare il criterio da modificare.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Quindi, seleziona i puntini di sospensione (`…`) accanto al nome dei criteri e un elenco a discesa visualizza i controlli per modificare, disattivare, eliminare o duplicare il ruolo. Seleziona modifica dal menu a discesa.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Viene visualizzata la schermata delle autorizzazioni dei criteri. Effettua gli aggiornamenti e seleziona **[!UICONTROL Salva e chiudi]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Il criterio viene aggiornato correttamente e viene reindirizzato al **[!UICONTROL Criteri]** scheda .

## Duplicare un criterio

Per duplicare un criterio esistente, selezionalo nella **[!UICONTROL Criteri]** scheda . In alternativa, utilizza l’opzione filtro per filtrare i risultati e trovare il criterio da modificare.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Quindi, seleziona i puntini di sospensione (`…`) accanto al nome di un criterio e un elenco a discesa visualizza i controlli per modificare, disattivare, eliminare o duplicare il ruolo. Seleziona duplica dal menu a discesa.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

La **[!UICONTROL Criterio duplicato]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la duplicazione.

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Il nuovo criterio viene visualizzato nell&#39;elenco come copia dell&#39;originale nel **[!UICONTROL Criteri]** scheda .

![salvataggi flash-role-duplicate](../../images/flac-ui/flac-role-duplicate-saved.png)

## Eliminare un criterio

Per eliminare un criterio esistente, selezionalo nella **[!UICONTROL Criteri]** scheda . In alternativa, utilizza l’opzione filtro per filtrare i risultati e trovare il criterio da eliminare.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Quindi, seleziona i puntini di sospensione (`…`) accanto al nome di un criterio e un elenco a discesa visualizza i controlli per modificare, disattivare, eliminare o duplicare il ruolo. Seleziona Elimina dal menu a discesa.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

La **[!UICONTROL Elimina criterio utente]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare l’eliminazione.

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

Viene restituito al **[!UICONTROL politiche]** appare una scheda e una conferma dell’eliminazione.

![flac-policy-delete-Confirm](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Attivare un criterio

Per attivare un criterio esistente, selezionarlo dalla **[!UICONTROL Criteri]** scheda . In alternativa, utilizza l’opzione filtro per filtrare i risultati e trovare il criterio da eliminare.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Quindi, seleziona i puntini di sospensione (`…`) accanto al nome di un criterio e un elenco a discesa visualizza i controlli per modificare, attivare, eliminare o duplicare il ruolo. Seleziona attiva dal menu a discesa.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

La **[!UICONTROL Attiva criterio utente]** viene visualizzata una finestra di dialogo in cui viene richiesto di confermare l’attivazione.

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

Viene restituito al **[!UICONTROL politiche]** appare una scheda e una conferma dell’attivazione. Lo stato del criterio viene visualizzato come attivo.

![attivato con flac-policy](../../images/flac-ui/flac-policy-activated.png)

## Passaggi successivi

Con la creazione di un nuovo criterio, puoi procedere al passaggio successivo per [gestire le autorizzazioni per un ruolo](permissions.md).
