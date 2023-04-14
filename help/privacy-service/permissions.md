---
title: Gestione delle autorizzazioni per Privacy Service
description: Scopri come gestire le autorizzazioni utente per Adobe Experience Platform Privacy Service utilizzando Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# Gestione delle autorizzazioni per Privacy Service

>[!IMPORTANT]
>
>Le autorizzazioni per Adobe Experience Platform Privacy Service sono state migliorate per aumentarne il livello di granularità. Queste modifiche consentono agli amministratori dell’organizzazione di concedere a più utenti l’accesso con il ruolo e il livello di autorizzazione desiderati. Gli utenti dell’account tecnico devono aggiornare le proprie autorizzazioni Privacy Service in quanto questo aggiornamento imminente rappresenta una modifica temporanea per loro. L&#39;applicazione di questa modifica delle autorizzazioni avrà luogo il **13 aprile 2023**. Consulta la documentazione su [migrazione delle credenziali API legacy](#migrate-tech-accounts) per informazioni sulla risoluzione del problema.
>
>Gli account tecnici sono disponibili per i clienti aziendali e creati tramite Adobe Developers Console. L’Adobe ID di un titolare di account tecnico termina in `@techacct.adobe.com`. Se non sei sicuro di essere un titolare di account tecnico, contatta l’amministratore dell’organizzazione.

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

>[!NOTE]
>
>Tutti i Privacy Service e [!UICONTROL Rinuncia alla vendita] Le autorizzazioni sono distinte e separate l&#39;una dall&#39;altra senza sovrapposizione funzionale. Ciò è possibile in quanto l’API di Privacy Service è considerata ideale.

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione lettura privacy] | Determina se l’utente può visualizzare le richieste di accesso ed eliminazione esistenti insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione per la scrittura della privacy] | Determina se un utente può creare nuove richieste di accesso ed eliminazione. |
| [!UICONTROL Autorizzazioni Privacy Service] | [!UICONTROL Autorizzazione per la distribuzione dei contenuti di lettura (Access)] | Quando una richiesta di accesso viene elaborata da Privacy Service, viene inviato a tale cliente un file ZIP contenente i dati del cliente. Quando si cercano i dettagli di una richiesta di accesso, questa autorizzazione determina se l&#39;utente può accedere al collegamento di download per il file ZIP della richiesta. |
| [!UICONTROL Autorizzazioni di rinuncia alla vendita] | [!UICONTROL Autorizzazione di lettura - Rinuncia alla vendita] | Determina se l’utente può visualizzare le richieste di rinuncia esistenti insieme ai relativi dettagli. |
| [!UICONTROL Autorizzazioni di rinuncia alla vendita] | [!UICONTROL Autorizzazione per scrittura - Rinuncia alla vendita] | Determina se un utente può creare nuove richieste di rinuncia. |

{style="table-layout:auto"}

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

In precedenza, gli account tecnici non richiedevano un profilo di prodotto per l’integrazione e le autorizzazioni. Tuttavia, a causa dei recenti miglioramenti delle autorizzazioni di Privacy Service, ora è necessario migrare le credenziali API legacy al profilo di prodotto. Questo aggiornamento consente di concedere autorizzazioni granulari ai titolari di account tecnici. Segui i passaggi descritti di seguito per aggiornare le autorizzazioni dell’account tecnico per Privacy Service.

#### Aggiornare le autorizzazioni dell’account tecnico {#update-tech-account-permissions}

Il primo passaggio nell’assegnazione di un set di autorizzazioni per l’account tecnico consiste nel passare alla [Adobe Admin Console](https://adminconsole.adobe.com/) e crea un nuovo profilo di prodotto per Privacy Service.

Dall’interfaccia utente di Admin Console, seleziona **Prodotti** dalla barra di navigazione, seguita da **[!UICONTROL Experience Cloud]** e **[!UICONTROL Adobe Experience Platform Privacy Service]** nella barra laterale sinistra. La [!UICONTROL Profili di prodotto] viene visualizzata la scheda . Seleziona **Nuovo profilo** per creare un nuovo profilo di prodotto per Privacy Service.

![La scheda Profili di prodotto di Experience Platform Privacy Service in Adobe Admin Console con Nuovo profilo evidenziato.](./images/permissions/create-product-profile.png)

La [!UICONTROL Creare un nuovo profilo di prodotto] viene visualizzata la finestra di dialogo . Le istruzioni complete su come creare un profilo di prodotto sono disponibili nella sezione [Guida all’interfaccia utente per la creazione di profili](../access-control/ui/create-profile.md).

Dopo aver salvato il nuovo profilo di prodotto, passa alla [Console Adobe Developer](https://developer.adobe.com/console/home) e accedi a quel prodotto o a quel progetto. Seleziona **[!UICONTROL Progetti]** dalla navigazione in alto, seguita dalla scheda del progetto.

>[!NOTE]
>
>Potrebbe essere necessario cancellare la cache e/o attendere un po&#39; di tempo per visualizzare il nuovo progetto nell’elenco dei progetti di Developer Console.

Dopo aver effettuato l’accesso al progetto, seleziona la **[!UICONTROL API Privacy Service]** integrazione dalla barra laterale sinistra.

![La scheda Progetti della console Adobe Developer con API Progetti e Privacy Service è evidenziata.](./images/permissions/login-to-dev-console-project.png)

Viene visualizzata la dashboard di integrazione dell’API di Privacy Service. Da questa dashboard puoi modificare il profilo di prodotto associato a quel progetto. Seleziona **[!UICONTROL Modificare i profili di prodotto]** per iniziare il processo. La [!UICONTROL Configurare l’API] viene visualizzata la finestra di dialogo .

![Dashboard dell’integrazione API di Privacy Service nella console Adobe Developer con Modifica profili prodotto evidenziati](./images/permissions/edit-product-profiles.png)

La [!UICONTROL Configurare l’API] mostra i profili di prodotto disponibili attualmente presenti nel servizio. Sono correlati ai profili di prodotto creati in Admin Console. Dall’elenco dei profili di prodotto disponibili, seleziona la casella di controllo per il nuovo profilo di prodotto creato per l’account tecnico in Admin Console. Questo associa automaticamente questo account tecnico alle autorizzazioni nel profilo di prodotto selezionato. Seleziona **[!UICONTROL Salva API configurata]** per confermare le impostazioni.

>[!NOTE]
>
>Se un account tecnico è già associato a un profilo di prodotto, verrà già selezionata una delle caselle di controllo dell’elenco dei profili di prodotto disponibili.

![È stata evidenziata la finestra di dialogo Configura API nella console Adobe Developer con un profilo di prodotto e l’opzione Salva API configurata.](./images/permissions/select-profile-for-tech-account.png)

#### Conferma l’applicazione delle impostazioni {#confirm-applied-settings}

Per confermare che le impostazioni sono state applicate all’account. Torna a [Admin Console](https://adminconsole.adobe.com/) e accedi al tuo nuovo profilo di prodotto creato. Seleziona la **[!UICONTROL Credenziali API]** per visualizzare un elenco dei progetti associati. Nell’elenco delle credenziali viene visualizzato il progetto utilizzato in Console per sviluppatori a cui è stato assegnato il profilo di prodotto all’account tecnico. Il nome di ciascuna credenziale API è composto dal nome del progetto con un numero generato in modo casuale e con suffisso alla fine. Selezionare una credenziale per aprire la [!UICONTROL Dettagli] pannello.

![Un profilo di prodotto nell’Admin Console con la scheda Credenziali API e una riga di credenziali del progetto evidenziate.](./images/permissions/confirm-credentials-in-admin-console.png)

La [!UICONTROL Dettagli] Il pannello contiene informazioni sulla credenziale API, tra cui l’ID tecnico associato, la chiave API, la data di creazione e l’ultima modifica e i prodotti Adobi associati.

![Il pannello Dettagli evidenziato di una credenziale API in Admin Console.](./images/permissions/admin-console-details-panel.png)

## Passaggi successivi

Questa guida descrive le autorizzazioni disponibili per Privacy Service e come gestirle tramite Admin Console.

Per i passaggi su come creare una nuova integrazione API dopo aver configurato i profili di prodotto, consulta la sezione [guida introduttiva per l’API di Privacy Service](./api/getting-started.md). Per ulteriori informazioni sulla gestione delle autorizzazioni per altre funzionalità di Adobe Experience Platform, consulta [documentazione sul controllo degli accessi](../access-control/home.md).
