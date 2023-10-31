---
solution: Experience Platform
title: Risolvere i problemi relativi ai playbook
description: Scopri i problemi comuni relativi ai playbook e come risolverli
badgeBeta: label="Beta" type="Informative"
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 100%

---

# Risoluzione dei problemi e limitazioni note (Beta)

>[!AVAILABILITY]
>
>Questa funzionalità è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per la versione beta di [!UICONTROL Playbook di casi d’uso], tieni presente i suggerimenti per la risoluzione dei problemi e delle limitazioni note.

## Limitazioni note {#known-limitations}

Quando crei una nuova istanza di un playbook, vengono generate nuove risorse. Per gli schemi generati, tuttavia, se uno schema viene generato in un’istanza di un playbook e lo si modifica, se si abilita un’altra istanza del playbook, *non* viene generato un altro schema. Invece, continuerai a utilizzare lo schema modificato anche all’interno della nuova istanza.
