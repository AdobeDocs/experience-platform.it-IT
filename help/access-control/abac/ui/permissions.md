---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC
title: Autorizzazioni per la gestione dei ruoli di controllo dell'accesso basato su attributi
description: Questo documento fornisce informazioni sulla configurazione delle autorizzazioni per un ruolo tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# Gestire le autorizzazioni per un ruolo

>[!IMPORTANT]
>
>Per la concessione delle autorizzazioni, il controllo degli accessi utilizza l’ID utente (un ID univoco interno assegnato a un utente). Quando un’organizzazione viene migrata da Adobe ID a Business ID, tutte le autorizzazioni impostate per i relativi utenti andranno perse perché l’ID utente viene modificato e il controllo degli accessi utilizzerà l’ID utente appena generato. Se la tua organizzazione è stata migrata al Business ID, contatta il rappresentante del tuo Adobe per migrare il tuo ID utente da Adobe ID al Business ID.

Autorizzazioni è l’area di Experience Cloud in cui gli amministratori possono definire i ruoli utente e i criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto.

Tramite le Autorizzazioni, puoi creare e gestire i ruoli, nonché assegnare le autorizzazioni per le risorse desiderate per tali ruoli. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.

Immediatamente dopo la [creazione di un nuovo ruolo](#create-a-new-role), si ritorna alla scheda **[!UICONTROL Ruoli]**. Se stai modificando le autorizzazioni per un ruolo esistente, seleziona il ruolo dalla scheda **[!UICONTROL Ruoli]**. In alternativa, utilizza l’opzione di filtro per filtrare i risultati e trovare un ruolo.

## Filtra ruoli

Selezionare l&#39;icona funnel (![icona filtro](/help/images/icons/filter.png)) per visualizzare un elenco di controlli filtro che consentono di limitare i risultati.

![flac-filters](../../images/flac-ui/flac-filters.png)

Nell’interfaccia utente sono disponibili i seguenti filtri per i ruoli:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Creato tra] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. |
| [!UICONTROL Creato da] | Filtra per creatore di ruoli selezionando un utente dal menu a discesa. |
| [!UICONTROL Modificato tra] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. |
| [!UICONTROL Modificato da] | Filtra per modificatore di ruolo selezionando un utente dal menu a discesa. |

Per rimuovere un filtro, seleziona la &quot;X&quot; sull&#39;icona della pillola per il filtro in questione, oppure seleziona **[!UICONTROL Cancella tutto]** per rimuovere tutti i filtri.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## Dettagli ruolo

Seleziona il ruolo dalla scheda **[!UICONTROL Ruoli]**, che aprirà la pagina dei dettagli del ruolo.

![dettagli flac](../../images/flac-ui/flac-details.png)

La scheda dei dettagli fornisce una panoramica del ruolo. Nella panoramica vengono visualizzati il nome del ruolo, la descrizione del ruolo, il nome dell&#39;utente che ha creato e modificato il ruolo, la data di creazione e modifica del ruolo e le autorizzazioni associate al ruolo. Se necessario, è possibile modificare il nome e la descrizione del ruolo.

## Gestire le etichette per un ruolo

Seleziona la scheda **[!UICONTROL Etichette]** per aprire la pagina delle etichette dei ruoli, quindi seleziona **[!UICONTROL Aggiungi etichette]** per assegnare le etichette al ruolo.

![flac-labels](../../images/flac-ui/flac-labels.png)

Le etichette sono elencate in questa pagina. Nell&#39;elenco vengono visualizzati il nome dell&#39;etichetta, il nome descrittivo, la categoria e la relativa descrizione.

Seleziona le etichette dall&#39;elenco da aggiungere al ruolo, quindi seleziona **[!UICONTROL Salva]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

Le etichette aggiunte vengono visualizzate nella scheda **[!UICONTROL Etichette]**.

![flac-ADDED-labels](../../images/flac-ui/flac-added-labels.png)

Per rimuovere un&#39;etichetta da un ruolo, selezionare l&#39;icona **X** accanto al nome dell&#39;etichetta.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Gestione delle sandbox per il ruolo

Seleziona la scheda **[!UICONTROL Sandbox]** per aprire la pagina dei ruoli sandbox. Qui puoi vedere un elenco di sandbox che sono state aggiunte al ruolo.

![flac-sandboxes](../../images/flac-ui/flac-sandboxes.png)

Per aggiungere altre sandbox a un ruolo, seleziona **[!UICONTROL Modifica]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

Nella schermata successiva viene richiesto di scegliere le autorizzazioni per le risorse esistenti nelle sandbox da includere nel ruolo utilizzando il menu a discesa. Al termine, selezionare **[!UICONTROL Salva ed esci]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Gestione degli utenti per il ruolo

Seleziona la scheda **[!UICONTROL Utenti]** per aprire la pagina Ruoli utenti, quindi seleziona **[!UICONTROL Aggiungi utenti]** per assegnare gli utenti al ruolo.

![flac-users](../../images/flac-ui/flac-users.png)

Selezionare gli utenti dall&#39;elenco che si desidera aggiungere al ruolo. In alternativa, utilizzare la barra di ricerca per cercare l&#39;utente immettendo il nome o l&#39;indirizzo di posta elettronica, quindi selezionare **[!UICONTROL Salva]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

Gli utenti aggiunti vengono visualizzati nella scheda **[!UICONTROL Utenti]**.

![utenti aggiunti](../../images/flac-ui/flac-added-users.png)

Per rimuovere un utente da un ruolo, selezionare l&#39;icona **X** accanto al nome dell&#39;utente.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

Il video seguente ha lo scopo di aiutare a comprendere come creare un nuovo ruolo e come gestire gli utenti per tale ruolo.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Gestione delle credenziali API per il ruolo {#manage-api-credentials-for-role}

Seleziona la scheda **[!UICONTROL Credenziali API]** per aprire la pagina Ruoli: Credenziali API, quindi seleziona **[!UICONTROL Aggiungi credenziali API]** per assegnare le credenziali API al ruolo.

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Seleziona le credenziali API dall&#39;elenco che desideri aggiungere al ruolo, quindi seleziona **[!UICONTROL Salva]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Le credenziali API aggiunte vengono visualizzate nella scheda **[!UICONTROL Credenziali API]**.

![flac-add-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Per rimuovere le credenziali API da un ruolo, selezionare l&#39;icona **X** accanto al nome della credenziale API.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Rimuovi credenziali API]**, in cui viene richiesto di confermare l&#39;eliminazione.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Verrai reindirizzato alla scheda **[!UICONTROL Credenziali API]**.

## Gestione dei gruppi di utenti per i ruoli

I gruppi di utenti sono utenti multipli che sono stati raggruppati e hanno l’accesso per eseguire le stesse funzioni.

Selezionare la scheda **[!UICONTROL Gruppi di utenti]** per aprire la pagina dei gruppi di utenti dei ruoli, quindi selezionare **[!UICONTROL Aggiungi gruppi]** per assegnare gruppi di utenti al ruolo.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

Selezionare i gruppi di utenti dall&#39;elenco che si desidera aggiungere al ruolo. In alternativa, utilizzare la barra di ricerca per cercare il gruppo di utenti immettendo il nome del gruppo, quindi selezionare **[!UICONTROL Salva]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

Il gruppo utenti aggiunto viene visualizzato nella scheda **[!UICONTROL Gruppi utenti]**.

![gruppi di utenti aggiunti tramite flac](../../images/flac-ui/flac-added-user-groups.png)

Per rimuovere un gruppo utenti da un ruolo, selezionare l&#39;icona **X** accanto al nome del gruppo utenti.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Rimuovi gruppo utenti]**, in cui viene richiesto di confermare l&#39;eliminazione.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Verrai reindirizzato alla scheda **[!UICONTROL Gruppi utenti]**.

## Aggiunta di utenti all’Experience Platform tramite un ruolo

Per aggiungere un utente a un ruolo, accedere all&#39;Admin Console e selezionare **[!UICONTROL Aggiungi utenti]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi utenti al team]**. Immetti l’indirizzo e-mail degli utenti, il nome (facoltativo) e il cognome (facoltativo).

Seleziona l&#39;icona della matita per selezionare prodotti e gruppi di utenti, seleziona **[!UICONTROL Adobe Experience Platform]**, quindi seleziona **[!UICONTROL AEP-Default-All-Users]**, quindi seleziona **[!UICONTROL Salva]**.

![product-profile](../../images/flac-ui/product-profile.png)

## Passaggi successivi

Una volta stabilite le autorizzazioni, puoi passare al passaggio successivo per [gestire gli utenti](users.md).
