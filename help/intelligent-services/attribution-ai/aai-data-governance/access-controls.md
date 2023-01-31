---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Controllo degli accessi per le Attribution AI
description: Questo documento fornisce informazioni sul controllo degli accessi basato sugli attributi per Attribution AI.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# Controllo degli accessi

Il controllo degli accessi per le Attribution AI è fornito tramite Adobe Experience Platform nella [Adobe Admin Console](https://adminconsole.adobe.com/). Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox.

Per ulteriori informazioni sul controllo degli accessi, consulta la sezione [panoramica sul controllo degli accessi](../../access-control/home).

## Controllo dell’accesso basato su attributi

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile solo in una versione limitata.

[Controllo dell&#39;accesso basato su attributi](../../../help/access-control/abac/overview.md) è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità ti consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia utente e l’interfaccia di amministrazione dei ruoli per definire i criteri di accesso ai campi dello schema XDM e gestire meglio l’accesso dato a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo degli accessi basato sugli attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Grazie al controllo degli accessi basato sugli attributi, gli amministratori possono controllare l’accesso degli utenti ai dati personali sensibili (SPD) e alle informazioni personali identificabili (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.

A causa del controllo dell’accesso basato sugli attributi, alcuni campi e funzionalità potrebbero avere accesso limitato e non essere disponibili per alcuni modelli di servizio Attribution AI. Ad esempio, &quot;Identity&quot;, &quot;Score Definition&quot; e &quot;Clone&quot;.

Nella parte superiore dell’area di lavoro Attribution AI **pagina approfondimenti**, i dettagli visualizzati nella barra laterale hanno accesso limitato.

![Area di lavoro Attribution AI con i campi dello schema limitati evidenziati.](./images/user-guide/access-restricted.png)

Se selezioni set di dati con schemi limitati nel **[!UICONTROL Crea flusso di lavoro modello]** accanto al nome del set di dati viene visualizzato un avviso con il messaggio: [!UICONTROL Sono escluse le informazioni limitate].

![Area di lavoro Attribution AI con i campi set di dati limitati evidenziati.](./images/user-guide/restricted-info-excluded.png)

Quando si visualizzano in anteprima i set di dati con schema limitato nel **[!UICONTROL Crea flusso di lavoro modello]** viene visualizzato un avviso che informa che [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nell’anteprima del set di dati.]

![Area di lavoro Attribution AI con i risultati dei campi dello schema con anteprima limitata evidenziati.](./images/user-guide/restricted-dataset-preview.png)

Dopo aver creato un modello con informazioni limitate, procedere al **[!UICONTROL Definire l&#39;obiettivo]** viene visualizzato un avviso nella parte superiore: [!UICONTROL A causa di restrizioni di accesso, alcune informazioni non vengono visualizzate nella configurazione.]

![L&#39;area di lavoro Attribution AI con i campi limitati dei risultati del modello evidenziati.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Passaggi successivi

Leggendo questa guida, ti sono stati introdotti i principi fondamentali del controllo degli accessi in [!DNL Experience Platform]. Ora puoi continuare con la [guida utente per il controllo degli accessi](./ui/overview.md) per i passaggi dettagliati su come utilizzare [!DNL Admin Console] per creare profili di prodotto e assegnare autorizzazioni per [!DNL Platform].
