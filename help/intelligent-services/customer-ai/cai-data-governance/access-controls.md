---
keywords: Experience Platform;guida utente;ia clienti;argomenti popolari;controlli di accesso;creare un modello;
solution: Experience Platform
feature: Customer AI
title: Controllo dell’accesso per IA per l’analisi dei clienti
description: Questo documento fornisce informazioni sul controllo degli accessi basato su attributi per IA per l’analisi dei clienti.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Controllo dell’accesso basato su attributi

>[!IMPORTANT]
>
>Il controllo degli accessi basato su attributi è attualmente disponibile solo in una versione limitata.

[Controllo degli accessi basato su attributi](../../../access-control/abac/overview.md) è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. Parallelamente, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso relativi ai campi dello schema XDM e gestire in modo migliore l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo dell’accesso basato su attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Tramite il controllo degli accessi basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti sia ai dati personali sensibili (SPD) che alle informazioni personali (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

A causa del controllo dell’accesso basato su attributi, alcuni campi e funzionalità avrebbero accesso limitato e non sarebbero disponibili per alcuni modelli di servizio di IA per l’analisi dei clienti. Alcuni esempi includono &quot;Identity&quot;, &quot;Score Definition&quot; e &quot;Clone&quot;.

![L’area di lavoro Customer AI con i campi limitati dei risultati del modello di servizio evidenziati.](../images/user-guide/unavailable-functionalities.png)

Nella parte superiore dell’area di lavoro di Customer AI **pagina approfondimenti**, i dettagli nella barra laterale, la definizione del punteggio, l’identità e gli attributi del profilo mostrano tutti &quot;Accesso limitato&quot;.

![L’area di lavoro di Customer AI con i campi limitati dello schema evidenziati.](../images/user-guide/access-restricted.png)

Quando visualizzi l’anteprima dei set di dati con schema limitato sul **[!UICONTROL Crea flusso di lavoro modello]** , viene visualizzato un avviso che informa che [!UICONTROL A causa delle restrizioni di accesso, alcune informazioni non vengono visualizzate nell’anteprima del set di dati.]

![L’area di lavoro Customer AI con i campi limitati dei set di dati di anteprima ed evidenziati i risultati con schema limitato.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Dopo aver creato un modello con informazioni limitate, passare alla **[!UICONTROL Definisci l’obiettivo]** fase, nella parte superiore viene visualizzato un avviso: [!UICONTROL A causa delle restrizioni di accesso, alcune informazioni non vengono visualizzate nella configurazione.]

![L’area di lavoro Customer AI con i campi limitati dei risultati del modello di servizio evidenziati.](../images/user-guide/information-not-displayed-save-and-exit.png)

Quando si utilizza il controllo degli accessi, **Visualizza Customer AI** e **Gestire Customer AI** I privilegi consentono l’accesso a diverse funzionalità di Customer AI. Il **Gestire Customer AI** autorizzazione consente di: **creare**,**aggiorna**, **eliminare**, **abilita**, o **disable** un modello mentre **Visualizza Customer AI** consente di leggerlo o visualizzarlo. Il **creare**, **aggiorna** e **eliminare** le azioni vengono registrate dai registri di audit.

Consulta la documentazione per saperne di più [assegnazione delle autorizzazioni per il controllo degli accessi](../../../access-control/home.md) o come [utilizzare i registri di audit per monitorare accesso e attività](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Passaggi successivi

Una volta letta questa guida, potrai scoprire i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. Ora puoi passare alla sezione [guida utente al controllo degli accessi](../overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].