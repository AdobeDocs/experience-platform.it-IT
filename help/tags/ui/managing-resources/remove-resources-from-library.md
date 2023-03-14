---
title: Rimuovere risorse da una libreria
description: Scopri come rimuovere le risorse da una libreria di tag.
exl-id: ad1dd093-962c-4f6d-85eb-c5ed1b644927
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 94%

---

# Rimuovere risorse da una libreria

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Quando non desideri più che una risorsa abbia effetto all&#39;interno di una build è necessario rimuoverla dalla libreria che la contiene e creare una nuova build.

>[!IMPORTANT]
>
>Le risorse nelle librerie sono interdipendenti. La rimozione di una risorsa da una build può modificare il comportamento di altre risorse all&#39;interno di questa.

Il processo di rimozione funziona in modo leggermente diverso a seconda dello stato in cui si trova la libreria.

## Librerie di Sviluppo

Le risorse all&#39;interno delle librerie di Sviluppo possono essere modificate direttamente.

1. Apri la libreria.
1. Rimuovi la risorsa.
1. Salva la libreria.
1. Crea la libreria.

## Librerie Inviate e Approvate

Le risorse all&#39;interno delle librerie Inviate o Approvate non possono essere modificate direttamente. È necessario riportare la libreria sullo stato di Sviluppo.

1. Rifiuta la libreria (riporta la libreria in Sviluppo).
1. Segui i passaggi descritti in precedenza in &quot;librerie di Sviluppo&quot; per rimuovere le risorse dalle librerie di Sviluppo.

## Librerie di Produzione

La rimozione di risorse da una libreria di Produzione è il caso più complesso. Non è possibile manipolare le risorse della libreria in questo stato e non è possibile riportarle allo stato di Sviluppo.

È necessario invece disabilitare la risorsa. Questa disattivazione è una modifica che aggiungi a una libreria di Sviluppo come qualsiasi altra modifica. Una volta che questa modifica è stata inserita in Produzione, la risorsa viene spostata dalla tua libreria di Produzione.

1. Disattiva la risorsa.
   1. Seleziona la risorsa nella vista elenco.
   1. Seleziona **[!UICONTROL Disabilita]**.
1. Crea una nuova libreria di Sviluppo.
1. Aggiungi la versione `latest` della risorsa disabilitata.
1. Salva e Genera.
1. Segui il processo classico per la promozione delle librerie in Produzione.
1. Per rimuovere la risorsa, pubblica su Produzione.
