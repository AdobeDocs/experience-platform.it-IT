---
keywords: Experience Platform;guida introduttiva;ia attribuzione;argomenti popolari;input ia attribuzione;output ia attribuzione;risoluzione dei problemi ia attribuzione;errori ia attribuzione
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Risoluzione dei problemi di errore di Attribution AI
description: Trova le risposte agli errori più comuni in Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Risoluzione dei problemi di errore di Attribution AI

Questo documento fornisce le risposte alle domande più frequenti su Attribution AI.

## Impossibile accedere alle Attribution AI in incognito Chrome

Gli errori di caricamento nella modalità in incognito di Google Chrome sono presenti a causa di aggiornamenti nelle impostazioni di sicurezza della modalità in incognito di Google Chrome. Il problema è attivamente in fase di elaborazione con Chrome per rendere experience.adobe.com un dominio fidato.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correzione consigliata

Per risolvere questo problema è necessario aggiungere experience.adobe.com come sito che può sempre utilizzare i cookie. Per iniziare, passa a **chrome://settings/cookies**. Quindi, scorri verso il basso fino a **Comportamenti personalizzati** seguito dalla selezione della sezione **Aggiungi** accanto a &quot;siti che possono sempre utilizzare i cookie&quot;. Nel popover visualizzato, copiare e incollare `[*.]experience.adobe.com` quindi seleziona la **Inclusione di cookie di terze parti** in questo sito. Al termine, seleziona **Aggiungi** e ricaricare le Attribution AI in incognito.

![correzione consigliata](./images/faq/cookies2.gif)
