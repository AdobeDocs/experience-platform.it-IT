---
product: experience-platform
audience: user
user-guide-title: Guida del sistema Experience Data Model (XDM)
breadcrumb-title: Guida di Data Model (XDM)
user-guide-description: Utilizza le classi e i mixin Experience Data Model (XDM) per standardizzare i dati dell’esperienza.
feature: Schemi
translation-type: tm+mt
source-git-commit: 27cdb65c846293d7edce340e1cb5a360c0e40604
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 22%

---


# Sistema Experience Data Model (XDM) {#xdm}

* [Panoramica del sistema XDM](home.md)
* Schemi {#schema}
   * [Nozioni di base sulla composizione dello schema](schema/composition.md)
   * [Best practice per la modellazione dei dati](schema/best-practices.md)
   * [Vincoli del tipo di campo XDM](schema/field-constraints.md)
   * [Dizionario dei campi XDM](schema/field-dictionary.md)
* Classi {#classes}
   * [Profilo individuale XDM](./classes/individual-profile.md)
   * [ExperienceEvent XDM](./classes/experienceevent.md)
* Mixins {#mixins}
   * Mixer di profili {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Dettagli demografici](./mixins/profile/person-details.md)
      * [Dati di contatto personali](./mixins/profile/personal-details.md)
      * [Dettagli di appartenenza al segmento](./mixins/profile/segmentation.md)
      * [Dettagli contatto lavoro](./mixins/profile/work-details.md)
   * Mixer eventi {#event}
      * [Dettagli ID utente finale](./mixins/event/enduserids.md)
      * [Dettagli dell&#39;ambiente](./mixins/event/environment-details.md)
   * [Aggiornamenti dei nomi misti](./mixins/name-updates.md)
* Tipi di dati {#data-types}
   * [Applicazione](./data-types/application.md)
   * [Beacon](./data-types/beacon.md)
   * [Dettagli del browser](./data-types/browser-details.md)
   * [Commerce](./data-types/commerce.md)
   * [Consensi e preferenze](./data-types/consents.md)
   * [Dispositivo](./data-types/device.md)
   * [Indirizzo e-mail](./data-types/email-address.md)
   * [Ambiente](./data-types/environment.md)
   * [Geo](./data-types/geo.md)
   * [Cerchio geografico](./data-types/geo-circle.md)
   * [Coordinate geografiche](./data-types/geo-coordinates.md)
   * [Dettagli interazione geografica](./data-types/geo-interaction-details.md)
   * [Forma geografica](./data-types/geo-shape.md)
   * [Identità](./data-types/identity.md)
   * [Misura](./data-types/measure.md)
   * [Ordine](./data-types/order.md)
   * [Elemento di pagamento](./data-types/payment-item.md)
   * [Persona](./data-types/person.md)
   * [Nome della persona](./data-types/person-name.md)
   * [Numero di telefono](./data-types/phone-number.md)
   * [Posizionare il contesto](./data-types/place-context.md)
   * [Dettagli POI](./data-types/poi-details.md)
   * [Interazione POI](./data-types/poi-interaction.md)
   * [Indirizzo postale](./data-types/postal-address.md)
   * [Ricerca](./data-types/search.md)
   * [Abbonamento](./data-types/subscription.md)
   * [Interazione web](./data-types/web-interactions.md)
   * [Dettagli della pagina web](./data-types/webpage-details.md)
* [!UICONTROL Schemas] Interfaccia {#ui}
   * [Panoramica](./ui/overview.md)
   * [Esplorare le risorse XDM](./ui/explore.md)
   * Creare e modificare risorse {#resources}
      * [Schemi](./ui/resources/schemas.md)
      * [Classi](./ui/resources/classes.md)
      * [Mixins](./ui/resources/mixins.md)
      * [Tipi di dati](./ui/resources/data-types.md)
   * Definire i campi {#fields}
      * [Panoramica](./ui/fields/overview.md)
      * [Campi obbligatori](./ui/fields/required.md)
      * [Campi oggetto](./ui/fields/object.md)
      * [Campi array](./ui/fields/array.md)
      * [Campi enumerati](./ui/fields/enum.md)
      * [Campi di identità](./ui/fields/identity.md)
      * [Campi di relazione](./ui/fields/relationship.md)
   * [Genera dati XDM di esempio](./ui/sample.md)
   * [Esportare schemi XDM](./ui/export.md)
* API del Registro di sistema dello schema {#api}
   * [Panoramica](api/overview.md)
   * [Introduzione](api/getting-started.md)
   * [Schemi](api/schemas.md)
   * [Comportamenti](api/behaviors.md)
   * [Classi](api/classes.md)
   * [Mixins](api/mixins.md)
   * [Tipi di dati](api/data-types.md)
   * [Descrittori](api/descriptors.md)
   * [Unioni](api/unions.md)
   * [Esporta/Importa](api/export-import.md)
   * [Dati di esempio](api/sample-data.md)
   * [Registro di controllo](api/audit-log.md)
   * [Schemi ad hoc](api/ad-hoc.md)
   * [Appendice](api/appendix.md)
* Tutorial {#tutorials}
   * [Creare uno schema (interfaccia utente)](tutorials/create-schema-ui.md)
   * [Creare uno schema (API)](tutorials/create-schema-api.md)
   * [Definire una relazione tra due schemi (interfaccia utente)](tutorials/relationship-ui.md)
   * [Definire una relazione tra due schemi (API)](tutorials/relationship-api.md)
   * [Creare uno schema ad-hoc (API)](tutorials/ad-hoc.md)
* [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
* [Riferimento API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Note sulla versione di Platform](https://www.adobe.com/go/platform-release-notes-en)