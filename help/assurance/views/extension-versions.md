---
title: Visualizzazione versioni estensioni
description: Questa guida contiene informazioni dettagliate sulla vista Versioni estensioni in Adobe Experience Platform Assurance.
exl-id: a3a649da-1ef1-45a3-a1ed-6a7bc16c2987
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Visualizzazione delle versioni delle estensioni

La vista Versione estensioni consente di ordinare e visualizzare rapidamente quali estensioni Adobe Experience Platform per dispositivi mobili sono state installate e se sono aggiornate in un client connesso a una sessione Assurance.

## Introduzione alle visualizzazioni delle versioni delle estensioni

Dopo [impostazione di Assurance](../tutorials/implement-assurance.md), nella **Home** visualizza, seleziona **[!UICONTROL Versioni dell&#39;estensione]**

![Versioni dell&#39;estensione](./images/versions/versions-extension.png)

## Verifica se la versione è aggiornata

All&#39;interno di questa vista, una tabella mostra sia la versione più recente di ogni SDK mobile, sia la versione corrente installata, se applicabile. Quando una versione è sincronizzata con la versione più recente, la versione installata presenterà un badge verde. In caso contrario, il badge verrà visualizzato in rosso.

![Confronto delle versioni delle estensioni](./images/versions/versions-extension-version.png)

## Esporta versioni

In alto a destra nella vista puoi selezionare **[!UICONTROL Esporta versioni]** che ti fornisce un payload JSON con tutte le informazioni sulle estensioni e sulla piattaforma utilizzata dal client. Puoi scegliere di esportare questi dati in un file JSON o copiarli negli Appunti.

![Esportazione delle versioni delle estensioni](./images/versions/versions-extension-export.png)
