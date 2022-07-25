---
title: Gestione delle autorizzazioni per la raccolta dati in Experience Platform
description: Panoramica di alto livello su come gestire le autorizzazioni e controllare l’accesso alle funzioni di raccolta dati in Adobe Experience Platform.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 7%

---

# Gestione delle autorizzazioni per la raccolta dati in Experience Platform

[Raccolta dati in Adobe Experience Platform](./home.md) è composto da diverse tecnologie che lavorano insieme per raccogliere e trasferire i tuoi dati. L’accesso a queste tecnologie è controllato tramite autorizzazioni granulari basate su ruoli in Adobe Admin Console.

Questa guida illustra come gestire le autorizzazioni per le funzioni di raccolta dati.

## Introduzione

Per configurare il controllo di accesso per la raccolta dei dati, è necessario disporre dei privilegi di amministratore per un’organizzazione con un’integrazione di prodotto con Adobe Experience Platform Data Collection. Il ruolo minimo che può concedere o revocare le autorizzazioni è un amministratore del profilo di prodotto. Altri ruoli di amministratore che possono gestire le autorizzazioni sono gli amministratori dei prodotti (possono gestire tutti i profili all’interno di un prodotto) e gli amministratori di sistema (senza restrizioni). Vedi l&#39;articolo su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) nella guida all’amministrazione di Adobe Enterprise per ulteriori informazioni.

Questa guida presuppone che tu abbia familiarità con i concetti di Admin Console di base come i profili di prodotto e le modalità con cui concedono le autorizzazioni di prodotto ai singoli utenti e gruppi. Per ulteriori informazioni, consulta la sezione [Guida utente di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

## Autorizzazioni disponibili

Le autorizzazioni pertinenti per la raccolta dei dati sono fornite attraverso due designazioni di prodotto nell&#39;Admin Console: **Adobe Experience Platform** e **Raccolta dati Adobe Experience Platform**. Le sezioni seguenti descrivono le autorizzazioni fornite in ciascun prodotto insieme alle descrizioni delle funzionalità specifiche a cui concedono l&#39;accesso.

### Autorizzazioni Adobe Experience Platform

Le autorizzazioni in Adobe Experience Platform includono l’accesso a datastreams, identità, schemi e sandbox. Per i passaggi su come configurare le autorizzazioni Adobe Experience Platform, consulta la [guida utente per il controllo degli accessi](../access-control/ui/overview.md).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| Sandbox | (N/D) | A seconda del [sandbox](../sandboxes/home.md) creati nell’organizzazione, puoi controllare l’accesso a ciascuno di essi tramite questa categoria di autorizzazioni nell’Admin Console. |
| Modellazione dati | Gestire gli schemi | Consente di visualizzare, creare e modificare [Schemi Experience Data Model (XDM)](../xdm/home.md). |
| Modellazione dati | Visualizzare gli schemi | Consente l’accesso in sola lettura agli schemi. |
| Gestione identità | Manage Identity Namespaces (Gestisci spazi dei nomi di identità) | Consente di visualizzare, creare e modificare [spazi dei nomi delle identità](../identity-service/namespaces.md). |
| Gestione identità | Visualizzare gli spazi dei nomi delle identità | Consente l’accesso in sola lettura ai namespace di identità. |
| Raccolta dati | Gestire i flussi di dati | Consente di visualizzare, creare e modificare [datastreams](../edge/datastreams/overview.md). |
| Raccolta dati | Visualizza i reami di dati | Consente l&#39;accesso in sola lettura ai datastreams. |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Autorizzazioni di raccolta dati Adobe Experience Platform

Le autorizzazioni in Raccolta dati di Adobe Experience Platform controllano l&#39;accesso a tag e funzionalità di inoltro eventi, tra cui proprietà, estensioni e ambienti. Per i passaggi su come configurare le autorizzazioni di raccolta dati di Adobe Experience Platform, consulta la [sezione sottostante](#manage).

| Categoria | Autorizzazione | Descrizione |
| --- | --- | --- |
| Piattaforme | Web | Consente l&#39;accesso a [proprietà web](../tags/ui/administration/companies-and-properties.md) se combinato con altri diritti di proprietà. |
| Piattaforme | Dispositivi mobili | Consente l&#39;accesso a [proprietà mobili](../tags/ui/administration/companies-and-properties.md) se combinato con altri diritti di proprietà. |
| Proprietà | (N/D) | A seconda delle proprietà create nell’organizzazione, puoi controllare l’accesso a ognuna di esse tramite questa categoria di autorizzazioni nell’Admin Console.<br><br>I diritti di proprietà assegnati a un utente si applicano solo alle proprietà a cui è stato concesso l&#39;accesso tramite questa categoria di autorizzazioni. |
| Diritti di proprietà | Approva | Consente di approvare una build della libreria come parte del [flusso di pubblicazione](../tags/ui/publishing/publishing-flow.md). |
| Diritti di proprietà | Sviluppa | Consente di sviluppare una build della libreria come parte del [flusso di pubblicazione](../tags/ui/publishing/publishing-flow.md). |
| Diritti di proprietà | Modifica, proprietà | Consente di modificare la configurazione di base per le proprietà a cui un utente ha accesso. |
| Diritti di proprietà | Gestire gli ambienti | Consente di gestire le [ambienti](../tags/ui/publishing/environments.md) per le proprietà a cui un utente ha accesso. |
| Diritti di proprietà | Gestire le estensioni | Consente di gestire le [estensioni](../tags/ui/managing-resources/extensions/overview.md) per le proprietà a cui un utente ha accesso. |
| Diritti di proprietà | Pubblica | Consente di pubblicare una build della libreria come parte del [flusso di pubblicazione](../tags/ui/publishing/publishing-flow.md). |
| Diritti aziendali | Sviluppa estensioni | Consente di creare e modificare pacchetti di estensione di proprietà della tua organizzazione, incluse versioni private e richieste di versioni pubbliche. |
| Diritti aziendali | Gestire le estensioni | Questa autorizzazione è applicabile solo se disponi di una licenza per Adobe Journey Optimizer o di un’altra soluzione che consente l’accesso ai messaggi in-app e push per dispositivi mobili. Questo ti consente di gestire le app che Adobe Experience Cloud conosce insieme alle credenziali push necessarie per comunicare con il servizio Firebase Cloud Messaging e il servizio Apple Push Notification. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Per ulteriori informazioni su come queste autorizzazioni influiscono sulle funzionalità dei tag, incluse le strategie di amministrazione per scenari comuni, consulta la documentazione sui tag in [autorizzazioni utente](../tags/ui/administration/user-permissions.md).

## Gestione delle autorizzazioni per la raccolta dati di Adobe Experience Platform {#manage}

>[!IMPORTANT]
>
>Questa sezione descrive solo come gestire le autorizzazioni per il prodotto Adobe Experience Platform Data Collection in Admin Console. Tuttavia, i passaggi per la gestione delle autorizzazioni nel prodotto Adobe Experience Platform sono simili.
>
>Consulta la sezione [guida all’interfaccia utente per il controllo degli accessi](../access-control/ui/overview.md) per istruzioni dettagliate sulla gestione delle autorizzazioni di Platform. A seconda degli SKU del prodotto a cui la tua organizzazione ha accesso, potresti non disporre di tutte le autorizzazioni disponibili.

Per gestire le autorizzazioni per la raccolta dati, accedi a [Admin Console](https://adminconsole.adobe.com/) e seleziona **[!UICONTROL Prodotti]** dalla navigazione superiore. Da qui, seleziona la scheda per **[!UICONTROL Raccolta dati Adobe Experience Platform]**.

![Immagine che mostra la scheda di prodotto Raccolta dati nell’Admin Console](./images/permissions/data-collection-card.png)

### Selezionare o creare un profilo di prodotto

La schermata successiva mostra un elenco dei profili di prodotto disponibili per la raccolta dati nell’organizzazione, il profilo predefinito è **[!DNL Default Data Collection All Access]**. Puoi scegliere di modificare il profilo di prodotto predefinito, se lo desideri, oppure puoi selezionare **[!UICONTROL Nuovo profilo]** per crearne una. Se nella tua organizzazione sono presenti più ruoli o gruppi di utenti che richiedono diversi livelli di accesso, devi creare un profilo di prodotto separato per ciascuno di essi.

![Immagine che mostra i profili di prodotto per la raccolta dati in Admin Console](./images/permissions/new-profile.png)

Dopo aver selezionato o creato un profilo di prodotto, puoi utilizzare la funzione **[!UICONTROL Modifica]** icone per iniziare [modifica delle autorizzazioni](#edit-permissions) per il profilo, oppure seleziona il **[!UICONTROL Utenti]** scheda per iniziare [assegnazione di utenti](#assign-users) al profilo.

![Immagine che mostra la scheda autorizzazioni per un Admin Console di profilo di prodotto](./images/permissions/edit-permission-categories.png)

### Modificare le autorizzazioni per il profilo di prodotto {#edit-permissions}

Quando modifichi le autorizzazioni per un profilo, le autorizzazioni disponibili sono elencate nella colonna a sinistra, mentre quelle incluse nel profilo sono elencate nella colonna a destra. Seleziona le autorizzazioni elencate per spostarle tra le due colonne.

![Immagine che mostra le autorizzazioni aggiunte nella colonna inclusa](./images/permissions/added-permissions.png)

Le autorizzazioni sono organizzate in categorie. Per passare da una categoria all’altra, seleziona la categoria desiderata dal menu di navigazione a sinistra.

![Immagine che mostra la sezione dei diritti aziendali in autorizzazioni](./images/permissions/switch-category.png)

Seleziona **[!UICONTROL Salva]** dopo aver configurato le autorizzazioni.

![Immagine che mostra la configurazione delle autorizzazioni da salvare per il profilo di prodotto](./images/permissions/save-permissions.png)

La visualizzazione del profilo di prodotto viene nuovamente visualizzata con le autorizzazioni aggiunte riportate.

![Immagine che mostra le autorizzazioni aggiunte per il profilo di prodotto](./images/permissions/permissions-added.png)

### Assegnare utenti al profilo prodotto {#assign-users}

Per assegnare gli utenti al profilo di prodotto (e concedere loro le autorizzazioni configurate del profilo), seleziona la **[!UICONTROL Utenti]** scheda , seguita da **[!UICONTROL Aggiungi utente]**.

![Immagine che mostra la scheda utenti per un profilo di prodotto in Admin Console](./images/permissions/manage-users.png)

Per ulteriori informazioni sulla gestione degli utenti per un profilo di prodotto, consulta [Documentazione di Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## Passaggi successivi

Questa guida descrive le autorizzazioni disponibili per l’interfaccia utente di raccolta dati e come gestirle tramite un Admin Console. Per ulteriori informazioni sulla gestione delle autorizzazioni per altre funzionalità di Adobe Experience Platform, consulta [documentazione sul controllo degli accessi](../access-control/home.md).
