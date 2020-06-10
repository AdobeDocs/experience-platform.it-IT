---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note sulla versione della piattaforma Experience - 10 agosto 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 7f9d1120ac323c60f899cb1cf855e55db20437ed
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 7%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 10 giugno 2020**

Nuove funzioni in Adobe Experience Platform:

- [Controllo di accesso](#access-control)
- [Sandbox](#sandboxes)

## Controllo di accesso {#access-control}

Experience Platform sfrutta i profili di prodotto di [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l&#39;accesso a diverse funzionalità della piattaforma, tra cui la modellazione dei dati, la gestione dei profili e l&#39;amministrazione della sandbox.

**Funzionalità chiave**

| Funzione | Descrizione |
|--- | ---|
| Autorizzazioni | In Admin Console, la scheda _Autorizzazioni_ all&#39;interno di un profilo di prodotto Piattaforma consente di personalizzare le funzionalità della piattaforma disponibili per gli utenti collegati a tale profilo. Le categorie di autorizzazioni disponibili includono: Modellazione dei dati, gestione dei dati, gestione dei profili, identità, monitoraggio dei dati, amministrazione sandbox, destinazioni, origini. |
| Accesso alle sandbox | La scheda _Autorizzazioni_ all&#39;interno di un profilo di prodotto Piattaforma può consentire agli utenti l&#39;accesso a sandbox specifiche. Per ulteriori informazioni, consultate la sezione sulle [sandbox](#sandboxes) di seguito. |

Per ulteriori informazioni, consulta la panoramica [sul controllo](../../access-control/home.md)degli accessi.

## Sandbox {#sandboxes}

Experience Platform è stata progettata per arricchire le applicazioni per esperienze digitali su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e all&#39;implementazione di tali applicazioni, garantendo al contempo la conformità operativa. Per rispondere a questa esigenza, Experience Platform fornisce sandbox che dividono una singola istanza della piattaforma in ambienti virtuali separati per aiutare a sviluppare e sviluppare applicazioni per esperienze digitali.

**Funzionalità chiave**

| Funzione | Descrizione |
|--- | ---|
| Sandbox produzione | Experience Platform fornisce un unico sandbox di produzione, che non può essere eliminato o reimpostato. |
| Sandbox non di produzione | È possibile creare più sandbox non di produzione per una singola istanza della piattaforma, per testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sul sandbox di produzione. |
| Switcher sandbox | Nell’interfaccia utente di Experience Platform, lo switcher sandbox nell’angolo in alto a sinistra dello schermo consente di passare dalle sandbox disponibili tramite un menu a discesa. |
| `x-sandbox-name` header | Tutte le chiamate alle API di Experience Platform ora devono includere la nuova `x-sandbox-name` intestazione, il cui valore fa riferimento all&#39; `name` attributo della sandbox in cui avrà luogo l&#39;operazione. |

Per ulteriori informazioni, consultate la panoramica sulle [sandbox](../../sandboxes/home.md).