---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC;;home;popular topic;access control;attribute-based access control;ABAC
title: Autorizzazioni per la gestione dei ruoli di controllo dell'accesso basato su attributi
description: Questo documento fornisce informazioni sulla configurazione delle autorizzazioni per un ruolo tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 12%

---

# Gestire le autorizzazioni per un ruolo {#manage-role-permissions}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Che cosa sono i ruoli?"
>abstract="I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. Classifica gli utenti che interagiscono con l’istanza Experience Platform e sono gli elementi costitutivi dei criteri di controllo degli accessi. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=it" text="Gestire i ruoli"

>[!IMPORTANT]
>
>Per la concessione delle autorizzazioni, il controllo degli accessi utilizza l’ID utente (un ID univoco interno assegnato a un utente). Quando un’organizzazione viene migrata da Adobe ID a Business ID, tutte le autorizzazioni impostate per i relativi utenti andranno perse perché l’ID utente viene modificato e il controllo degli accessi utilizzerà l’ID utente appena generato. Se l’organizzazione viene migrata al Business ID, contatta il rappresentante Adobe per migrare l’ID utente da Adobe ID al Business ID.

Autorizzazioni è l’area di Experience Cloud in cui gli amministratori possono definire i ruoli utente e i criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto.

Tramite le Autorizzazioni, puoi creare e gestire i ruoli, nonché assegnare le autorizzazioni per le risorse desiderate per tali ruoli. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico.

Immediatamente dopo la [creazione di un nuovo ruolo](#create-a-new-role), si ritorna alla scheda **[!UICONTROL Ruoli]**. Se stai modificando le autorizzazioni per un ruolo esistente, seleziona il ruolo dalla scheda **[!UICONTROL Ruoli]**. In alternativa, utilizza l’opzione di filtro per filtrare i risultati e trovare un ruolo.

## Filtra ruoli

Selezionare l&#39;icona funnel (![icona filtro](/help/images/icons/filter.png)) per visualizzare un elenco di controlli filtro che consentono di limitare i risultati.

![Dashboard dei ruoli nell&#39;interfaccia utente delle autorizzazioni con la sezione Ruoli filtro evidenziata.](../../images/flac-ui/flac-filters.png)

Nell’interfaccia utente sono disponibili i seguenti filtri per i ruoli:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Creato tra] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. |
| [!UICONTROL Creato da] | Filtra per creatore di ruoli selezionando un utente dal menu a discesa. |
| [!UICONTROL Modificato tra] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. |
| [!UICONTROL Modificato da] | Filtra per modificatore di ruolo selezionando un utente dal menu a discesa. |

Per rimuovere un filtro, seleziona la &quot;X&quot; sull&#39;icona della pillola per il filtro in questione, oppure seleziona **[!UICONTROL Cancella tutto]** per rimuovere tutti i filtri.

![Dashboard dei ruoli nell&#39;interfaccia utente delle autorizzazioni con le selezioni X e Cancella tutte evidenziate nei filtri selezionati.](../../images/flac-ui/flac-clear-filters.png)

## Dettagli del ruolo {#role-details}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Panoramica del ruolo"
>abstract="La finestra di dialogo della panoramica sui ruoli mostra i dettagli del ruolo, incluse le risorse e le sandbox a cui un determinato ruolo può accedere. Per gestire etichette, utenti, gruppi di utenti e credenziali API per il ruolo, passa alla scheda corrispondente dell’area di lavoro del ruolo."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-labels-for-a-role" text="Gestire le etichette per un ruolo"
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-users-for-a-role" text="Gestire gli utenti per un ruolo"

Seleziona il ruolo dalla scheda **[!UICONTROL Ruoli]**, che aprirà la dashboard [!UICONTROL Dettagli] del ruolo.

![L&#39;area di lavoro Dettagli per il ruolo selezionato viene visualizzata con le informazioni di panoramica evidenziate.](../../images/flac-ui/flac-details.png)

Il dashboard [!UICONTROL Details] fornisce una panoramica del ruolo. Nella panoramica vengono visualizzati il nome del ruolo, la descrizione, l’autore e l’ultimo modificatore, oltre alle date di creazione e modifica. Vengono inoltre visualizzate le autorizzazioni associate al ruolo e l’elenco delle sandbox assegnate. Se necessario, è possibile modificare il nome e la descrizione del ruolo.

## Gestire le etichette per un ruolo

Seleziona la scheda **[!UICONTROL Etichette]** per aprire l&#39;area di lavoro delle etichette dei ruoli, quindi seleziona **[!UICONTROL Aggiungi etichette]** per assegnare le etichette al ruolo.

![L&#39;area di lavoro Etichette del ruolo viene visualizzata con la scheda Etichette e il pulsante Aggiungi etichette evidenziati.](../../images/flac-ui/flac-labels.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Applica etichette di accesso e governance dei dati]**, che presenta un elenco di etichette. Nell&#39;elenco vengono visualizzati il nome dell&#39;etichetta, il nome descrittivo, la categoria e la relativa descrizione.

Seleziona le etichette dall&#39;elenco da aggiungere al ruolo, quindi seleziona **[!UICONTROL Salva]**

![Finestra di dialogo Applica etichette di accesso e governance dei dati con un&#39;etichetta selezionata.](../../images/flac-ui/flac-add-labels.png)

Le etichette aggiunte vengono visualizzate nella scheda **[!UICONTROL Etichette]**.

![Area di lavoro etichette del ruolo con l&#39;etichetta aggiunta evidenziata.](../../images/flac-ui/flac-added-labels.png)

Per rimuovere un&#39;etichetta da un ruolo, selezionare l&#39;etichetta, quindi selezionare **[!UICONTROL Rimuovi etichette]**.

![Area di lavoro Etichette del ruolo con un ruolo selezionato e l&#39;opzione Rimuovi etichette evidenziata.](../../images/flac-ui/flac-delete-labels.png)

## Gestire le sandbox per un ruolo

Seleziona la scheda **[!UICONTROL Dettagli]** e passa alla sezione **[!UICONTROL Sandbox]**. Seleziona **[!UICONTROL Visualizza tutto]** per visualizzare l&#39;elenco completo delle sandbox aggiunte al ruolo.

![Area di lavoro dettagli del ruolo con la sezione Sandbox evidenziata.](../../images/flac-ui/flac-sandboxes.png)

Per aggiungere altre sandbox a un ruolo, seleziona **[!UICONTROL Modifica]** in alto a destra nell&#39;interfaccia utente.

![Area di lavoro dettagli del ruolo con l&#39;opzione Modifica evidenziata.](../../images/flac-ui/flac-add-sandboxes.png)

Nella schermata successiva viene richiesto di scegliere le risorse sandbox da includere nel ruolo utilizzando il menu a discesa. Al termine, selezionare **[!UICONTROL Salva]** e quindi **[!UICONTROL Chiudi]**.

![Dashboard delle risorse del ruolo con il menu a discesa delle risorse sandbox evidenziato.](../../images/flac-ui/flac-add-role-permission.png)

## Gestire gli utenti per un ruolo

Seleziona la scheda **[!UICONTROL Utenti]** per aprire l&#39;area di lavoro [!UICONTROL Utenti], quindi seleziona **[!UICONTROL Aggiungi utenti]** per assegnare gli utenti al ruolo.

![L&#39;area di lavoro Utenti del ruolo viene visualizzata con la scheda Utenti e l&#39;opzione Aggiungi utenti evidenziata.](../../images/flac-ui/flac-users.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi utenti]**. Selezionare gli utenti dall&#39;elenco che si desidera aggiungere al ruolo. In alternativa, utilizzare la barra di ricerca per cercare l&#39;utente immettendo il nome o l&#39;indirizzo di posta elettronica, quindi selezionare **[!UICONTROL Salva]**

![La finestra di dialogo Aggiungi utenti con un utente selezionato e l&#39;opzione Barra di ricerca e salvataggio evidenziata.](../../images/flac-ui/flac-add-users.png)

Gli utenti aggiunti vengono visualizzati nella scheda **[!UICONTROL Utenti]**.

![Nell&#39;area di lavoro Utenti del ruolo sono visualizzati gli utenti aggiunti al ruolo.](../../images/flac-ui/flac-added-users.png)

Per rimuovere un utente da un ruolo, selezionare l&#39;icona **X** accanto al nome dell&#39;utente.

![Nell&#39;area di lavoro Utenti del ruolo è visualizzato un utente con l&#39;opzione X evidenziata.](../../images/flac-ui/flac-remove-users.png)

Il video seguente ha lo scopo di aiutare a comprendere come creare un nuovo ruolo e come gestire gli utenti per tale ruolo.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Gestire le credenziali API per un ruolo {#manage-api-credentials-for-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_apicredentials_about"
>title="Che cosa sono le credenziali API?"
>abstract="Le credenziali API vengono assegnate a ruoli per consentire a utenti e sviluppatori di accedere alle API di Experience Platform. Utilizzando le API di Experience Platform, puoi eseguire in modo programmatico operazioni CRUD (Create, Read, Update, Delete) di base sui dati, ad esempio la configurazione di attributi calcolati, l’accesso a dati/entità, l’esportazione di dati, l’eliminazione di dati o batch non necessari e altro ancora."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/landing/platform-apis/api-guide" text="Guida API di Experience Platform"

>[!IMPORTANT]
>
> Per utilizzare e gestire le credenziali API in [!UICONTROL Autorizzazioni], gli utenti devono disporre dei privilegi di amministratore di sistema.

Per utilizzare le API di Experience Platform come utente o sviluppatore, un amministratore di sistema deve aggiungere credenziali API oltre al set di autorizzazioni assegnato da un ruolo. Per una guida completa sulla creazione e l&#39;assegnazione delle credenziali API e sulle autorizzazioni necessarie, consulta l&#39;esercitazione dettagliata in [autenticare e accedere alle API di Experience Platform](../../../landing/api-authentication.md#generate-credentials).

Seleziona la scheda **[!UICONTROL Credenziali API]** per aprire l&#39;area di lavoro delle credenziali API dei ruoli, quindi seleziona **[!UICONTROL Aggiungi credenziali API]** per assegnare le credenziali API al ruolo.

![Area di lavoro credenziali API del ruolo con l&#39;opzione Aggiungi credenziali evidenziata.](../../images/flac-ui/flac-api-credentials.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi credenziali API]**. Seleziona le credenziali API dall&#39;elenco da aggiungere al ruolo, quindi seleziona **[!UICONTROL Salva]**

![Finestra di dialogo Aggiungi credenziali API con una credenziale selezionata ed opzione Salva evidenziata.](../../images/flac-ui/flac-add-api-credentials.png)

Le credenziali API aggiunte vengono visualizzate nella scheda **[!UICONTROL Credenziali API]**.

![Area di lavoro credenziali API del ruolo con le credenziali aggiunte visualizzate.](../../images/flac-ui/flac-added-api-credentials.png)

Per rimuovere una credenziale API da un ruolo, selezionare l&#39;icona **X** accanto al nome della credenziale API.

![L&#39;area di lavoro delle credenziali API del ruolo con l&#39;opzione X per rimuovere una credenziale evidenziata.](../../images/flac-ui/flac-remove-api-credentials.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Rimuovi credenziali API]**, in cui viene richiesto di confermare l&#39;eliminazione. Selezionare **[!UICONTROL Conferma]** per completare la rimozione delle credenziali selezionate.

![Viene evidenziata la richiesta di conferma per la rimozione delle credenziali.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

Verrai reindirizzato alla scheda **[!UICONTROL Credenziali API]**.

## Gestire gruppi di utenti per un ruolo {#manage-user-groups}

>[!CONTEXTUALHELP]
>id="platform_permissions_usergroups_about"
>title="Che cosa sono i gruppi di utenti?"
>abstract="I gruppi di utenti sono insiemi di più utenti che condividono l’accesso alle stesse funzioni. L’accesso alle risorse all’interno di un’organizzazione viene gestito tramite i ruoli assegnati ai gruppi di utenti."
>additional-url="https://experienceleague.adobe.com/it/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Gestire i ruoli"

I gruppi di utenti sono utenti multipli che sono stati raggruppati e hanno accesso per eseguire le stesse funzioni.

Selezionare la scheda **[!UICONTROL Gruppi utenti]** per aprire l&#39;area di lavoro dei gruppi utenti del ruolo, quindi selezionare **[!UICONTROL Aggiungi gruppi]** per assegnare gruppi di utenti al ruolo.

![Area di lavoro Gruppi utenti del ruolo con opzione Aggiungi gruppi](../../images/flac-ui/flac-user-groups.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi gruppi]**. Selezionare i gruppi di utenti dall&#39;elenco che si desidera aggiungere al ruolo. In alternativa, utilizzare la barra di ricerca per cercare il gruppo di utenti immettendo il nome del gruppo, quindi selezionare **[!UICONTROL Salva]**

![Finestra di dialogo Aggiungi gruppi con un gruppo di utenti selezionato e opzione di ricerca e salvataggio evidenziata.](../../images/flac-ui/flac-add-user-groups.png)

Il gruppo utenti aggiunto viene visualizzato nella scheda **[!UICONTROL Gruppi utenti]**.

![Nell&#39;area di lavoro Gruppi utenti del ruolo è visualizzato l&#39;elenco dei gruppi di utenti aggiunti.](../../images/flac-ui/flac-added-user-groups.png)

Per rimuovere un gruppo utenti da un ruolo, selezionare l&#39;icona **X** accanto al nome del gruppo utenti.

![Area di lavoro Gruppi utenti del ruolo con l&#39;opzione X evidenziata per rimuovere un gruppo di utenti specifico.](../../images/flac-ui/flac-remove-user-groups.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Rimuovi gruppo utenti]**, in cui viene richiesto di confermare l&#39;eliminazione. Selezionare **[!UICONTROL Conferma]** per rimuovere il gruppo di utenti selezionato.

![Viene visualizzato ed evidenziato il popover per la rimozione di un gruppo di utenti.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

Verrai reindirizzato alla scheda **[!UICONTROL Gruppi utenti]**.

## Aggiungere utenti ad Experience Platform

In qualità di amministratore di sistema, puoi concedere agli sviluppatori l&#39;accesso a un utente in modo che possano [creare integrazioni](../../../landing/api-authentication.md#generate-credentials) in Adobe Developer Console.

Per aggiungere un Experience Platform utente, accedi a [Admin Console](https://adminconsole.adobe.com) e seleziona **[!UICONTROL Aggiungi utenti]**.

![Dashboard di Adobe Admin Console con l&#39;opzione Aggiungi utenti evidenziata.](../../images/flac-ui/product-profile-add-users.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi utenti al team]**. Immettere l&#39;indirizzo di posta elettronica, il nome (facoltativo) e il cognome (facoltativo) dell&#39;utente. Quindi seleziona **[!UICONTROL Prodotti]**.

![Finestra di dialogo Aggiungi utenti al team con l&#39;opzione Campi utente e prodotti evidenziata.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Seleziona prodotti]**. Seleziona **[!UICONTROL Adobe Experience Platform]**.

![La finestra di dialogo per la selezione dei prodotti con Adobe Experience Platform è evidenziata.](../../images/flac-ui/product-profile-select-product.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Seleziona profili di prodotto]**. Seleziona **[!UICONTROL AEP-Default-All-Users]**, quindi seleziona **[!UICONTROL Salva]**.

![La finestra di dialogo Seleziona profili di prodotto con AEP-Default-All-Users selezionata e Applica evidenziata.](../../images/flac-ui/product-profile-select-product-profiles.png)

Rivedi le informazioni, quindi seleziona **[!UICONTROL Salva]** per aggiungere l&#39;utente.

![Finestra di dialogo Aggiungi utenti al team con le informazioni utente e le selezioni selezionate e l&#39;opzione Salva evidenziata.,](../../images/flac-ui/product-profile-save-user.png)

## Passaggi successivi

Una volta stabilite le autorizzazioni, puoi passare al passaggio successivo per [gestire gli utenti](users.md).
