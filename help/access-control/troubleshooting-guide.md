---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida alla risoluzione dei problemi di controllo degli accessi
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Guida alla risoluzione dei problemi di controllo degli accessi

Questo documento contiene le risposte alle domande frequenti sul controllo degli accessi in Adobe Experience Platform. Per domande e risoluzione dei problemi relativi ad altri servizi della piattaforma, consulta la guida [alla risoluzione dei problemi della piattaforma](../landing/troubleshooting.md)Experience.

Experience Platform sfrutta i profili di prodotto in [Adobe Admin Console](http://adminconsole.adobe.com) per fornire un controllo **degli** accessi basato sui ruoli, collegando gli utenti con autorizzazioni e sandbox.  Per ulteriori informazioni, consulta la panoramica [sul controllo](home.md) degli accessi.

## Dove posso trovare le mie autorizzazioni di accesso correnti?

Se sei un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto per la tua organizzazione IMS, puoi visualizzare il profilo di prodotto assegnato e le autorizzazioni che fornisce all’interno di Adobe Admin Console. Consulta la guida [utente per il controllo degli](./ui/overview.md) accessi per istruzioni su come navigare nell&#39;Admin Console per visualizzare le autorizzazioni di un profilo di prodotto.

Se non sei un amministratore, puoi comunque visualizzare le autorizzazioni di accesso correnti inviando una richiesta all’ `/acl/effective-policies` endpoint nell’API di controllo degli accessi. Per ulteriori informazioni, consulta la sezione &quot;Visualizza criteri effettivi&quot; nella guida [per gli sviluppatori del controllo](./api/effective-policies.md) degli accessi.

## Alcune funzioni nell’interfaccia utente della piattaforma non sono disponibili. In che modo l&#39;accesso a queste funzioni è controllato dalle autorizzazioni?

Se non disponete delle autorizzazioni di accesso per una particolare funzione Piattaforma, tale funzione verrà nascosta o disattivata nell’interfaccia utente della piattaforma. Ad esempio, per visualizzare la scheda &quot;Profili&quot;, è necessario disporre delle autorizzazioni &quot;Visualizza profili&quot; o &quot;Gestisci profili&quot;. Contatta il tuo amministratore se hai bisogno di autorizzazioni aggiuntive per le funzionalità di Experience Platform.

## In che modo sono raggruppate le autorizzazioni e quale gruppo contiene l&#39;autorizzazione da utilizzare?

Le autorizzazioni sono raggruppate e suddivise in categorie in base alle funzionalità della piattaforma a cui si applicano (come Gestione dati e Gestione profili). Per un elenco completo delle autorizzazioni disponibili e dei gruppi a cui appartengono, consultate la sezione [](home.md#permissions) Autorizzazioni nella panoramica sul controllo di accesso.

Per ulteriori informazioni sulla fornitura di controlli di accesso basati sui ruoli, consultate la panoramica [sul controllo di](home.md) accesso.