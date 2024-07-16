---
solution: Experience Platform
title: Limitazioni note e risoluzione dei problemi relativi ai playbook
description: Scopri di più sui problemi noti e i problemi comuni dei playbook e come risolverli
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Risoluzione dei problemi {#troubleshooting}

Visualizza suggerimenti per la risoluzione dei problemi relativi a errori comuni durante l’utilizzo dei playbook basati su casi d’uso

## Adobe Journey Optimizer Surfaces non configurato {#surfaces-not-configured}

Durante la creazione di un&#39;istanza di un playbook, è possibile che venga visualizzato il messaggio seguente.

![Risoluzione dei problemi](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Questo perché i playbook Journey Optimizer creano messaggi per i canali e-mail, push e SMS. Per configurare le diverse superfici, leggere la guida [guida introduttiva](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer).

## Stato *non riuscito* durante la creazione di una nuova istanza {#status-failed}

Se durante il tentativo di creazione di un&#39;istanza viene visualizzato un messaggio di errore, è possibile che l&#39;amministratore non abbia concesso le autorizzazioni utente necessarie. Un playbook contiene molte risorse diverse e l’utente ha bisogno delle autorizzazioni per crearle per poter creare correttamente l’istanza del playbook. Consulta la sezione [autorizzazioni](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) di questa guida sulla configurazione delle autorizzazioni.

## Errore di importazione {#import-failure}

I clienti operano all’interno di ambienti di test diversi e, occasionalmente, durante l’importazione di un’istanza dal proprio ambiente alla sandbox di Adobe, potrebbe non riuscire. Per visualizzare lo stato di queste importazioni, seleziona Sandbox dal menu di navigazione a sinistra, quindi seleziona Processi. Qui puoi visualizzare tutti i dettagli dei file importati. Selezionare un file con uno stato di errore, quindi scegliere Visualizza dettagli processo. Viene visualizzata una finestra modale. Seleziona Visualizza file JSON, scorri verso il basso e copia il messaggio di errore visualizzato in &quot;messages&quot;. È possibile che vengano visualizzati più messaggi di errore, quindi assicurati di copiarli tutti. Invia questi al tuo team di Adobi durante il tentativo di registrare un ticket bug. In questo modo il processo di risoluzione dei problemi viene accelerato e il team può disporre di un contesto più completo.
