---
keywords: Experience Platform;home;argomenti popolari;risoluzione dei problemi;controllo degli accessi
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
description: Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi del controllo degli accessi

Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], fare riferimento alla [guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com) per fornire il controllo degli accessi basato sui ruoli, collegando gli utenti con autorizzazioni e sandbox.  Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](home.md).

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore del profilo di prodotto della tua organizzazione, puoi visualizzare il tuo profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno di Adobe Admin Console. Per istruzioni su come esplorare [!DNL Admin Console] per visualizzare le autorizzazioni di un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md).

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta all&#39;endpoint `/acl/effective-policies` nell&#39;API di controllo degli accessi. Per ulteriori informazioni, vedere la sezione &quot;View effective policies&quot; nella [guida per gli sviluppatori del controllo degli accessi](./api/effective-policies.md).

## Alcune funzionalità nell&#39;interfaccia utente di [!DNL Platform] non sono disponibili. In che modo l’accesso a queste funzioni è controllato dalle autorizzazioni?

Se non si dispone delle autorizzazioni di accesso per una caratteristica [!DNL Platform] specifica, tale caratteristica verrà nascosta o disattivata nell&#39;interfaccia utente [!DNL Experience Platform]. Ad esempio, per visualizzare la scheda &quot;[!UICONTROL Profili]&quot; è necessario disporre delle autorizzazioni &quot;[!UICONTROL Visualizza profili]&quot; o &quot;[!UICONTROL Gestisci profili]&quot;. Contattare l&#39;amministratore se sono necessarie ulteriori autorizzazioni per le funzionalità di [!DNL Experience Platform].

## Come vengono raggruppate le autorizzazioni e quale gruppo contiene l’autorizzazione che desidero utilizzare?

Le autorizzazioni sono raggruppate e classificate in base alle funzionalità [!DNL Platform] a cui si applicano (ad esempio [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, vedere la sezione [autorizzazioni](home.md#permissions) nella panoramica del controllo di accesso.

Per ulteriori informazioni su come fornire il controllo degli accessi basato sui ruoli, vedere la [panoramica sul controllo degli accessi](home.md).

## Cosa succede alle autorizzazioni dopo la migrazione da Adobe IO a Business ID?

Per la concessione delle autorizzazioni, il controllo degli accessi utilizza l’ID utente (un ID univoco interno assegnato a un utente). Quando un’organizzazione viene migrata da Adobe ID a Business ID, tutte le autorizzazioni impostate per i relativi utenti andranno perse perché l’ID utente viene modificato e il controllo degli accessi utilizzerà l’ID utente appena generato. Se la tua organizzazione è stata migrata al Business ID, contatta il rappresentante del tuo Adobe per migrare il tuo ID utente da Adobe ID al Business ID.
