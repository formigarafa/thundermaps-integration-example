# SampleIntegration

## Description
This project is to be uses as reference when building new ThunderMaps
Integrations.

## Composition
Every ThunderMaps Integration is supposed to be a Rails Engine, but depending on
how simple is the integration any well structured gem may suffice.

## Initialization
The integration engine should include a initializer script in its
`config/initializers` directory connect the integration via subscribing to
published events and/or via registering callbacks to provide data.

The integration engine may also be provided with a rails initializer script to
be included in the main app to setup any eventual per environment requirement.

## Integration points
The application provide currently the following list of integration points but
that list can be extended on request if considered reasonable by ThunderMaps
Team.
Is worth saying that all of these integration points are optional so you can
implement only what is required for each case. But obviously, if you are providing
a `*_form` callback you will want to subscribe to one of the respective events
avalilable to make use of the data provided on such form fields.

### Channel Integrations
A report object is provided with all available information to every integration point in the list below.
* `:report_form_created_sync`: Event triggered on creation of a report. The date provided in the integrated form will be available under `report.integrated_forms[integration_name]` hash.
* `:report_form_created_async`: Event triggered asynchronously after a report creation.
* `:report_form`: Callback used to build integrated form fields to be presented with report form.
* `:report_data`: Callback used to retrieve data from integration to be displayed with a report.

### Configuration Integrations
A channel object is provided with all available information to every integration point in the list below.
* `:configuration_form`: Callback used to build configuration form to be presented to the user when he is configuring details for the integration.
* `:configuration_data`: Callback used to retrieve configuration for current integration.
* `:configuration_data_updated`: Event triggered when user updates its settings on integration configuration. Besides the channel object, a `updated_settings` hash is provided with this event to be stored and/or used as required.

## Initializer example:
This snippet of code shows what the integration engine could provide as
initializer to be included in the main app
```
# enabling presentation of integrated data
SampleIntegration.integrated_report_is_to_be_shown = Rails.env.production?
```

## Copyright and license
Code and documentation Copyright 2016 Cloudsource LTD. Code released under the MIT license.
