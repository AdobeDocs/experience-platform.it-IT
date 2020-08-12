---
title: 'Note sulla versione di Adobe Experience Platform '
description: ' note sulla versione del Experience Platform ottobre, 2020'
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: e9d7a045a88e0126549adcfa6136684e7b933b71
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: Ottobre 2020**

Nuove funzioni in Adobe Experience Platform:

- [!DNL Access control](#access-control)
- [!DNL Sandboxes](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] sfrutta i profili di prodotto [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l&#39;accesso a diverse funzionalità della piattaforma, tra cui la modellazione dei dati, la gestione dei profili e l&#39;amministrazione della sandbox.

**Funzionalità chiave**

| Funzione | Descrizione |
|--- | ---|
| Autorizzazioni | In [!DNL Admin Console], la scheda all&#39;interno di un profilo di [!DNL Platform] prodotto consente di personalizzare [!DNL Platform] le funzionalità disponibili per gli utenti collegati a tale profilo. Le categorie di autorizzazioni disponibili includono: [!UICONTROL Data Modeling], [!UICONTROL Data Management], [!UICONTROL Profile Management], [!UICONTROL Identities], [!UICONTROL Data Monitoring], [!UICONTROL Sandbox Administration], [!UICONTROL Destinations], [!UICONTROL Sources]. |
| Accesso alle sandbox | La scheda [!UICONTROL _Autorizzazioni _]all&#39;interno di un profilo di[!DNL Platform]prodotto può consentire agli utenti l&#39;accesso a sandbox specifiche. Per ulteriori informazioni, consultate la sezione sulle[sandbox](#sandboxes)di seguito. |

Per ulteriori informazioni, consulta la panoramica [sul controllo](../../access-control/home.md)degli accessi.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e all&#39;implementazione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, [!DNL Experience Platform] fornisce sandbox che dividono una singola [!DNL Platform] istanza in ambienti virtuali separati per aiutare a sviluppare e sviluppare applicazioni di esperienza digitale.

**Funzionalità chiave**

| Funzione | Descrizione |
|--- | ---|
| Sandbox produzione | [!DNL Experience Platform] fornisce una singola sandbox di produzione, che non può essere eliminata o reimpostata. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per una singola [!DNL Platform] istanza, per testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sul sandbox di produzione. |
| Switcher sandbox | Nell&#39;interfaccia [!DNL Experience Platform] utente, lo switcher sandbox nell&#39;angolo superiore sinistro dello schermo consente di passare dalle sandbox disponibili a un menu a discesa. |
| `x-sandbox-name` header | Tutte le chiamate alle [!DNL Experience Platform] API ora devono includere la nuova `x-sandbox-name` intestazione, il cui valore fa riferimento all&#39; `name` attributo della sandbox in cui avrà luogo l&#39;operazione. |

Per ulteriori informazioni, consultate la panoramica sulle [sandbox](../../sandboxes/home.md).