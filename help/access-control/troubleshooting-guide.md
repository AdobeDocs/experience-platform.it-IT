---
keywords: Experience Platform;home;argomenti comuni;risoluzione dei problemi;controllo accessi
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
description: Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di controllo degli accessi

Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altre [!DNL Platform] i servizi [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto nel [Adobe Admin Console](https://adminconsole.adobe.com) per fornire un controllo degli accessi basato su ruoli, collegare gli utenti con autorizzazioni e sandbox.  Consulta la sezione [panoramica sul controllo degli accessi](home.md) per ulteriori informazioni.

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto per la tua organizzazione IMS, puoi visualizzare il tuo profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno di Adobe Admin Console. Consulta la sezione [guida utente per il controllo degli accessi](./ui/overview.md) per istruzioni su come navigare nel [!DNL Admin Console] per visualizzare le autorizzazioni di un profilo di prodotto.

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta al `/acl/effective-policies` endpoint nell&#39;API di controllo di accesso. Vedi la sezione &quot;Visualizza criteri efficaci&quot; in [guida per sviluppatori di controllo accessi](./api/effective-policies.md) per ulteriori informazioni.

## Alcune funzionalità nel [!DNL Platform] Interfaccia utente non disponibile. In che modo l’accesso a queste funzioni è controllato dalle autorizzazioni?

Se non si dispone delle autorizzazioni di accesso per una particolare [!DNL Platform] questa funzione verrà nascosta o disattivata nella [!DNL Experience Platform] Interfaccia utente. Ad esempio, per visualizzare il &quot;[!UICONTROL Profili]&quot;, è necessario disporre della scheda &quot;[!UICONTROL Visualizza profili]&quot; o &quot;[!UICONTROL Gestisci profili]&quot; autorizzazioni. Contatta l’amministratore se hai bisogno di autorizzazioni aggiuntive per [!DNL Experience Platform] funzionalità.

## Come sono raggruppate le autorizzazioni e quale gruppo contiene l&#39;autorizzazione che voglio utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie dalla [!DNL Platform] funzionalità a cui si applicano (ad esempio [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, consulta la sezione [sezione autorizzazioni](home.md#permissions) nella panoramica sul controllo accessi.

Consulta la sezione [panoramica sul controllo degli accessi](home.md) per ulteriori informazioni su come fornire un controllo dell&#39;accesso basato sui ruoli.

## Cosa succede alle autorizzazioni dopo la migrazione da Adobe IO a Business ID?

Il controllo di accesso utilizza l&#39;ID utente (un ID univoco interno assegnato a un utente) per concedere le autorizzazioni. Quando un&#39;organizzazione viene migrata da Adobe ID a Business ID, tutte le autorizzazioni impostate per i suoi utenti andranno perse perché l&#39;ID utente cambia e il controllo degli accessi utilizza l&#39;ID utente appena generato. Se la tua organizzazione viene migrata a Business ID, contatta il tuo rappresentante di Adobe per migrare il tuo ID utente da Adobe ID a Business ID.
