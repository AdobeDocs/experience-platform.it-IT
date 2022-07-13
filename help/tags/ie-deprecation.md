---
title: Terminazione del supporto per i tag in Internet Explorer 10 e 11
description: Adobe Experience Platform non fornisce più il supporto per l'aggiornamento dei tag in Internet Explorer 10 e 11.
source-git-commit: 0103f1af37dc202087d3c81d495de88d3de7c377
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Fine del supporto dei tag in Internet Explorer 10 e 11

Man mano che il panorama dell’esperienza digitale online continua a evolversi, Adobe non investe più risorse per supportare Internet Explorer 10 (IE10) e Internet Explorer 11 (IE11) per i tag in Adobe Experience Platform. Sebbene Adobe non stia rimuovendo attivamente il supporto per IE10 e IE11, l&#39;impatto di questi browser sulle nuove funzionalità non sarà più considerato negli aggiornamenti futuri.

## Perché IE10 e IE11 non sono più supportati?

Ci sono quattro motivi per cui i tag non supportano più IE10 e IE11:

* **Microsoft cessa il supporto di IE10 e IE11**: A partire da gennaio 2020, [Microsoft ha smesso di supportare IE10](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-10-end-of-support) per aggiornamenti di sicurezza e non di sicurezza. A partire da giugno 2022, [Microsoft ha smesso di supportare IE11](https://docs.microsoft.com/en-us/lifecycle/announcements/internet-explorer-11-end-of-support) su alcune versioni di Windows.
* **Il settore in espansione sta cessando il supporto di IE10 e IE11**: Poiché il settore più ampio riduce il supporto per IE10 e IE11, la capacità dei tag di mantenere la compatibilità con queste tecnologie diventa sempre più ostacolata.
* **Le tecnologie moderne non supportano IE10 e IE11**: Affinché i tag continuino a supportare le tecnologie più moderne, deve terminare il supporto per IE10 e IE11 perché queste tecnologie moderne non sono compatibili con questi browser web.
* **Il supporto di IE10 e IE11 rallenta lo sviluppo delle funzioni generali**: Molte nuove funzioni rilasciate per i tag richiedono un&#39;attenta considerazione di IE10 e IE11. Questa considerazione si traduce in ore di lavoro aggiuntivo per acquisire strumenti di test difficili da trovare che funzionano con IE10 e IE11, aggiungere codice aggiuntivo per far funzionare le funzionalità con IE10 e IE11 che non hanno supporto nativo, e ricerca per assicurarsi che la funzione funzioni funzioni come previsto. Interrompendo il supporto per IE10 e IE11, Adobe può fornire nuove funzionalità più velocemente.

## Effetti della deprecazione di IE10 e IE11

Dopo che il supporto è stato dichiarato obsoleto, si verificheranno i seguenti effetti:

* Le nuove funzionalità potrebbero non supportare IE10 e IE11.
* Il test per il supporto di nuove funzioni e correnti utilizzando IE10 e IE11 cesserà.
* Funzioni che una volta supportate IE10 e IE11 potrebbero non supportare più questi browser.
