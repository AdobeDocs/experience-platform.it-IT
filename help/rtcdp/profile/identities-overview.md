---
keywords: identità rtcdp;identità rtcdp;identità cdp in tempo reale
title: Identità in Real-time Customer Data Platform
description: Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e del loro comportamento combinando le identità tra dispositivi e sistemi.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 5611a5abc7d1ed7781108b6f263e7550092b715d
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Panoramica sulle identità

Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una visione migliore dei tuoi clienti e del loro comportamento collegando le identità tra i vari dispositivi e sistemi. In genere, i clienti interagiscono con il tuo marchio su più canali, tra cui la navigazione sul sito web online, l&#39;acquisto in negozio, l&#39;iscrizione al programma fedeltà o la chiamata di un help desk per il supporto, per citarne alcuni. Su questi diversi sistemi, esiste un&#39;identità creata per quel cliente e [!DNL Identity Service] consente di unire queste identità per vedere il quadro completo.

Ora, invece di cinque clienti separati che interagiscono con il tuo marchio su cinque canali diversi, puoi vedere che si tratta dello stesso cliente e assicurarti che riceva un’esperienza coerente, personalizzata e pertinente attraverso ogni interazione. Man mano che si conoscono ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito web decide di registrarsi per un account e di effettuare l&#39;accesso), le informazioni vengono unite e l&#39;immagine del cliente diventa sempre più chiara.

## Namespace Identity

Gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] e fungono da indicatori che forniscono contesto aggiuntivo alle identità dei clienti. Un esempio di spazio dei nomi ID comunemente utilizzato è &quot;E-mail&quot;, dove l’utilizzo dello stesso indirizzo e-mail in più siti web consente di unire diverse identità diverse, ciascuna con un ID cliente univoco, in quanto di fatto appartenente allo stesso cliente. [!DNL Experience Platform] consente di utilizzare i namespace ID per cercare singoli profili all’interno dell’interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consulta la [panoramica del profilo](profile-browse.md). Per ulteriori informazioni sugli spazi dei nomi di identità, consulta la [panoramica dello spazio dei nomi di identità](../../identity-service/namespaces.md).

## Grafici di identità

Un grafico di identità è una mappa delle relazioni tra diversi namespace di identità, che fornisce una rappresentazione visiva del modo in cui il cliente interagisce con il tuo marchio attraverso diversi canali. Tutti i grafici di identità dei clienti vengono gestiti e aggiornati collettivamente da [!DNL Identity Service] in tempo quasi reale, in risposta all&#39;attività dei clienti.

[!DNL Identity Service] gestisce un grafico delle identità visibile solo dalla tua organizzazione e generato in base ai tuoi dati, denominato grafico privato. [!DNL Identity Service] potenzia il grafico privato quando un record di dati acquisito contiene più di un’identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse sono definite e gestite da [!DNL Identity Service] e sfruttate da [!DNL Real-time Customer Profile] per creare un quadro completo delle singole interazioni dei clienti. Per ulteriori informazioni, visita la [documentazione del servizio Identity](../../identity-service/home.md).
