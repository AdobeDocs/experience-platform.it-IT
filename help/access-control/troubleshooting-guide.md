---
keywords: ' Experience Platform;home;argomenti più comuni;risoluzione dei problemi;controllo degli accessi'
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
topic: troubleshooting guide
description: Questo documento contiene le risposte alle domande frequenti sul controllo degli accessi in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi di controllo degli accessi

Questo documento contiene le risposte alle domande frequenti sul controllo degli accessi in Adobe Experience Platform. Per le domande e la risoluzione dei problemi relativi ad altri servizi [!DNL Platform], fare riferimento alla [Guida alla risoluzione dei problemi  Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto nella  [ Admin ](http://adminconsole.adobe.com) Console del Adobe per fornire un controllo dell&#39;accesso basato sui ruoli, collegando gli utenti con autorizzazioni e sandbox.  Per ulteriori informazioni, vedere la [panoramica sul controllo degli accessi](home.md).

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto per l’organizzazione IMS, puoi visualizzare il profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno dell’Adobe Admin Console. Per istruzioni su come navigare all&#39; [!DNL Admin Console] per visualizzare le autorizzazioni di un profilo di prodotto, vedere la [guida utente del controllo di accesso](./ui/overview.md).

Se non si è un amministratore, è comunque possibile visualizzare le autorizzazioni di accesso correnti inviando una richiesta all&#39;endpoint `/acl/effective-policies` nell&#39;API di controllo di accesso. Per ulteriori informazioni, vedere la sezione &quot;Visualizza criteri effettivi&quot; in [guida per gli sviluppatori di controlli di accesso](./api/effective-policies.md).

## Alcune funzionalità nell&#39;interfaccia di [!DNL Platform] non sono disponibili. In che modo l&#39;accesso a queste funzioni è controllato dalle autorizzazioni?

Se non disponete delle autorizzazioni di accesso per una particolare funzione [!DNL Platform], tale funzionalità verrà nascosta o disattivata nell&#39;interfaccia di [!DNL Experience Platform]. Ad esempio, per visualizzare la scheda &quot;[!UICONTROL Profiles]&quot;, è necessario disporre delle autorizzazioni &quot;[!UICONTROL View Profiles]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;. Contattate l&#39;amministratore se avete bisogno di autorizzazioni aggiuntive per le funzionalità [!DNL Experience Platform].

## In che modo sono raggruppate le autorizzazioni e quale gruppo contiene l&#39;autorizzazione da utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie in base alle [!DNL Platform] funzionalità a cui si applicano (ad esempio [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, consultate la sezione [permissions](home.md#permissions) nella panoramica sul controllo di accesso.

Per ulteriori informazioni sulla fornitura di controlli di accesso basati sui ruoli, vedere la [panoramica sul controllo di accesso](home.md).