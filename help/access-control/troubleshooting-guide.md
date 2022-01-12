---
keywords: Experience Platform;home;argomenti comuni;risoluzione dei problemi;controllo accessi
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
topic-legacy: troubleshooting guide
description: Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '321'
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
