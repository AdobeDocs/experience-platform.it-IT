---
keywords: Experience Platform;home;argomenti comuni;risoluzione dei problemi;controllo accessi
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
topic-legacy: troubleshooting guide
description: Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di controllo degli accessi

Questo documento fornisce le risposte alle domande più frequenti sul controllo degli accessi in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi [!DNL Platform], consulta la [Guida alla risoluzione dei problemi di Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] sfrutta i profili di prodotto in  [Adobe Admin Console ](http://adminconsole.adobe.com) per fornire un controllo degli accessi basato sui ruoli, collegando gli utenti con autorizzazioni e sandbox.  Per ulteriori informazioni, consulta la [panoramica sul controllo degli accessi](home.md) .

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto per la tua organizzazione IMS, puoi visualizzare il tuo profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno di Adobe Admin Console. Per istruzioni su come navigare [!DNL Admin Console] per visualizzare le autorizzazioni di un profilo di prodotto, consulta la [guida utente per il controllo degli accessi](./ui/overview.md) .

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta all’ endpoint `/acl/effective-policies` nell’API di controllo accessi. Per ulteriori informazioni, consulta la sezione &quot;Visualizzare i criteri effettivi&quot; in [guida per gli sviluppatori del controllo di accesso](./api/effective-policies.md).

## Alcune funzionalità nell’ interfaccia utente di [!DNL Platform] non sono disponibili. In che modo l’accesso a queste funzioni è controllato dalle autorizzazioni?

Se non disponi delle autorizzazioni di accesso per una particolare funzione [!DNL Platform], tale funzione sarà nascosta o disattivata nell’ interfaccia utente di [!DNL Experience Platform] . Ad esempio, per visualizzare la scheda &quot;[!UICONTROL Profiles]&quot;, è necessario disporre delle autorizzazioni &quot;[!UICONTROL View Profiles]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;. Contatta l’amministratore se hai bisogno di autorizzazioni aggiuntive per le funzionalità [!DNL Experience Platform] .

## Come sono raggruppate le autorizzazioni e quale gruppo contiene l&#39;autorizzazione che voglio utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie in base alle funzionalità [!DNL Platform] a cui si applicano (ad esempio [!DNL Data Management] e [!DNL Profile Management]). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, consulta la sezione [autorizzazioni](home.md#permissions) nella panoramica del controllo accessi.

Per ulteriori informazioni su come fornire un controllo degli accessi basato su ruolo, consulta la [panoramica sul controllo degli accessi](home.md) .
