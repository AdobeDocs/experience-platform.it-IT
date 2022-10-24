---
keywords: identità rtcdp;identità rtcdp;identità cdp in tempo reale
title: Identità in Real-time Customer Data Platform
description: Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore dei clienti e del loro comportamento combinando le identità tra dispositivi e sistemi.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Panoramica sulle identità

Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una visione migliore dei tuoi clienti e del loro comportamento collegando le identità tra i vari dispositivi e sistemi. In genere, i clienti interagiscono con il tuo marchio su più canali, tra cui la navigazione sul sito web online, l&#39;acquisto in negozio, l&#39;iscrizione al programma fedeltà o la chiamata di un help desk per il supporto, per citarne alcuni. In questi diversi sistemi, esiste un&#39;identità creata per quel cliente e [!DNL Identity Service] rende possibile unire queste identità per vedere il quadro completo.

Ora, invece di cinque clienti separati che interagiscono con il tuo marchio su cinque canali diversi, puoi vedere che si tratta dello stesso cliente e assicurarti che riceva un’esperienza coerente, personalizzata e pertinente attraverso ogni interazione. Man mano che si conoscono ulteriori informazioni sul cliente (ad esempio, un browser anonimo del sito web decide di registrarsi per un account e di effettuare l&#39;accesso), le informazioni vengono unite e l&#39;immagine del cliente diventa sempre più chiara.

## Namespace Identity

Gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] e fungono da indicatori che forniscono contesto aggiuntivo alle identità dei clienti. Un esempio di spazio dei nomi ID comunemente utilizzato è &quot;E-mail&quot;, dove l’utilizzo dello stesso indirizzo e-mail in più siti web consente di unire diverse identità diverse, ciascuna con un ID cliente univoco, in quanto di fatto appartenente allo stesso cliente. [!DNL Experience Platform] consente di utilizzare i namespace ID per cercare singoli profili all’interno dell’interfaccia utente. Per ulteriori informazioni sulla visualizzazione dei profili, consulta la sezione [panoramica della navigazione del profilo](profile-browse.md). Per ulteriori informazioni sugli spazi dei nomi delle identità, consulta [panoramica dello spazio dei nomi identità](../../identity-service/namespaces.md).

## Grafici di identità

Un grafico di identità è una mappa delle relazioni tra diversi namespace di identità, che fornisce una rappresentazione visiva del modo in cui il cliente interagisce con il tuo marchio attraverso diversi canali. Tutti i grafici di identità dei clienti sono gestiti e aggiornati collettivamente da [!DNL Identity Service] in tempo quasi reale, in risposta all&#39;attività del cliente.

[!DNL Identity Service] gestisce un grafico delle identità visibile solo dalla tua organizzazione e generato in base ai tuoi dati, denominato grafico privato. [!DNL Identity Service] potenzia il grafico privato quando un record di dati acquisito contiene più di un’identità, aggiungendo una relazione tra le identità trovate.

## Passaggi successivi

Le identità e le relazioni tra di esse sono definite e mantenute da [!DNL Identity Service] e sfruttato da [!DNL Real-time Customer Profile] creare un quadro completo delle interazioni di ogni singolo cliente. Per ulteriori informazioni, visita la [Documentazione del servizio Identity](../../identity-service/home.md).
