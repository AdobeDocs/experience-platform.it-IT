---
keywords: Experience Platform;home;argomenti popolari;risoluzione dei problemi;controllo degli accessi
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
description: Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del controllo degli accessi

Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, fare riferimento al [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com) per fornire un controllo dell’accesso basato sui ruoli, collegare gli utenti con autorizzazioni e sandbox.  Consulta la [panoramica sul controllo degli accessi](home.md) per ulteriori informazioni.

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore del profilo di prodotto per la tua organizzazione IMS, puoi visualizzare il profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno di Adobe Admin Console. Consulta la [guida utente al controllo degli accessi](./ui/overview.md) per istruzioni su come navigare in [!DNL Admin Console] per visualizzare le autorizzazioni di un profilo di prodotto.

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta a `/acl/effective-policies` nell’API di controllo degli accessi. Consulta la sezione &quot;Visualizzare i criteri effettivi&quot; in [guida per gli sviluppatori sul controllo degli accessi](./api/effective-policies.md) per ulteriori informazioni.

## Alcune funzioni di [!DNL Platform] Interfaccia utente non disponibile. In che modo l’accesso a queste funzioni è controllato dalle autorizzazioni?

Se non disponi delle autorizzazioni di accesso per un particolare [!DNL Platform] , tale funzione sarà nascosta o disattivata nella [!DNL Experience Platform] UI. Ad esempio, per visualizzare il &quot;[!UICONTROL Profili]&quot;, è necessario disporre della scheda &quot;[!UICONTROL Visualizza profili]&quot; o &quot;[!UICONTROL Gestisci profili]&quot; autorizzazioni. Contatta l’amministratore se hai bisogno di autorizzazioni aggiuntive per [!DNL Experience Platform] funzionalità.

## Come vengono raggruppate le autorizzazioni e quale gruppo contiene l’autorizzazione che desidero utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie in base al [!DNL Platform] le funzionalità a cui si applicano (come [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, vedere [sezione autorizzazioni](home.md#permissions) nella panoramica del controllo degli accessi.

Consulta la [panoramica sul controllo degli accessi](home.md) per ulteriori informazioni su come fornire il controllo degli accessi basato sui ruoli.

## Cosa succede alle autorizzazioni dopo la migrazione da Adobe IO a Business ID?

Per la concessione delle autorizzazioni, il controllo degli accessi utilizza l’ID utente (un ID univoco interno assegnato a un utente). Quando un’organizzazione viene migrata da Adobe ID a Business ID, tutte le autorizzazioni impostate per i relativi utenti andranno perse perché l’ID utente viene modificato e il controllo degli accessi utilizzerà l’ID utente appena generato. Se la tua organizzazione è stata migrata al Business ID, contatta il rappresentante del tuo Adobe per migrare il tuo ID utente da Adobe ID al Business ID.
