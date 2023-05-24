---
title: Gestione autorizzazioni per Privacy Service
description: Scopri come gestire le autorizzazioni utente per Adobe Experience Platform Privacy Service utilizzando Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# Gestire le autorizzazioni per Privacy Service

>[!IMPORTANT]
>
>Le autorizzazioni per Adobe Experience Platform Privacy Service sono state migliorate per aumentarne il livello di granularità. Queste modifiche consentono agli amministratori dell’organizzazione di concedere a più utenti l’accesso con il ruolo e il livello di autorizzazione desiderati. Gli utenti dell’account tecnico devono aggiornare le autorizzazioni Privacy Service in quanto questo aggiornamento imminente costituisce per loro una modifica fondamentale. L&#39;applicazione di questa modifica delle autorizzazioni avrà luogo il **13 aprile 2023**. Consulta la documentazione su [migrazione delle credenziali API legacy](#migrate-tech-accounts) per indicazioni sulla risoluzione del problema.
>
>Gli account tecnici sono disponibili per i clienti aziendali e vengono creati tramite la console per sviluppatori Adobe. L’Adobe ID di un titolare di account tecnico termina in `@techacct.adobe.com`. Se non sei sicuro di essere il titolare di un account tecnico, contatta l’amministratore dell’organizzazione.

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

>[!NOTE]
>
>Tutti i Privacy Service e [!UICONTROL Rinuncia alla vendita] Le autorizzazioni sono distinte e separate l&#39;una dall&#39;altra senza sovrapposizioni funzionali. Ciò è possibile in quanto l’API Privacy Service è considerata idempotente.

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

In precedenza, gli account tecnici non richiedevano un profilo di prodotto per l’integrazione e le autorizzazioni. Tuttavia, a causa dei recenti miglioramenti apportati alle autorizzazioni Privacy Service, ora è necessario migrare le credenziali API legacy al profilo di prodotto. Questo aggiornamento consente di concedere autorizzazioni granulari ai titolari di account tecnici. Per aggiornare le autorizzazioni dell’account tecnico per Privacy Service, segui la procedura indicata di seguito.

#### Aggiornare le autorizzazioni dell’account tecnico {#update-tech-account-permissions}

Il primo passaggio nell’assegnazione di un set di autorizzazioni per l’account tecnico consiste nel passare al [Adobe Admin Console](https://adminconsole.adobe.com/) e creare un nuovo profilo di prodotto per Privacy Service.

Dall’interfaccia utente di Admin Console, seleziona **Prodotti** dalla barra di navigazione, seguito da **[!UICONTROL Experience Cloud]** e **[!UICONTROL Adobe Experience Platform Privacy Service]** nella barra laterale a sinistra. Il [!UICONTROL Profili di prodotto] viene visualizzata la scheda. Seleziona **Nuovo profilo** per creare un nuovo profilo di prodotto per Privacy Service.

![La scheda Experience Platform di profili di prodotto di Privacy Service in Adobe Admin Console con il nuovo profilo evidenziato.](./images/permissions/create-product-profile.png)

Il [!UICONTROL Creare un nuovo profilo di prodotto] viene visualizzata. Le istruzioni complete su come creare un profilo di prodotto sono disponibili nella sezione [Guida all’interfaccia utente per creare profili](../access-control/ui/create-profile.md).

Dopo aver salvato il nuovo profilo di prodotto, vai alla [Console Adobe Developer](https://developer.adobe.com/console/home) e accedi al prodotto o al progetto. Seleziona **[!UICONTROL Progetti]** dalla navigazione in alto, seguita dalla scheda del progetto.

>[!NOTE]
>
>Potrebbe essere necessario cancellare la cache e/o attendere un po’ di tempo prima che il nuovo progetto venga visualizzato nell’elenco dei progetti di Console sviluppatori.

Dopo aver effettuato l’accesso al progetto, seleziona la **[!UICONTROL API PRIVACY SERVICE]** dalla barra laterale a sinistra.

![La scheda Progetti della console Adobe Developer con Progetti e API Privacy Service evidenziati.](./images/permissions/login-to-dev-console-project.png)

Viene visualizzato il dashboard di integrazione dell’API Privacy Service. Da questa dashboard puoi modificare il profilo di prodotto associato a quel progetto. Seleziona **[!UICONTROL Modificare i profili di prodotto]** per iniziare il processo. Il [!UICONTROL Configurare API] viene visualizzata.

![Dashboard di integrazione dell’API Privacy Service nella console Adobe Developer, con l’opzione Modifica profili di prodotto evidenziata](./images/permissions/edit-product-profiles.png)

Il [!UICONTROL Configurare API] mostra i profili di prodotto attualmente presenti nel servizio. Sono correlate ai profili di prodotto creati nell’Admin Console. Dall’elenco dei profili di prodotto disponibili, seleziona la casella di controllo per il nuovo profilo di prodotto creato per l’account tecnico nell’Admin Console. Questo associa automaticamente questo account tecnico alle autorizzazioni nel profilo di prodotto selezionato. Seleziona **[!UICONTROL Salva API configurata]** per confermare le impostazioni.

>[!NOTE]
>
>Se a un profilo di prodotto è già associato un account tecnico, verrà già selezionata una delle caselle di controllo dell’elenco dei profili di prodotto disponibili.

![Nella finestra di dialogo Configura API nella console Adobe Developer, sono evidenziate le caselle di controllo con un profilo di prodotto e Salva API configurata.](./images/permissions/select-profile-for-tech-account.png)

#### Conferma l&#39;applicazione delle impostazioni {#confirm-applied-settings}

Per verificare che le impostazioni siano state applicate all&#39;account. Torna a [Admin Console](https://adminconsole.adobe.com/) e passa al nuovo profilo di prodotto creato. Seleziona la **[!UICONTROL Credenziali API]** per visualizzare un elenco dei progetti associati. Il progetto utilizzato in Console sviluppatori in cui hai assegnato il profilo di prodotto all’account tecnico viene visualizzato nell’elenco delle credenziali. Il nome di ciascuna credenziale API è composto dal nome del progetto con un numero generato in modo casuale e con suffisso alla fine. Seleziona una credenziale per aprire [!UICONTROL Dettagli] pannello.

![Un profilo di prodotto nell’Admin Console con la scheda Credenziali API ed evidenziata una riga di credenziali del progetto.](./images/permissions/confirm-credentials-in-admin-console.png)

Il [!UICONTROL Dettagli] Il pannello contiene informazioni sulle credenziali API, tra cui l’ID tecnico associato, la chiave API, la data di creazione e dell’ultima modifica, nonché i prodotti Adobe associati.

![Il pannello Dettagli evidenziato di una credenziale API in Admin Console.](./images/permissions/admin-console-details-panel.png)

## Passaggi successivi

Questa guida descrive le autorizzazioni disponibili per Privacy Service e come gestirle con Admin Console.

Per informazioni su come creare una nuova integrazione API dopo la configurazione dei profili di prodotto, consulta [guida introduttiva all’API di Privacy Service](./api/getting-started.md). Per ulteriori informazioni sulla gestione delle autorizzazioni per altre funzionalità di Adobe Experience Platform, consulta [documentazione sul controllo degli accessi](../access-control/home.md).
