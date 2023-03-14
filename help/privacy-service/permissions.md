---
title: Gestione autorizzazioni per Privacy Service
description: Scopri come gestire le autorizzazioni utente per Adobe Experience Platform Privacy Service utilizzando Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: ebcfdc9f73fc9120cf3819169d72bd828d0b35a6
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# Gestire le autorizzazioni per Privacy Service

Accesso a [Adobe Experience Platform Privacy Service](./home.md) è controllato tramite autorizzazioni granulari basate sui ruoli in Adobe Admin Console. Creando profili di prodotto che assegnano autorizzazioni a gruppi di utenti, puoi determinare chi ha accesso a quali funzioni in Privacy Service [UI](./ui/overview.md) e [API](./api/overview.md).

>[!NOTE]
>
>Quando crei un’integrazione per l’API Privacy Service, devi selezionare un profilo di prodotto esistente per determinare per quali funzioni o azioni l’integrazione dispone delle autorizzazioni. Consulta la guida su [guida introduttiva all’API di Privacy Service](./api/getting-started.md) per ulteriori informazioni.

Questa guida illustra come gestire le autorizzazioni per Privacy Service.

## Introduzione

Per configurare il controllo degli accessi per Privacy Service, è necessario disporre dei privilegi di amministratore per un’organizzazione che dispone di un’integrazione di prodotto con Adobe Experience Platform Privacy Service. Il ruolo minimo che può concedere o revocare le autorizzazioni è un **amministratore profilo prodotto**. Altri ruoli di amministratore che possono gestire le autorizzazioni sono **amministratori di prodotto** (può gestire tutti i profili all’interno di un prodotto) e **amministratori di sistema** (nessuna restrizione). Vedi l’articolo su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) per ulteriori informazioni, consulta l’Adobe guida all’amministrazione di Enterprise.

Questa guida presuppone che tu abbia familiarità con i concetti di base degli Admin Console, come i profili di prodotto e il modo in cui concedono le autorizzazioni di prodotto a singoli utenti e gruppi. Per ulteriori informazioni, vedere [Guida utente di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

## Autorizzazioni disponibili

La tabella seguente illustra le autorizzazioni disponibili per Privacy Service con una descrizione delle funzionalità specifiche a cui concedono l’accesso:

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione di lettura della privacy] | Determina se l’utente può visualizzare le richieste di accesso ed eliminazione esistenti, insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione di scrittura per la privacy] | Determina se un utente può creare nuove richieste di accesso ed eliminazione. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione di lettura (accesso) per la distribuzione dei contenuti] | Quando una richiesta di accesso viene elaborata da Privacy Service, a tale cliente viene inviato un file ZIP contenente i dati del cliente. Quando si cercano i dettagli di una richiesta di accesso, questa autorizzazione determina se l’utente può accedere al collegamento di download per il file ZIP della richiesta. |
| [!UICONTROL Autorizzazioni di rifiuto vendita] | [!UICONTROL Autorizzazione di lettura - Rifiuto della vendita] | Determina se l’utente può visualizzare le richieste di rifiuto del consenso esistenti, insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni di rifiuto vendita] | [!UICONTROL Autorizzazione di scrittura - Rifiuto della vendita] | Determina se un utente può creare nuove richieste di rifiuto della vendita. |

{style="table-layout:auto"}

## Gestire le autorizzazioni {#manage}

Per gestire le autorizzazioni di Privacy Service, accedi a [Admin Console](https://adminconsole.adobe.com/) e seleziona **[!UICONTROL Prodotti]** dalla navigazione in alto. Da qui, seleziona **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Immagine che mostra la scheda prodotto Privacy Service in Admin Console](./images/permissions/privacy-service-card.png)

### Seleziona o crea un profilo di prodotto

La schermata successiva mostra un elenco dei profili di prodotto disponibili per Privacy Service nell’organizzazione. Se non esiste alcun profilo di prodotto, seleziona **[!UICONTROL Nuovo profilo]** per crearne uno. Se nell’organizzazione sono presenti più ruoli o gruppi di utenti che richiedono livelli di accesso diversi, è necessario creare un profilo di prodotto separato per ciascuno di essi.

![Immagine che mostra i profili di prodotto di Privacy Service in Admin Console](./images/permissions/select-or-create-profile.png)

Dopo aver selezionato un profilo di prodotto, puoi utilizzare **[!UICONTROL Autorizzazioni]** scheda per iniziare [autorizzazioni di modifica](#edit-permissions) per il profilo, oppure seleziona il **[!UICONTROL Utenti]** scheda per iniziare [assegnazione di utenti](#assign-users) al profilo.

![Immagine che mostra la scheda delle autorizzazioni per un Admin Console di profilo di prodotto](./images/permissions/users-permissions-tabs.png)

### Modificare le autorizzazioni per il profilo {#edit-permissions}

Il giorno **[!UICONTROL Autorizzazioni]** , selezionare una delle categorie di autorizzazione visualizzate per accedere alla visualizzazione di modifica delle autorizzazioni.

Quando si modificano le autorizzazioni per un profilo, le autorizzazioni disponibili sono elencate nella colonna a sinistra, mentre quelle incluse nel profilo sono elencate nella colonna a destra. Seleziona le autorizzazioni elencate per spostarle tra una colonna e l’altra.

![Immagine che mostra le colonne di autorizzazione disponibili e incluse](./images/permissions/edit-permissions.png)

Le autorizzazioni sono organizzate in categorie. Per passare da una categoria all’altra, seleziona la categoria desiderata dal menu di navigazione a sinistra.

![Immagine che mostra [!UICONTROL Rinuncia alla vendita] sezione in autorizzazioni](./images/permissions/switch-category.png)

Seleziona **[!UICONTROL Salva]** al termine della configurazione delle autorizzazioni.

![Immagine che mostra la configurazione delle autorizzazioni salvata per il profilo di prodotto](./images/permissions/save-permissions.png)

La vista del profilo di prodotto viene nuovamente visualizzata con le autorizzazioni aggiunte riportate.

![Immagine che mostra le autorizzazioni aggiunte per il profilo di prodotto](./images/permissions/permissions-added.png)

### Assegnare utenti al profilo {#assign-users}

Per assegnare gli utenti al profilo di prodotto (e concedere le autorizzazioni configurate per il profilo), seleziona la **[!UICONTROL Utenti]** , seguito da **[!UICONTROL Aggiungi utente]**.

![Immagine che mostra la scheda Utenti per un profilo di prodotto in Admin Console](./images/permissions/manage-users.png)

Per ulteriori informazioni sulla gestione degli utenti per un profilo di prodotto, consulta [Documentazione di Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Migrare le credenziali API legacy al profilo {#migrate-tech-accounts}

>[!NOTE]
>
>Questa sezione si applica solo alle credenziali API esistenti create prima che le autorizzazioni Privacy Service fossero integrate in Adobe Admin Console. Per le nuove credenziali, i profili di prodotto (e le relative autorizzazioni) vengono assegnati tramite [Progetti della console Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) invece.<br><br>Consulta la sezione su [assegnazione di profili di prodotto a un progetto](./api/getting-started.md#product-profiles) per ulteriori informazioni, consulta la guida introduttiva all’API di Privacy Service.

Per migrare le credenziali API legacy al profilo di prodotto, seleziona **[!UICONTROL Credenziali API]**, seguito da **[!UICONTROL Aggiungi credenziali API]**.

![[!UICONTROL Aggiungi credenziali API] in fase di selezione in Admin Console, sotto [!UICONTROL Credenziali API] scheda per un profilo di prodotto](./images/permissions/api-credentials.png)

Scegli i progetti Developer Console desiderati dall’elenco, quindi seleziona **[!UICONTROL Salva]** per aggiungerli al profilo di prodotto. Tutte le chiamate API che utilizzano le credenziali di questi progetti ereditano le autorizzazioni granulari concesse dal profilo di prodotto.

## Passaggi successivi

Questa guida descrive le autorizzazioni disponibili per Privacy Service e come gestirle con Admin Console.

Per informazioni su come creare una nuova integrazione API dopo la configurazione dei profili di prodotto, consulta [guida introduttiva all’API di Privacy Service](./api/getting-started.md). Per ulteriori informazioni sulla gestione delle autorizzazioni per altre funzionalità di Adobe Experience Platform, consulta [documentazione sul controllo degli accessi](../access-control/home.md).
