---
title: Configurazione dell'estensione
description: Scopri come configurare un’estensione tag per raccogliere le impostazioni globali da un utente nell’interfaccia utente di raccolta dati di Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 70%

---

# Configurazione dell&#39;estensione

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Con la configurazione dell’estensione si definisce il modo in cui un’estensione raccoglie le impostazioni globali da un utente. Ad esempio, considera un’estensione che consente all’utente di inviare un beacon tramite un’azione Invia beacon, e che tale beacon debba sempre contenere un ID account. Vogliamo evitare che agli utenti venga richiesto di immettere l’ID account ogni volta che devono configurare un’azione Invia beacon. L’estensione dovrà quindi richiedere l’ID account una sola volta, dalla vista di configurazione dell’estensione. Ogni volta che un beacon viene inviato, il modulo libreria dell’azione Invia beacon può richiamare l’ID account dalla configurazione dell’estensione e aggiungerlo al beacon.

Quando gli utenti installano un&#39;estensione a una proprietà tag in Adobe Experience Platform, viene mostrata loro la vista di configurazione dell&#39;estensione che l&#39;estensione fornirà. L’estensione potrà essere installata solo dopo che sarà stata configurata. Per informazioni su come creare una schermata per la configurazione delle estensioni, consulta il documento sulle [viste](./web/views.md).

Una volta salvate le impostazioni da una vista di configurazione dell&#39;estensione, queste verranno emesse nella libreria di runtime di tag. Potrai quindi accedere a tali impostazioni dai moduli libreria delle estensioni richiamando [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configurazione dell’estensione è una funzione opzionale che puoi scegliere di non sfruttare.
