---
solution: Experience Platform
title: Ottenere e concedere autorizzazioni di accesso per dashboard di Experience Platform
type: Documentation
description: Consente agli utenti di visualizzare, modificare e aggiornare dashboard di Experience Platform tramite Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 6%

---

# Autorizzazioni di accesso per le dashboard

Per consentire agli utenti di visualizzare, modificare e aggiornare le dashboard, devi prima abilitare le autorizzazioni. In Adobe Experience Platform, il controllo degli accessi viene fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com/). Gli utenti sono collegati con autorizzazioni e sandbox tramite i profili di prodotto in [!DNL Admin Console].

Questo documento fornisce un riepilogo delle autorizzazioni disponibili per le dashboard, incluse le funzionalità a cui danno accesso e le funzioni utente che abilitano. Per informazioni dettagliate su come ottenere e assegnare le autorizzazioni di accesso, leggere la [panoramica sul controllo di accesso](../access-control/home.md).

## Prerequisiti

Per configurare il controllo degli accessi per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con un&#39;integrazione di prodotto [!DNL Experience Platform]. Per ulteriori informazioni, consulta l&#39;articolo di Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/it/enterprise/using/admin-roles.html).

## Autorizzazioni disponibili per il dashboard {#available-permissions}

Il servizio [!DNL Dashboards] fornisce tre autorizzazioni che, se combinate, forniscono accesso completo ai [!UICONTROL Profili], [!UICONTROL Segmenti], [!UICONTROL Destinazioni] e [!UICONTROL Utilizzo licenze] all&#39;interno di Adobe Experience Platform. Queste autorizzazioni sono:

| Autorizzazione | Descrizione |
|---|---|
| **Gestione dashboard standard** | Questa autorizzazione è un **autorizzazione globale di lettura e scrittura**. Consente di [creare widget personalizzati](./customize/custom-widgets.md) e [modificare lo schema widget](./customize/edit-schema.md) tramite la [!UICONTROL libreria widget]. |
| **Visualizza dashboard standard** | In questo modo viene fornita la funzionalità **sola lettura** per i dashboard [!UICONTROL Profili], [!UICONTROL Destinazioni] e [!UICONTROL Segmenti] e viene consentito l&#39;accesso a tali dashboard tramite la navigazione a sinistra di Platform. Aggiunge inoltre [!UICONTROL Dashboard] alla barra di navigazione a sinistra e consente di accedere alla scheda Inventario e integrazioni [!UICONTROL Dashboard]. |
| **Visualizza dashboard utilizzo licenze** | Questa autorizzazione consente agli utenti **di sola lettura** di accedere al [dashboard sull&#39;utilizzo delle licenze](./guides/license-usage.md) nell&#39;interfaccia utente di Experience Platform. |

Cinque autorizzazioni non incluse nella categoria [!DNL Dashboard] sono potenzialmente necessarie a seconda delle tue esigenze. La tabella seguente illustra le posizioni delle categorie nell’Admin Console:

>[!IMPORTANT]
>
>Sia le autorizzazioni **[!DNL Manage Standard Dashboards]** che le autorizzazioni **[!DNL View Standard Dashboards]** **richiedono** un&#39;autorizzazione &quot;visualizzazione&quot; o &quot;gestione&quot; dalla categoria [!DNL Profile Management] o [!DNL Destinations] nell&#39;Admin Console per attivare le sezioni rilevanti nell&#39;interfaccia utente di Platform.

| Autorizzazione | Admin Console posizione categoria |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice di controllo degli accessi

La seguente matrice di controllo di accesso fornisce una suddivisione di quali autorizzazioni sono necessarie e di quale funzione forniscono per quanto riguarda l’accesso alle diverse funzioni del dashboard. Le autorizzazioni sono elencate nella riga orizzontale superiore e l’area di lavoro dell’interfaccia utente di Platform è elencata lungo la colonna sinistra.

|   | [!UICONTROL Visualizza dashboard standard] O [!UICONTROL Gestisci dashboard standard] | [!UICONTROL Visualizza profili],<br/>[!UICONTROL Visualizza segmenti],<br/> [!UICONTROL Visualizza destinazioni] | [!UICONTROL Gestisci query] e [!UICONTROL Gestisci sandbox] | [!UICONTROL Visualizza dashboard utilizzo licenze] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] nel menu di navigazione a sinistra. | N/D | **È RICHIESTA l&#39;autorizzazione &quot;Visualizza&quot; o &quot;Gestisci&quot;** per ogni dashboard corrispondente. | N/D | N/D |
| [!DNL Dashboards] nel menu di navigazione a sinistra. | ABILITATO | **È richiesta almeno una**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(scheda Sfoglia) | ABILITATO | N/D | N/D | N/D |
| [!DNL Dashboards] [!DNL Integrations] scheda <br/> (utilizzata per installare Power BI) | ABILITATO | **È necessario almeno un elemento** | N/D | N/D |
| Pulsante Power BI installazione e flusso di lavoro | ABILITATO | N/D | **OBBLIGATORIO** | N/D |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dashboard.<br/>Possibilità di modificare gli schemi dei widget e di aggiungere nuovi attributi per la personalizzazione dei widget | **È RICHIESTA LA GESTIONE DEL Dashboard STANDARD** | **OBBLIGATORIO (per ogni dashboard)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | ABILITATO |

{style="table-layout:auto"}

## Aggiungere le autorizzazioni al profilo di prodotto

Utilizza le informazioni fornite sopra per aggiungere le autorizzazioni appropriate al tuo profilo di prodotto. Per istruzioni complete su [come aggiungere le autorizzazioni tramite l&#39;interfaccia utente di controllo degli accessi](../access-control/ui/permissions.md), vedere la documentazione.

Per le descrizioni delle autorizzazioni, fare riferimento alla sezione [autorizzazioni disponibili](#available-permissions) precedente in questo documento.

>[!NOTE]
>
>Non è necessario abilitare tutte le autorizzazioni per tutti gli utenti. A seconda della struttura dell’organizzazione, potrebbe essere utile creare profili di prodotto separati per alcuni utenti e concedere un accesso limitato (ad esempio in sola lettura). Per informazioni su [come assegnare le autorizzazioni per utenti specifici](../access-control/ui/users.md), consulta la documentazione sulla gestione degli utenti per un profilo di prodotto.

Dopo aver aggiunto le autorizzazioni di accesso necessarie, gli utenti dell’organizzazione possono iniziare a visualizzare le dashboard all’interno dell’interfaccia utente di Experience Platform ed eseguire altre azioni in base alle autorizzazioni assegnate.
