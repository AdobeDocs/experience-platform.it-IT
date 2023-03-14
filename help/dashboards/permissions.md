---
solution: Experience Platform
title: Ottenere e concedere autorizzazioni di accesso per dashboard di Experience Platform
type: Documentation
description: Consente agli utenti di visualizzare, modificare e aggiornare dashboard di Experience Platform tramite Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 7%

---

# Autorizzazioni di accesso per le dashboard

Per consentire agli utenti di visualizzare, modificare e aggiornare le dashboard, devi prima abilitare le autorizzazioni. In Adobe Experience Platform, il controllo degli accessi viene fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com/). Gli utenti sono collegati con autorizzazioni e sandbox tramite i profili di prodotto in [!DNL Admin Console].

Questo documento fornisce un riepilogo delle autorizzazioni disponibili per le dashboard, incluse le funzionalità a cui danno accesso e le funzioni utente che abilitano. Per informazioni dettagliate su come ottenere e assegnare le autorizzazioni di accesso, leggi [panoramica sul controllo degli accessi](../access-control/home.md).

## Prerequisiti

Per configurare il controllo degli accessi per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con [!DNL Experience Platform] integrazione dei prodotti. Consulta l’articolo di Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) per ulteriori informazioni.

## Autorizzazioni disponibili per il dashboard {#available-permissions}

Il [!DNL Dashboards] fornisce tre autorizzazioni che, se combinate, forniscono accesso completo al [!UICONTROL Profili], [!UICONTROL Segmenti], [!UICONTROL Destinazioni], e [!UICONTROL Utilizzo licenze] dashboard in Adobe Experience Platform. Queste autorizzazioni sono:

| Autorizzazione | Descrizione |
|---|---|
| **Gestione dashboard standard** | Questa autorizzazione è un **autorizzazione globale di lettura e scrittura**. Ti consente di: [creare widget personalizzati](./customize/custom-widgets.md) e [modificare lo schema del widget](./customize/edit-schema.md) tramite [!UICONTROL Libreria widget]. |
| **Visualizza dashboard standard** | Questo fornisce **sola lettura** funzionalità per [!UICONTROL Profili], [!UICONTROL Destinazioni], e [!UICONTROL Segmenti] e consente di accedervi tramite la navigazione a sinistra di Platform. Aggiunge anche [!UICONTROL Dashboard] nella barra di navigazione a sinistra e accedere al [!UICONTROL Dashboard] scheda inventario e integrazioni. |
| **Visualizza dashboard utilizzo licenze** | Questa autorizzazione consente agli utenti di **sola lettura** accesso a [dashboard utilizzo licenze](./guides/license-usage.md) nell’interfaccia utente di Experience Platform. |

Sono disponibili cinque autorizzazioni non incluse nel [!DNL Dashboard] categoria potenzialmente necessaria a seconda delle esigenze. La tabella seguente illustra le posizioni delle categorie nell’Admin Console:

>[!IMPORTANT]
>
>Entrambe **[!DNL Manage Standard Dashboards]** e **[!DNL View Standard Dashboards]** autorizzazioni **richiedi** un&#39;autorizzazione di &quot;visualizzazione&quot; o &quot;gestione&quot; dal [!DNL Profile Management] o [!DNL Destinations] nell’Admin Console per attivare le sezioni pertinenti nell’interfaccia utente di Platform.

| Autorizzazione | Admin Console posizione categoria |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice di controllo degli accessi

La seguente matrice di controllo di accesso fornisce una suddivisione di quali autorizzazioni sono necessarie e di quale funzione forniscono per quanto riguarda l’accesso alle diverse funzioni del dashboard. Le autorizzazioni sono elencate nella riga orizzontale superiore e l’area di lavoro dell’interfaccia utente di Platform è elencata lungo la colonna sinistra.

|  | [!UICONTROL Visualizza dashboard standard] OPPURE [!UICONTROL Gestisci dashboard standard] | [!UICONTROL Visualizza profili],<br/>[!UICONTROL Visualizzare segmenti],<br/> [!UICONTROL Visualizza destinazioni] | [!UICONTROL Gestire le query] E [!UICONTROL Gestione sandbox] | [!UICONTROL Visualizza dashboard utilizzo licenze] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] nel menu di navigazione a sinistra. | N/D | **È RICHIESTA un&#39;autorizzazione &quot;Visualizza&quot; o &quot;Gestisci&quot;** per ogni dashboard. | N/D | N/D |
| [!DNL Dashboards] nel menu di navigazione a sinistra. | ABILITATO | **È richiesta almeno una**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(scheda Sfoglia) | ABILITATO | N/D | N/D | N/D |
| [!DNL Dashboards] [!DNL Integrations] scheda <br/>(utilizzato per installare Power BI) | ABILITATO | **È richiesta almeno una** | N/D | N/D |
| Pulsante Power BI installazione e flusso di lavoro | ABILITATO | N/D | **OBBLIGATORIO** | N/D |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dashboard.<br/>Possibilità di modificare gli schemi di widget e aggiungere nuovi attributi per la personalizzazione dei widget | **NECESSARIO Manage-standard-dashboard** | **OBBLIGATORIO (per ogni dashboard)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | ABILITATO |

{style="table-layout:auto"}

## Aggiungere le autorizzazioni al profilo di prodotto

Utilizza le informazioni fornite sopra per aggiungere le autorizzazioni appropriate al tuo profilo di prodotto. Per istruzioni complete su, consulta la documentazione di [come aggiungere autorizzazioni tramite l’interfaccia utente di controllo degli accessi](../access-control/ui/permissions.md).

Per le descrizioni delle autorizzazioni, fare riferimento a [autorizzazioni disponibili](#available-permissions) in questo documento.

>[!NOTE]
>
>Non è necessario abilitare tutte le autorizzazioni per tutti gli utenti. A seconda della struttura dell’organizzazione, potrebbe essere utile creare profili di prodotto separati per alcuni utenti e concedere un accesso limitato (ad esempio in sola lettura). Per informazioni, consulta la documentazione sulla gestione degli utenti per un profilo di prodotto. [come assegnare autorizzazioni per utenti specifici](../access-control/ui/users.md).

Dopo aver aggiunto le autorizzazioni di accesso necessarie, gli utenti dell’organizzazione possono iniziare a visualizzare le dashboard all’interno dell’interfaccia utente di Experience Platform ed eseguire altre azioni in base alle autorizzazioni assegnate.
