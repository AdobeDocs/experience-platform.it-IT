---
title: Configurazione dell'estensione
description: Scopri come configurare un’estensione tag per raccogliere le impostazioni globali da un utente nell’interfaccia di Data Collection di Adobe Experience Platform.
exl-id: 2bf33617-1398-499f-8325-3849dbdb1f97
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 93%

---

# Configurazione dell&#39;estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Con la configurazione dell’estensione si definisce il modo in cui un’estensione raccoglie le impostazioni globali da un utente. Ad esempio, considera un’estensione che consente all’utente di inviare un beacon tramite un’azione Invia beacon, e che tale beacon debba sempre contenere un ID account. Vogliamo evitare che agli utenti venga richiesto di immettere l’ID account ogni volta che devono configurare un’azione Invia beacon. L’estensione dovrà quindi richiedere l’ID account una sola volta, dalla vista di configurazione dell’estensione. Ogni volta che un beacon viene inviato, il modulo libreria dell’azione Invia beacon può richiamare l’ID account dalla configurazione dell’estensione e aggiungerlo al beacon.

Quando un utente installa un’estensione su una proprietà tag di Adobe Experience Platform, viene visualizzata la schermata per la configurazione dell’estensione fornita dall’estensione stessa. L’estensione potrà essere installata solo dopo che sarà stata configurata. Per informazioni su come creare una schermata per la configurazione delle estensioni, consulta il documento sulle [viste](./web/views.md).

Una volta salvate le impostazioni dalla vista di configurazione dell’estensione, queste verranno emesse nella libreria runtime di tag. Potrai quindi accedere a tali impostazioni dai moduli libreria delle estensioni richiamando [`turbine.getExtensionSettings()`](./turbine.md#get-extension-settings).

La configurazione dell’estensione è una funzione opzionale che puoi scegliere di non sfruttare.
