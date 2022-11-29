---
title: Gestione delle autorizzazioni per Privacy Service
description: Scopri come gestire le autorizzazioni utente per Adobe Experience Platform Privacy Service utilizzando Adobe Admin Console.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Gestione delle autorizzazioni per Privacy Service

Accesso a [Adobe Experience Platform Privacy Service](./home.md) è controllato tramite autorizzazioni granulari basate su ruoli in Adobe Admin Console. Creando profili di prodotto che assegnano autorizzazioni a gruppi di utenti, puoi determinare chi ha accesso a quali funzionalità in Privacy Service [Interfaccia](./ui/overview.md) e [API](./api/overview.md).

>[!NOTE]
>
>Quando crei un’integrazione per l’API Privacy Service, devi selezionare un profilo di prodotto esistente per determinare le funzioni o le azioni per le quali l’integrazione dispone delle autorizzazioni. Consulta la guida su [guida introduttiva all’API di Privacy Service](./api/getting-started.md) per ulteriori informazioni.

Questa guida illustra come gestire le autorizzazioni per Privacy Service.

## Introduzione

Per configurare il controllo di accesso per Privacy Service, è necessario disporre dei privilegi di amministratore per un’organizzazione con integrazione di prodotto con Adobe Experience Platform Privacy Service. Il ruolo minimo che può concedere o revocare le autorizzazioni è un **amministratore del profilo di prodotto**. Altri ruoli di amministratore che possono gestire le autorizzazioni sono **amministratori di prodotto** (può gestire tutti i profili all’interno di un prodotto) e **amministratori di sistema** (nessuna restrizione). Vedi l&#39;articolo su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) nella guida all’amministrazione di Adobe Enterprise per ulteriori informazioni.

Questa guida presuppone che tu abbia familiarità con i concetti di Admin Console di base come i profili di prodotto e le modalità con cui concedono le autorizzazioni di prodotto ai singoli utenti e gruppi. Per ulteriori informazioni, consulta la sezione [Guida utente di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

## Autorizzazioni disponibili

La tabella seguente delinea le autorizzazioni disponibili per Privacy Service con una descrizione delle funzionalità specifiche a cui concedono l’accesso:

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione lettura privacy] | Determina se l’utente può visualizzare le richieste di accesso ed eliminazione esistenti insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione per la scrittura della privacy] | Determina se un utente può creare nuove richieste di accesso ed eliminazione. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione per la distribuzione dei contenuti di lettura (Access)] | Quando una richiesta di accesso viene elaborata da Privacy Service, viene inviato a tale cliente un file ZIP contenente i dati del cliente. Quando si cercano i dettagli di una richiesta di accesso, questa autorizzazione determina se l&#39;utente può accedere al collegamento di download per il file ZIP della richiesta. |
| [!UICONTROL Autorizzazioni di rinuncia alla vendita] | [!UICONTROL Autorizzazione di lettura - Rinuncia alla vendita] | Determina se l’utente può visualizzare le richieste di rinuncia esistenti insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni di rinuncia alla vendita] | [!UICONTROL Autorizzazione per scrittura - Rinuncia alla vendita] | Determina se un utente può creare nuove richieste di rinuncia. |

{style=&quot;table-layout:auto&quot;}

## Gestire le autorizzazioni {#manage}

Per gestire le autorizzazioni di Privacy Service, accedi a [Admin Console](https://adminconsole.adobe.com/) e seleziona **[!UICONTROL Prodotti]** dalla navigazione superiore. Da qui, seleziona **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Immagine che mostra la scheda prodotto Privacy Service in Admin Console](./images/permissions/privacy-service-card.png)

### Selezionare o creare un profilo di prodotto

La schermata successiva mostra un elenco dei profili di prodotto disponibili per Privacy Service all’interno della tua organizzazione. Se non esistono profili di prodotto, seleziona **[!UICONTROL Nuovo profilo]** per crearne una. Se nella tua organizzazione sono presenti più ruoli o gruppi di utenti che richiedono diversi livelli di accesso, devi creare un profilo di prodotto separato per ciascuno di essi.

![Immagine che mostra i profili di prodotto di Privacy Service in Admin Console](./images/permissions/select-or-create-profile.png)

Dopo aver selezionato un profilo di prodotto, puoi utilizzare la funzione **[!UICONTROL Autorizzazioni]** scheda per iniziare [modifica delle autorizzazioni](#edit-permissions) per il profilo, oppure seleziona il **[!UICONTROL Utenti]** scheda per iniziare [assegnazione di utenti](#assign-users) al profilo.

![Immagine che mostra la scheda autorizzazioni per un Admin Console di profilo di prodotto](./images/permissions/users-permissions-tabs.png)

### Modifica le autorizzazioni per il profilo {#edit-permissions}

Sulla **[!UICONTROL Autorizzazioni]** seleziona una delle categorie di autorizzazioni visualizzate per accedere alla visualizzazione di modifica delle autorizzazioni.

Quando modifichi le autorizzazioni per un profilo, le autorizzazioni disponibili sono elencate nella colonna a sinistra, mentre quelle incluse nel profilo sono elencate nella colonna a destra. Seleziona le autorizzazioni elencate per spostarle tra le due colonne.

![Immagine che mostra le colonne di autorizzazione disponibili e incluse](./images/permissions/edit-permissions.png)

Le autorizzazioni sono organizzate in categorie. Per passare da una categoria all’altra, seleziona la categoria desiderata dal menu di navigazione a sinistra.

![Immagine che mostra [!UICONTROL Rinuncia alla vendita] sezione sotto le autorizzazioni](./images/permissions/switch-category.png)

Seleziona **[!UICONTROL Salva]** dopo aver configurato le autorizzazioni.

![Immagine che mostra la configurazione delle autorizzazioni da salvare per il profilo di prodotto](./images/permissions/save-permissions.png)

La visualizzazione del profilo di prodotto viene nuovamente visualizzata con le autorizzazioni aggiunte riportate.

![Immagine che mostra le autorizzazioni aggiunte per il profilo di prodotto](./images/permissions/permissions-added.png)

### Assegnare gli utenti al profilo {#assign-users}

Per assegnare gli utenti al profilo di prodotto (e concedere loro le autorizzazioni configurate del profilo), seleziona la **[!UICONTROL Utenti]** scheda , seguita da **[!UICONTROL Aggiungi utente]**.

![Immagine che mostra la scheda utenti per un profilo di prodotto in Admin Console](./images/permissions/manage-users.png)

Per ulteriori informazioni sulla gestione degli utenti per un profilo di prodotto, consulta [Documentazione di Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Migrazione delle credenziali API legacy al profilo {#migrate-tech-accounts}

>[!NOTE]
>
>Questa sezione si applica solo alle credenziali API esistenti create prima dell’integrazione delle autorizzazioni di Privacy Service in Adobe Admin Console. Per le nuove credenziali, i profili di prodotto (e le relative autorizzazioni) vengono assegnati tramite [Progetti della console Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/projects/) invece.<br><br>Vedi la sezione su [assegnazione di profili di prodotto a un progetto](./api/getting-started.md#product-profiles) nella guida introduttiva di Privacy Service API per ulteriori informazioni.

Per migrare le credenziali API legacy al profilo di prodotto, seleziona **[!UICONTROL Credenziali API]**, seguita da **[!UICONTROL Aggiungi credenziali API]**.

![[!UICONTROL Aggiungi credenziali API] selezionato nell&#39;Admin Console, sotto il [!UICONTROL Credenziali API] scheda per un profilo di prodotto](./images/permissions/api-credentials.png)

Scegli dall’elenco i progetti Console per sviluppatori desiderati, quindi seleziona **[!UICONTROL Salva]** per aggiungerli al profilo di prodotto. Tutte le chiamate API che utilizzano le credenziali di questi progetti erediteranno le autorizzazioni granulari concesse dal profilo di prodotto.

## Passaggi successivi

Questa guida descrive le autorizzazioni disponibili per Privacy Service e come gestirle tramite Admin Console.

Per i passaggi su come creare una nuova integrazione API dopo aver configurato i profili di prodotto, consulta la sezione [guida introduttiva per l’API di Privacy Service](./api/getting-started.md). Per ulteriori informazioni sulla gestione delle autorizzazioni per altre funzionalità di Adobe Experience Platform, consulta [documentazione sul controllo degli accessi](../access-control/home.md).
