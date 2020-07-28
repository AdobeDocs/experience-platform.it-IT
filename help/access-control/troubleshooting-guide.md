---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---


# Guida alla risoluzione dei problemi di controllo degli accessi

Questo documento contiene le risposte alle domande frequenti sul controllo degli accessi in  Adobe Experience Platform. Per le domande e la risoluzione dei problemi relativi ad altri [!DNL Platform] servizi, consulta la guida alla risoluzione dei problemi del [Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto in [Adobe Admin Console](http://adminconsole.adobe.com) per fornire un controllo **dell&#39;** accesso basato sui ruoli, collegando gli utenti con autorizzazioni e sandbox.  Per ulteriori informazioni, consulta la panoramica [sul controllo](home.md) degli accessi.

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto per l’organizzazione IMS, puoi visualizzare il profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno dell’Adobe Admin Console. Consulta la guida [utente per il controllo](./ui/overview.md) degli accessi per istruzioni su come navigare all&#39;interno del [!DNL Admin Console] profilo di prodotto per visualizzare le autorizzazioni di un profilo di prodotto.

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta all’ `/acl/effective-policies` endpoint nell’API di controllo degli accessi. Per ulteriori informazioni, consulta la sezione &quot;Visualizza criteri effettivi&quot; nella guida [per gli sviluppatori del controllo](./api/effective-policies.md) degli accessi.

## Alcune funzioni nell’ [!DNL Platform] interfaccia utente non sono disponibili. In che modo l&#39;accesso a queste funzioni è controllato dalle autorizzazioni?

Se non disponete delle autorizzazioni di accesso per una particolare [!DNL Platform] funzione, tale funzione verrà nascosta o disattivata nell’ [!DNL Experience Platform] interfaccia utente. Ad esempio, per visualizzare la scheda &quot;[!UICONTROL Profiles]&quot;, è necessario disporre delle autorizzazioni &quot;[!UICONTROL View Profiles]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;. Contatta l’amministratore se hai bisogno di autorizzazioni aggiuntive per [!DNL Experience Platform] le funzionalità.

## In che modo sono raggruppate le autorizzazioni e quale gruppo contiene l&#39;autorizzazione da utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie in base alle [!DNL Platform] funzionalità a cui si applicano (ad esempio [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, consultate la sezione [](home.md#permissions) Autorizzazioni nella panoramica sul controllo di accesso.

Per ulteriori informazioni sulla fornitura di controlli di accesso basati sui ruoli, consultate la panoramica [sul controllo di](home.md) accesso.