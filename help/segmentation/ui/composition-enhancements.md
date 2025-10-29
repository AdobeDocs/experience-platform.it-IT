---
title: Miglioramenti alla composizione del pubblico
description: Scopri i miglioramenti apportati alla composizione del pubblico con un arricchimento del pubblico e un’attivazione più rapida.
hide: true
hidefromtoc: true
source-git-commit: 42e639b403edbaf666d8bc21eb35b2b75530d6b0
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Miglioramenti alla composizione del pubblico

Ora hai accesso a **due** miglioramenti per la composizione del pubblico:

- [Arricchimento del pubblico](#audience-enrichment)
- [Attivazione più rapida](#faster-activation)

## Arricchimento del pubblico {#audience-enrichment}

L’arricchimento del pubblico consente di generare una matrice di valori che consentono ai profili di qualificarsi per il pubblico creato.

Per aggiungere un arricchimento del pubblico alla composizione, seleziona il blocco **[!UICONTROL Audience]** più in alto nell&#39;area di lavoro. Dopo aver assegnato un nome al pubblico, seleziona **[!UICONTROL Build rule]** per aprire l&#39;area di lavoro del generatore di regole.

![Il blocco del pubblico è evidenziato, così come il pulsante Genera regola.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

Viene visualizzata l’area di lavoro del generatore di regole. Ora puoi creare un criterio di filtro per l’arricchimento del pubblico. I criteri di filtro **devono** includere un attributo all&#39;interno di un array. L’attributo array dipende dalla struttura dello schema della tua organizzazione. Dopo aver creato i criteri di filtro, seleziona **[!UICONTROL Delivery]** nel pannello di destra.

![L&#39;area di lavoro del generatore di regole mostra un esempio di un pubblico che può essere arricchito. Viene evidenziato anche il pulsante Delivery.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

Scegliete l&#39;array di oggetti da utilizzare per l&#39;arricchimento dall&#39;elenco nel pannello sinistro. Se nel profilo è presente un solo array, l’array viene selezionato automaticamente. Seleziona **[!UICONTROL Save]** per tornare alla composizione del pubblico.

<!-- , as well as the fields you want to be used in the enrichment. -->

![Viene visualizzata la struttura dello schema per la struttura di arricchimento.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

Nella composizione del pubblico, il blocco [!UICONTROL Audience] è ora di tipo &quot;[!UICONTROL Rule builder with enhancement]&quot;. Seleziona **[!UICONTROL Publish]** per attivare il pubblico con il successivo batch giornaliero.

![Il blocco del pubblico è evidenziato e indica che è stato aggiunto un pubblico con arricchimento.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### Dettagli del comportamento e guardrail

Tieni presenti i dettagli e i guardrail seguenti quando utilizzi l’arricchimento del pubblico:

- Puoi utilizzare l’arricchimento del pubblico solo nei tipi di pubblico creati in Composizione pubblico
- Il primo blocco utilizzato nella composizione **deve** essere un pubblico basato su regole.
- **impossibile** utilizzare altre operazioni all&#39;interno della composizione.
- Dopo la pubblicazione, **non puoi** modificare la composizione sul pubblico basato su regole.

   - È *possibile* copiare la composizione in una bozza e modificare la bozza se si desidera apportare modifiche alla composizione di base o al pubblico basato su regole.

- È possibile utilizzare solo **un** array di oggetti per generare il payload di arricchimento all&#39;interno di un singolo pubblico

   - L&#39;array di payload può essere nidificato all&#39;interno di un oggetto (fino a sette livelli nello schema del profilo), ma **non può essere** contenuto in un altro array.
   - L&#39;array di payload **deve** avere un massimo di 50 righe.
   - Tutti gli output di colonne all&#39;interno del payload **devono** essere di tipo primitivo.
   - Viene eseguito l&#39;output solo delle prime **venti** colonne dell&#39;array.

- Al momento sono disponibili solo **dieci** composizioni di pubblico

## Attivazione più rapida {#faster-activation}

L’attivazione più rapida consente di attivare il pubblico in una destinazione a valle subito dopo la valutazione della composizione. Di conseguenza, se la destinazione è impostata per l’attivazione dopo la valutazione del segmento, non è più necessario attendere 24 ore il completamento del processo di valutazione.

Per ulteriori informazioni, consulta la guida [attivare tipi di pubblico per le destinazioni dei profili batch](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files).
