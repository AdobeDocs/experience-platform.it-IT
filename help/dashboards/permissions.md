---
solution: Experience Platform
title: Come ottenere e concedere autorizzazioni di accesso per Experienci Platform dashboard
type: Documentation
description: Consente agli utenti di visualizzare, modificare e aggiornare le dashboard di Experience Platform tramite Adobe Admin Console.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f138bb0f1b8d289cc872afc065d31c5e55d4b05c
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 7%

---

# Autorizzazioni di accesso per le dashboard

Per consentire agli utenti di visualizzare, modificare e aggiornare le dashboard, devi prima abilitare le autorizzazioni. In Adobe Experience Platform, il controllo degli accessi viene fornito tramite [Adobe Admin Console](https://adminconsole.adobe.com/). Gli utenti sono collegati a autorizzazioni e sandbox attraverso i profili di prodotto nella sezione [!DNL Admin Console].

Questo documento fornisce un riepilogo delle autorizzazioni disponibili per le dashboard, incluse le funzioni a cui danno accesso e le funzioni utente abilitate. Per informazioni dettagliate su come ottenere e assegnare le autorizzazioni di accesso, si prega di iniziare leggendo il [panoramica sul controllo degli accessi](../access-control/home.md).

## Prerequisiti

Per configurare il controllo di accesso per [!DNL Experience Platform], è necessario disporre dei privilegi di amministratore per un&#39;organizzazione con un [!DNL Experience Platform] integrazione del prodotto. Consulta l’articolo Adobe Help Center su [ruoli amministrativi](https://helpx.adobe.com/enterprise/using/admin-roles.html) per ulteriori informazioni.

## Autorizzazioni del dashboard disponibili {#available-permissions}

La [!DNL Dashboards] il servizio fornisce tre autorizzazioni che, una volta combinate, forniscono accesso completo al [!UICONTROL Profili], [!UICONTROL Segmenti], [!UICONTROL Destinazioni]e [!UICONTROL Utilizzo della licenza] dashboard in Adobe Experience Platform. Queste autorizzazioni sono:

| Autorizzazione | Descrizione |
|---|---|
| **Gestire dashboard standard** | Questa autorizzazione è **autorizzazione globale di lettura e scrittura**. Ti consente di [creare widget personalizzati](./customize/custom-widgets.md) e [modificare lo schema del widget](./customize/edit-schema.md) attraverso [!UICONTROL Libreria widget]. |
| **Visualizza dashboard standard** | Questo fornisce **sola lettura** funzionalità per [!UICONTROL Profili], [!UICONTROL Destinazioni]e [!UICONTROL Segmenti] dashboard e consente di accedervi tramite la navigazione a sinistra di Platform. Aggiunge anche [!UICONTROL Dashboard] alla navigazione a sinistra e all&#39;accesso al [!UICONTROL Dashboard] scheda inventario e integrazioni . |
| **Visualizza dashboard di utilizzo della licenza** | Questa autorizzazione consente agli utenti **sola lettura** accesso [dashboard di utilizzo della licenza](./guides/license-usage.md) nell’interfaccia utente di Experience Platform. |

Ci sono cinque autorizzazioni non incluse nel [!DNL Dashboard] categoria potenzialmente necessaria a seconda delle esigenze. La tabella seguente illustra le posizioni delle rispettive categorie nell’Admin Console:

>[!IMPORTANT]
>
>Entrambi i **[!DNL Manage Standard Dashboards]** e **[!DNL View Standard Dashboards]** permissions **richiedere** un&#39;autorizzazione &quot;visualizza&quot; o &quot;gestisci&quot; dal [!DNL Profile Management] o [!DNL Destinations] nell’Admin Console per attivare le sezioni pertinenti all’interno dell’interfaccia utente di Platform.

| Autorizzazione | Posizione categoria Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrice di controllo degli accessi

La seguente matrice di controllo accessi fornisce un raggruppamento delle autorizzazioni necessarie e della funzione fornita per quanto riguarda l’accesso alle diverse funzioni del dashboard. Le autorizzazioni sono elencate nella riga orizzontale superiore e l’area di lavoro dell’interfaccia utente di Platform è elencata nella colonna a sinistra.

|  | [!UICONTROL Visualizza dashboard standard] O [!UICONTROL Gestione dashboard standard] | [!UICONTROL Visualizza profili],<br/>[!UICONTROL Visualizzare i segmenti],<br/> [!UICONTROL Visualizzare le destinazioni] | [!UICONTROL Gestire le query] &amp; [!UICONTROL Gestire le sandbox] | [!UICONTROL Visualizza dashboard di utilizzo della licenza] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] nella navigazione a sinistra. | N/D | **È RICHIESTA un&#39;autorizzazione &quot;Visualizza&quot; o &quot;Gestisci&quot;** per ogni dashboard corrispondente. | N/D | N/D |
| [!DNL Dashboards] nella navigazione a sinistra. | ATTIVATO | **Almeno un**. | N/D | N/D |
| [!DNL Dashboards] [!DNL Inventory] <br/>(scheda Sfoglia) | ATTIVATO | N/D | N/D | N/D |
| [!DNL Dashboards] [!DNL Integrations] scheda <br/>(utilizzato per installare Power BI) | ATTIVATO | **Almeno un** | N/D | N/D |
| Pulsante Power BI Install e flusso di lavoro | ATTIVATO | N/D | **OBBLIGATORIO** | N/D |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] dashboard.<br/>Possibilità di modificare gli schemi di widget e di aggiungere nuovi attributi per la personalizzazione dei widget | **Gestione dashboard standard RICHIESTO** | **OBBLIGATORIO (per ciascun dashboard)** | N/D | N/D |
| [!DNL License Usage Dashboard] | N/D | N/D | N/D | ATTIVATO |

{style=&quot;table-layout:auto&quot;}

## Aggiungere autorizzazioni al profilo di prodotto

Utilizza le informazioni fornite sopra per aggiungere le autorizzazioni appropriate al tuo profilo di prodotto. Consulta la documentazione per le istruzioni complete su [come aggiungere autorizzazioni tramite l’interfaccia utente del controllo accessi](../access-control/ui/permissions.md).

Per una descrizione delle autorizzazioni, consulta la [autorizzazioni disponibili](#available-permissions) sezione precedente in questo documento.

>[!NOTE]
>
>Non è necessario abilitare tutte le autorizzazioni per tutti gli utenti. A seconda della struttura della tua organizzazione, puoi creare profili di prodotto separati per alcuni utenti e concedere un accesso limitato (ad esempio in sola lettura). Consulta la documentazione sulla gestione degli utenti per un profilo di prodotto per ulteriori informazioni [come assegnare autorizzazioni per utenti specifici](../access-control/ui/users.md).

Dopo aver aggiunto le autorizzazioni di accesso necessarie, gli utenti all’interno dell’organizzazione possono iniziare a visualizzare le dashboard nell’interfaccia utente di Experience Platform ed eseguire altre azioni in base alle autorizzazioni assegnate.
