---
keywords: Experience Platform;guida utente;customer ai;argomenti comuni;controlli di accesso;creare un modello;
solution: Experience Platform
feature: Customer AI
title: Controllo degli accessi per Customer AI
description: Questo documento fornisce informazioni sul controllo degli accessi basato sugli attributi per Customer AI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Controllo dell’accesso basato su attributi

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile solo in una versione limitata.

[Controllo dell&#39;accesso basato su attributi](../../../access-control/abac/overview.md) è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità ti consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia utente e l’interfaccia di amministrazione dei ruoli per definire i criteri di accesso ai campi dello schema XDM e gestire meglio l’accesso dato a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo degli accessi basato sugli attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Grazie al controllo degli accessi basato sugli attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti ai dati personali sensibili (SPD) e alle informazioni personali (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.

A causa del controllo degli accessi basato sugli attributi, alcuni campi e funzionalità avrebbero accesso limitato e non sarebbero disponibili per alcuni modelli di servizio Customer AI. Ad esempio, &quot;Identity&quot;, &quot;Score Definition&quot; e &quot;Clone&quot;.

![Area di lavoro di Customer AI con i campi limitati del modello di servizio evidenziati.](../images/user-guide/unavailable-functionalities.png)

Nella parte superiore dell’area di lavoro di Customer AI **pagina approfondimenti**, noterai che i dettagli nella barra laterale, nella definizione del punteggio, nell’identità e negli attributi di profilo mostrano tutti &quot;Accesso limitato&quot;.

![Area di lavoro di Customer AI con i campi limitati dello schema evidenziati.](../images/user-guide/access-restricted.png)

Quando si visualizzano in anteprima i set di dati con schema limitato nel **[!UICONTROL Crea flusso di lavoro modello]** viene visualizzato un avviso che informa che [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nell’anteprima del set di dati.]

![Area di lavoro di Customer AI con i campi limitati dei set di dati di anteprima con risultati dello schema limitati evidenziati.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Dopo aver creato un modello con informazioni limitate e procedere con il **[!UICONTROL Definire l&#39;obiettivo]** viene visualizzato un avviso nella parte superiore: [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nella configurazione.]

![Area di lavoro di Customer AI con i campi limitati del modello di servizio evidenziati.](../images/user-guide/information-not-displayed-save-and-exit.png)

Quando si utilizza il controllo di accesso, la **Visualizzare Customer AI** e **Gestire l’intelligenza artificiale del cliente** i privilegi concedono l’accesso a diverse funzionalità di Customer AI. La **Gestire l’intelligenza artificiale del cliente** L&#39;autorizzazione consente di: **creare**,**update**, **delete**, **abilita** oppure **disable** un modello **Visualizzare Customer AI** consente di leggerlo o visualizzarlo. La **creare**, **update** e **delete** le azioni vengono registrate dai registri di controllo.

Consulta la documentazione per informazioni [assegnazione di autorizzazioni per il controllo degli accessi](../../../access-control/home.md) o come [utilizzare i registri di controllo per monitorare l’accesso e l’attività](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Passaggi successivi

Leggendo questa guida, ti sono stati introdotti i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. Ora puoi continuare con la [guida utente per il controllo degli accessi](../overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].