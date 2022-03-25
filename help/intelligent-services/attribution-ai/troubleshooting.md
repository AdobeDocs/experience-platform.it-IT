---
keywords: Experience Platform;guida introduttiva;ai di attribuzione;argomenti comuni;input di ai di attribuzione;output di ai di attribuzione;risoluzione dei problemi di attribuzione;errori di ai di attribuzione
solution: Intelligent Services, Real-time Customer Data Platform
feature: Attribution AI
title: Risoluzione dei problemi relativi agli errori di Attribution AI
description: Trova le risposte agli errori comuni nelle Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Risoluzione dei problemi relativi agli errori di Attribution AI

Questo documento fornisce le risposte alle domande più frequenti sulle Attribution AI.

## Impossibile accedere a Attribution AI in Chrome in incognito

Gli errori di caricamento nella modalità in incognito di Google Chrome sono presenti a causa degli aggiornamenti nelle impostazioni di sicurezza in modalità in incognito di Google Chrome. Il problema è in fase di elaborazione con Chrome per rendere experience.adobe.com un dominio fidato.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correzione consigliata

Per risolvere questo problema è necessario aggiungere experience.adobe.com come sito che può sempre utilizzare i cookie. Inizia passando a **chrome://settings/cookies**. Quindi, scorri verso il basso fino a **Comportamenti personalizzati** seguita dalla selezione della **Aggiungi** accanto a &quot;siti che possono sempre utilizzare i cookie&quot;. Nel pover che appare, copia e incolla `[*.]experience.adobe.com` quindi seleziona la **Inclusione di cookie di terze parti** in questa casella di controllo del sito. Al termine, seleziona **Aggiungi** e ricaricare le Attribution AI in incognito.

![correzione consigliata](./images/faq/cookies2.gif)
