---
keywords: Experience Platform;guida introduttiva;ia attribuzione;argomenti popolari;input ia attribuzione;output ia attribuzione;risoluzione dei problemi ia attribuzione;errori ia attribuzione
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: Risoluzione dei problemi di errore di Attribution AI
description: Trova le risposte agli errori più comuni in Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Risoluzione dei problemi di errore di Attribution AI

Questo documento fornisce le risposte alle domande più frequenti su Attribution AI.

## Impossibile accedere alle Attribution AI in incognito Chrome

Gli errori di caricamento in modalità incognito di Google Chrome sono presenti a causa di aggiornamenti nelle impostazioni di protezione in modalità incognito di Google Chrome. Il problema è stato affrontato attivamente con Chrome per rendere experience.adobe.com un dominio affidabile.

![Immagine di errore](./images/faq/error.PNG){width=500}

### Correzione consigliata

Per risolvere questo problema è necessario aggiungere experience.adobe.com come sito che può sempre utilizzare i cookie. Per iniziare, passa a **chrome://settings/cookies**. Quindi, scorri verso il basso fino alla sezione **Comportamenti personalizzati**, quindi seleziona il pulsante **Aggiungi** accanto a &quot;Siti che possono sempre utilizzare i cookie&quot;. Nel popover visualizzato, copia e incolla `[*.]experience.adobe.com`, quindi seleziona la casella di controllo **Includi cookie di terze parti** su questo sito. Al termine, seleziona **Aggiungi** e ricarica l&#39;Attribution AI in incognito.

![correzione consigliata](./images/faq/cookies2.gif)
