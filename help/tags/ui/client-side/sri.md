---
title: Supporto di Subresource Integrity (SRI)
description: Scopri come Subresource Integrity (SRI) è supportato in Adobe Experience Platform.
exl-id: bd8bc3f7-9a85-44e2-ae07-f0664179b51c
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 96%

---

# Supporto di Subresource Integrity (SRI)

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

In questo documento viene illustrato il supporto di Subresource Integrity (SRI) in Adobe Experience Platform.

I siti web moderni sono realizzati facendo riferimento a immagini, contenuti e script provenienti da varie parti del web. SRI consente a un browser di verificare che i contenuti di un file richiesto non siano stati modificati in modo imprevisto.

Sebbene i relativi casi d’uso si completino a vicenda, l’SRI è diversa dai Criteri di sicurezza del contenuto (CSP), che garantiscono che solo i file provenienti da origini attendibili siano consentiti sul sito web. L’SRI compie un passo ulteriore e garantisce che il contenuto di questi file corrisponda alle aspettative.

>[!NOTE]
>
>Per informazioni più dettagliate sull’SRI, consulta i [documenti web MDN](https://developer.mozilla.org/it-IT/docs/Web/Security/Subresource_Integrity).

Il processo di convalida dell’SRI può essere riassunto come segue:

1. Viene generato un hash di crittografia della risorsa da convalidare.
1. Sul sito web, l’hash viene inserito nell’attributo `integrity` dell’elemento HTML che carica il file.
1. Quando il browser visualizza l’attributo `integrity`, richiede la risorsa e genera in modo indipendente la propria versione dell’hash di crittografia.
1. Il browser confronta l’hash `integrity` con quello generato. Se corrispondono, la risorsa viene consentita. Se non corrispondono, la risorsa viene bloccata.

## Limitazioni nei sistemi di gestione dei tag

In qualità di sistema di gestione dei tag (TMS), i tag in Adobe Experience Platform forniscono una build della libreria JavaScript compilata da caricare sulle pagine con un singolo elemento `<script>` (codice da incorporare). La funzionalità dinamica offerta dal TMS si ottiene sostituendo i contenuti di tale script in modo dinamico, senza che sia necessario apportare ulteriori modifiche.

Tuttavia, quando i contenuti dello script cambiano, cambia anche l’hash di crittografia dei contenuti. Pertanto, l’unico modo per far funzionare l’SRI con un TMS è aggiornare il codice di incorporamento nello stesso momento in cui si pubblica una nuova build. Per molti, questo è in contraddizione con lo scopo principale dell’utilizzo di un TMS.

L’alternativa migliore per la sicurezza dei tag consiste nell’implementare un criterio di sicurezza del contenuto (CSP, Content Security Policy). Per ulteriori informazioni, consulta la guida su [CSP e tag](./content-security-policy.md).

## Integrazione dell’SRI nella distribuzione di build

Se desideri utilizzare comunque l’SRI per le build delle librerie, dovrai utilizzare l’hosting autonomo. Se utilizzi un hosting gestito da Adobe, non puoi utilizzare l’SRI in mancanza di un periodo di tempo in cui i nuovi contenuti della build non corrispondono all’attributo `integrity` del codice di incorporamento.

L’automazione del processo di aggiornamento del codice di incorporamento varia a seconda della struttura del sito, ma i passaggi generali possono essere riassunti come segue:

1. Recupera la build della libreria di produzione tramite la distribuzione SFTP o scaricando l’archivio dall’interfaccia utente.
1. Genera l’hash di crittografia della build principale.
1. Verifica che l’attributo `integrity` del codice di incorporamento sia aggiornato al nuovo hash e che la build di riferimento sia aggiornata come parte della stessa distribuzione.

>[!IMPORTANT]
>
>Questo approccio coinvolge solo la build principale e non include eventuali file più piccoli.

## Passaggi successivi

In questo documento sono state trattate le limitazioni dell’utilizzo dell’SRI con i tag e i passaggi necessari per integrarla nelle distribuzioni di build delle librerie nonostante tali limitazioni. Se non lo hai già fatto, ti consigliamo vivamente di leggere la guida su [CSP e tag](./content-security-policy.md) per scoprire un’opzione di sicurezza alternativa.
