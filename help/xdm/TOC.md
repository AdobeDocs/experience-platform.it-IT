---
audience: user
user-guide-title: Guida del sistema Experience Data Model (XDM)
breadcrumb-title: Guida di Experience Data Model (XDM)
user-guide-description: Utilizza i gruppi di campi per classi e schemi di Experience Data Model (XDM) per standardizzare i dati dell’esperienza.
feature: Schemas
source-git-commit: e476574e35ea18a50749009ffd1b4182941cc496
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 15%

---


# Sistema Experience Data Model (XDM) {#xdm}

* [Panoramica del sistema XDM](home.md)
* Schemi {#schema}
   * [Nozioni di base sulla composizione dello schema](schema/composition.md)
   * [Best practice per la modellazione dei dati](schema/best-practices.md)
   * [Dati sensibili e personali](./schema/sensitive-and-personal-data.md)
   * [Vincoli del tipo di campo XDM](schema/field-constraints.md)
   * [Spaziatura dei nomi in XDM](./schema/namespaces.md)
   * Modelli di dati di settore {#industries}
      * [Panoramica](./schema/industries/overview.md)
      * [Vendita al dettaglio](./schema/industries/retail.md)
      * [Servizi finanziari](./schema/industries/financial.md)
      * [Medicale](./schema/industries/healthcare.md)
      * [Telecomunicazioni](./schema/industries/telecom.md)
      * [Viaggi e ospitalità](./schema/industries/travel-hospitality.md)
   * [Dizionario dei campi XDM](schema/field-dictionary.md)
* Classi {#classes}
   * [Profilo individuale XDM](./classes/individual-profile.md)
   * [ExperienceEvent XDM](./classes/experienceevent.md)
   * [Medicina](./classes/medication.md)
   * [Pagatore](./classes/payer.md)
   * [Pianificare](./classes/plan.md)
   * [Criterio](./classes/policy.md)
   * [Prodotto](./classes/product.md)
   * [Provider](./classes/provider.md)
   * [Definizione del segmento](./classes/segment-definition.md)
   * Classi B2B {#b2b}
      * [Account aziendale XDM](./classes/b2b/business-account.md)
      * [Relazione personale account aziendale XDM](./classes/b2b/business-account-person-relation.md)
      * [Campagna aziendale XDM](./classes/b2b/business-campaign.md)
      * [Membri di una campagna aziendale XDM](./classes/b2b/business-campaign-members.md)
      * [Opportunità aziendali XDM](./classes/b2b/business-opportunity.md)
      * [Relazione personale opportunità di business XDM](./classes/b2b/business-opportunity-person-relation.md)
      * [Elenco di marketing aziendale XDM](./classes/b2b/business-marketing-list.md)
      * [Membri elenco marketing commerciale XDM](./classes/b2b/business-marketing-list-members.md)
* Gruppi di campi {#field-groups}
   * Profilo individuale XDM {#profile}
      * [Consensi e preferenze](./field-groups/profile/consents.md)
      * [Dettagli demografici](./field-groups/profile/demographic-details.md)
      * [Consenso IAB TCF 2.0](./field-groups/profile/iab.md)
      * [IdentityMap](./field-groups/profile/identitymap.md)
      * [Dettagli dei membri del settore sanitario](./field-groups/profile/healthcare-member-details.md)
      * [Dettagli fedeltà](./field-groups/profile/loyalty-details.md)
      * [Dati di contatto personali](./field-groups/profile/personal-contact-details.md)
      * [Dettagli di appartenenza al segmento](./field-groups/profile/segmentation.md)
      * [Abbonamento a domicilio](./field-groups/profile/telecom-subscription.md)
      * [Dettagli contatto lavoro](./field-groups/profile/work-contact-details.md)
      * [Componenti per Business Person XDM](./field-groups/profile/business-person-components.md)
      * [Dettagli sulle persone aziendali XDM](./field-groups/profile/business-person-details.md)
   * ExperienceEvent XDM {#event}
      * [Estensione completa Adobe Analytics](./field-groups/event/analytics-full-extension.md)
      * [Dettagli sulla pubblicità](./field-groups/event/advertising-details.md)
      * [Dettagli applicazione](./field-groups/event/application-details.md)
      * [Trasferimenti di saldo](./field-groups/event/balance-transfers.md)
      * [Dettagli di marketing per le campagne](./field-groups/event/campaign-marketing-details.md)
      * [Azioni a schede](./field-groups/event/card-actions.md)
      * [Dettagli canale](./field-groups/event/channel-details.md)
      * [Dettagli Commerce](./field-groups/event/commerce-details.md)
      * [Dettagli sui depositi](./field-groups/event/deposit-details.md)
      * [Dettagli sul trasferimento dei dispositivi](./field-groups/event/device-trade-in-details.md)
      * [Prenotazione pranzo](./field-groups/event/dining-reservation.md)
      * [Dettagli ID utente finale](./field-groups/event/enduserids.md)
      * [Dettagli dell&#39;ambiente](./field-groups/event/environment-details.md)
      * [Riserva di volo](./field-groups/event/flight-reservation.md)
      * [Consenso IAB TCF 2.0](./field-groups/event/iab.md)
      * [Riserva](./field-groups/event/lodging-reservation.md)
      * [Dettagli richiesta preventivo](./field-groups/event/quote-request-details.md)
      * [Dettagli prenotazione](./field-groups/event/reservation-details.md)
      * [Dettagli Sitetool](./field-groups/event/sitetool-details.md)
      * [Ricerca nel sito di supporto](./field-groups/event/support-site-search.md)
      * [Dettagli aggiornamento](./field-groups/event/upgrade-details.md)
      * [Dettagli di upselling](./field-groups/event/upsell-details.md)
      * [Dettagli Web](./field-groups/event/web-details.md)
   * Campagna aziendale XDM {#b2b-campaign}
      * [Dettagli della campagna aziendale XDM](./field-groups/b2b-campaign/details.md)
   * Membri di una campagna aziendale XDM {#b2b-campaign-members}
      * [Dettagli dei membri della campagna aziendale XDM](./field-groups/b2b-campaign-members/details.md)
   * Medicina {#medication}
      * [Medicina sanitaria](./field-groups/medication/healthcare-medication.md)
   * Pianificare {#plan}
      * [Dettagli sul piano sanitario](./field-groups/plan/healthcare-plan-details.md)
   * Prodotto {#product}
      * [Catalogo dei prodotti](./field-groups/product/product-catalog.md)
      * [Categoria di prodotti](./field-groups/product/product-category.md)
   * Provider {#provider}
      * [Fornitore sanitario](./field-groups/provider/healthcare-provider.md)
   * [Aggiornamenti dei nomi dei gruppi di campi](./field-groups/name-updates.md)
* Tipi di dati {#data-types}
   * [Dettagli account](./data-types/account-details.md)
   * [Pausa annunci](./data-types/ad-break.md)
   * [Applicazione](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Dettagli del browser](./data-types/browser-details.md)
   * [Origine B2B](./data-types/b2b-source.md)
   * [Commerce](./data-types/commerce.md)
   * [Stringa di consenso](./data-types/consent-string.md)
   * [Consensi e preferenze](./data-types/consents.md)
   * [Valuta](./data-types/currency.md)
   * [Dispositivo](./data-types/device.md)
   * [Indirizzo e-mail](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Canale esperienza](./data-types/experience-channel.md)
   * [Attributi di controllo del sistema di origine esterna](./data-types/external-source-system-audit-attributes.md)
   * [Conto finanziario](./data-types/financial-account.md)
   * [Campo di consenso generico](./data-types/consent-field.md)
   * [Campo preferenza marketing generico](./data-types/marketing-field.md)
   * [Campo preferenza marketing generico con sottoscrizioni](./data-types/marketing-field-subscriptions.md)
   * [Campo preferenza personalizzazione generica](./data-types/personalization-field.md)
   * [Geo](./data-types/geo.md)
   * [Cerchio geografico](./data-types/geo-circle.md)
   * [Coordinate geografiche](./data-types/geo-coordinates.md)
   * [Dettagli interazione geografica](./data-types/geo-interaction-details.md)
   * [Forma geografica](./data-types/geo-shape.md)
   * [Identità](./data-types/identity.md)
   * [Impression](./data-types/impressions.md)
   * [Dettagli di implementazione](./data-types/implementation-details.md)
   * [Ricerca interna del sito](./data-types/internal-site-search.md)
   * [Coppia di valori chiave](./data-types/key-value-pair.md)
   * [Marketing](./data-types/marketing.md)
   * [Misura](./data-types/measure.md)
   * [Ordine](./data-types/order.md)
   * [Elemento di pagamento](./data-types/payment-item.md)
   * [Utente](./data-types/person.md)
   * [Nome della persona](./data-types/person-name.md)
   * [Numero di telefono](./data-types/phone-number.md)
   * [Posizionare il contesto](./data-types/place-context.md)
   * [Dettagli POI](./data-types/poi-details.md)
   * [Interazione POI](./data-types/poi-interaction.md)
   * [Indirizzo postale](./data-types/postal-address.md)
   * [Voce dell’elenco dei prodotti](./data-types/product-list-item.md)
   * [Cerca](./data-types/search.md)
   * [Abbonamento](./data-types/subscription.md)
   * [Abbonamento a domicilio](./data-types/telecom-subscription.md)
   * [Transazione](./data-types/transaction.md)
   * [Informazioni web](./data-types/web-information.md)
   * [Interazione web](./data-types/web-interaction.md)
   * [Dettagli della pagina web](./data-types/webpage-details.md)
* [!UICONTROL Schemi] Interfaccia {#ui}
   * [Panoramica](./ui/overview.md)
   * [Esplorare le risorse XDM](./ui/explore.md)
   * Creare e modificare le risorse {#resources}
      * [Schemi](./ui/resources/schemas.md)
      * [Classi](./ui/resources/classes.md)
      * [Gruppi di campi](./ui/resources/field-groups.md)
      * [Tipi di dati](./ui/resources/data-types.md)
   * Definire i campi {#fields}
      * [Panoramica](./ui/fields/overview.md)
      * [Campi obbligatori](./ui/fields/required.md)
      * [Campi oggetto](./ui/fields/object.md)
      * [Campi array](./ui/fields/array.md)
      * [Campi enumerati](./ui/fields/enum.md)
      * [Campi di identità](./ui/fields/identity.md)
      * [Campi di relazione](./ui/fields/relationship.md)
   * [Flussi di lavoro basati sul campo](./ui/field-based-workflows.md)
   * [Genera dati XDM di esempio](./ui/sample.md)
   * [Esportare schemi XDM](./ui/export.md)
* API del Registro di sistema dello schema {#api}
   * [Panoramica](api/overview.md)
   * [Introduzione](api/getting-started.md)
   * [Schemi](api/schemas.md)
   * [Comportamenti](api/behaviors.md)
   * [Classi](api/classes.md)
   * [Gruppi di campi dello schema](api/field-groups.md)
   * [Tipi di dati](api/data-types.md)
   * [Descrittori](api/descriptors.md)
   * [Unioni](api/unions.md)
   * [Conversione da CSV a schema](api/csv-to-schema.md)
   * [Esporta](api/export.md)
   * [Importa](api/import.md)
   * [Dati di esempio](api/sample-data.md)
   * [Registro di controllo](api/audit-log.md)
   * [Schemi ad hoc](api/ad-hoc.md)
   * [Mixins (obsoleto)](api/mixins.md)
   * [Appendice](api/appendix.md)
* Tutorial {#tutorials}
   * [Creare uno schema nell’interfaccia utente](tutorials/create-schema-ui.md)
   * [Creare uno schema nell’API](tutorials/create-schema-api.md)
   * [Definire campi personalizzati nell’API](./tutorials/custom-fields-api.md)
   * [Aggiungere valori consigliati a un campo (API)](tutorials/suggested-values.md)
   * [Campo XDM obsoleto](tutorials/field-deprecation.md)
   * [Definire una relazione di schema nell’interfaccia utente](tutorials/relationship-ui.md)
   * [Definire una relazione di schema nell’API](tutorials/relationship-api.md)
   * [Definire una relazione di schema in Real-time CDP B2B Edition](tutorials/relationship-b2b.md)
   * [Gestione delle etichette di utilizzo dei dati per uno schema](tutorials/labels.md)
   * [Creare uno schema ad hoc](tutorials/ad-hoc.md)
* [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
* [Riferimento API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)
* [Note sulla versione di Platform](https://www.adobe.com/go/platform-release-notes-en)