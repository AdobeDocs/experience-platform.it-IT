---
title: Supporto CDN Premium per i tag
description: Scopri la funzionalità premium CDN per i tag e come può essere utilizzata per distribuire i contenuti in più aree geografiche.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Supporto CDN Premium per tag (Beta)

>[!IMPORTANT]
>
>La funzione premium CDN per i tag è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. Questa documentazione è soggetta a modifiche.

Quando utilizzi un [Host gestito da Adobe](./hosts/managed-by-adobe-host.md) per distribuire le risorse dei tag Adobe Experience Platform sul sito web, queste risorse vengono distribuite tra le varie reti di distribuzione dei contenuti (CDN) in tutto il mondo, in modo da fornire la velocità di download più rapida. Tuttavia, alcune aree richiedono la replica e l’hosting di tutte le risorse del sito web su un server all’interno di tale area.

Per questo motivo, i tag in Experience Platform forniscono una funzionalità CDN premium che consente di distribuire contenuti a queste aree speciali.

Il supporto per la rete CDN Premium è una funzione a pagamento e deve essere acquistato dalla tua organizzazione per abilitarlo e utilizzarlo. Questa guida illustra come configurare e utilizzare questa funzione nell’interfaccia utente di raccolta dati dopo l’acquisto.

## Abilita la rete CDN premium per la tua organizzazione

La rete CDN Premium è abilitata a livello aziendale. Una volta che la tua organizzazione avrà acquistato la funzionalità CDN premium, un amministratore di Adobe abiliterà la tua azienda nell’interfaccia utente di raccolta dati.

## Ricrea e installa le librerie di tag con i codici di incorporamento aggiornati

Una volta abilitato il CDN premium, non significa che le risorse dei tag vengano immediatamente replicate e pronte all&#39;uso nelle nuove aree geografiche. Ciò significa solo che ora puoi scegliere quando accettare questa funzionalità.

>[!IMPORTANT]
>
>Le librerie create prima di abilitare la rete CDN Premium continueranno a funzionare esattamente come lo sono oggi. Questo vale anche per le librerie non gestite da Adobe, in quanto [ambienti archiviati](./environments.md#archive) utilizza solo URL relativi per i percorsi delle risorse. Dopo aver abilitato la CDN premium, qualsiasi libreria creata che non è gestita da Adobe si comporterà come se la funzionalità CDN Premium non fosse abilitata.

Dopo aver abilitato la rete CDN premium e aver ricostruito tutte le librerie che desideri utilizzare dalle nuove aree di hosting, puoi recuperare i nuovi codici di incorporamento della regione di hosting da aggiungere ai tuoi siti web.

>[!NOTE]
>
>Il codice di incorporamento della libreria elencato in [!UICONTROL Standard] l&#39;area di hosting continuerà a funzionare così com&#39;è, così come tutti i codici di incorporamento Page Top o Page Bottom già sui tuoi siti web.

Visita il **[!UICONTROL Ambienti]** per trovare i nuovi codici di incorporamento, vai alla pagina o visualizza le istruzioni di installazione dell&#39;ambiente dalla schermata di modifica della libreria . Ogni nuova area di hosting supportata viene visualizzata dopo [!UICONTROL Standard] area di hosting (utilizzata per le aree del mondo supportate senza CDN premium). La schermata seguente mostra un codice di incorporamento per la regione Cina, che utilizza `.cn` come dominio di primo livello (TLD).

![Codice di incorporamento per l’area della Cina](../../images/ui/publishing/premium-cdn/embed-codes.png)

Scegli il codice di incorporamento appropriato per la pagina web e incollalo all’interno della `<head>` tag del documento. Per ulteriori informazioni sull’utilizzo dei codici di incorporamento per installare le librerie di tag, consulta [guida all’interfaccia utente per ambienti](./environments.md#installation).

## Passaggi successivi

Questa guida illustra come abilitare e installare la funzionalità CDN premium per l’implementazione dei tag. Per ulteriori informazioni sull’installazione e il test delle librerie di tag sulle proprietà web e mobili, consulta [panoramica sulla pubblicazione](./overview.md).
