---
keywords: Experience Platform;guida introduttiva;attribuzione ai;argomenti più comuni
feature: Attribution AI
title: Guida introduttiva di Attribution AI
description: Le seguenti guide richiedono una comprensione dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo di IA per l’attribuzione. Prima di iniziare le esercitazioni, consulta i seguenti documenti.
exl-id: ab269c24-97ac-4da9-9b6c-7d2dde61f0dc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 6%

---

# Guida introduttiva ad Attribution AI

Per le guide seguenti è necessario conoscere i vari servizi [!DNL Adobe Experience Platform] coinvolti nell&#39;utilizzo di IA per l&#39;attribuzione. Prima di iniziare le esercitazioni, consulta i seguenti documenti:

- [Panoramica del sistema Experience Data Model (XDM)](../../xdm/home.md): XDM è il framework fondamentale che consente a [!DNL Adobe Experience Cloud], con tecnologia Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto. La metodologia su cui è basato Experience Platform, il sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Experience Platform.
- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): questo documento fornisce un&#39;introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): questo tutorial illustra i passaggi necessari per la creazione di uno schema tramite l&#39;Editor di schema in Experience Platform.

IA per l’attribuzione richiede set di dati per la conformità allo schema Consumer Experience Events (CEE), che è un gruppo di campi dello schema [Experience Data Model (XDM)](../../xdm/home.md). Contatta il supporto Adobe all’indirizzo attributionai-support@adobe.com per implementare o modificare questi dati. Se sono presenti dati sulla spesa dei supporti, puoi eseguire ulteriori analisi, ad esempio ricavi incrementali e ROI. Se i dati del profilo cliente sono disponibili, è possibile attribuire ulteriori crediti al livello del profilo cliente.

## Terminologia

- **Evento di conversione:** qualsiasi evento digitale o interazione digitale eseguito dai clienti per indicare una fase cardine verso un obiettivo, ad esempio le registrazioni di conferenze. Altri esempi includono conversioni a pagamento, iscrizioni gratuite a un account o qualifiche per una caratteristica.

- **Punto di contatto:** qualsiasi evento digitale o interazione digitale eseguita dai clienti nel percorso verso un obiettivo. Alcuni esempi includono le attività di marketing correlate al periodo precedente all’acquisto, le impression pubblicitarie visualizzate e i clic di ricerca a pagamento.

## Download dei punteggi di IA per l’attribuzione

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e procedere ai [passaggi successivi](#next-steps).

Il download dei punteggi di IA per l’attribuzione viene eseguito tramite una combinazione di chiamate API. Per effettuare chiamate alle API di Experience Platform, devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in Experience Platform sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API di Experience Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Controllo degli accessi {#access-control}

Quando si utilizza il controllo degli accessi basato sui ruoli, i privilegi **Visualizza IA per l&#39;attribuzione** e **Gestisci IA per l&#39;attribuzione** concedono l&#39;accesso a diverse funzionalità di IA per l&#39;attribuzione. **Gestisci IA per l&#39;attribuzione** consente di **creare**, **clone**, **modificare**, **eliminare**, **abilitare** o **disabilitare** un&#39;istanza mentre **Visualizza IA per l&#39;attribuzione** consente di **leggere** o **visualizzarla**. Le azioni **create**, **edit** e **delete** vengono registrate nei registri di controllo.

Consulta la documentazione per scoprire [come assegnare le autorizzazioni per il controllo degli accessi](../../../help/access-control/home.md) o come [utilizzare i registri di audit per monitorare gli accessi e l&#39;attività](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Passaggi successivi {#next-steps}

Una volta che sei pronto e hai impostato tutte le credenziali e gli schemi, inizia seguendo la [guida all&#39;interfaccia utente di IA per l&#39;attribuzione](./user-guide.md). Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.
