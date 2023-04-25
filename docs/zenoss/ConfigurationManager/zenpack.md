# Configuration Manager

## Subscription

This integration is a subscription-based Professional Services
engagement. Our Integration Services are offered as subscriptions in
order to provide initial setup and ongoing compatibility and
maintenance. All standard packages are renewable every 12 months from
the date of purchase. [Contact Zenoss](https://tryit.zenoss.com/zenpack-contact){.external-link} to
request more information regarding this or any other ZenPacks.

### Authors:

Zenoss Inc.

### Maintainers:

Zenoss Inc.

### Organization:

Zenoss Inc.

### Name:

Configuration Manager Integration Service

### Version:

3.3.1

### More Information:

## Configuration Manager Integration Service

This annual subscription service allows Zenoss RM/CZ configuration to be
sent from one RM/CZ to another and provides a UI for comparing
configuration snapshots. This integration is renewable every 12 months
from the date of purchase and is designed to offer ongoing compatibility
between the products.

## About

The Configuration Manager ZenPack provides a facility for the export,
import and
comparison of Zenoss monitoring configurations. Selection criteria can
be defined to
determine what configuration data is exported. Imported packages of
configuration
data can be selectively applied to the running Zenoss system, or used in
comparisons
with other import configuration change packages.

The ZenPack must be installed on both the source and the target systems.

## Features

-   Supports both file-based and Rabbit AMQP-based import/export.
-   A daemon to read exported data from queues and automatically import
    changes.
-   A user interface for comparing Imported Change Packages.
-   Pre-configured selection criteria templates and an export wizard.
-   One-click configuration snapshot export

|                    |                                                   |
|--------------------|---------------------------------------------------|
| Prerequisite       | Restriction                                       |
| Product            | RM 5.2.6 or higher (untested on earlier versions) |
| Required ZenPacks  | ZenPacks.zenoss.PS.Util 1.9.0 or higher           |
| Other dependencies | None                                              |

## Additional Documentation

[![](rest/documentConversion/latest/conversion/thumbnail/48038242/1)](/download/attachments/48038240/ConfigMan_3.1.0.pdf?version=1&modificationDate=1645716858000&api=v2){.confluence-embedded-file}

##  Changelog

3.3.1

Fixes

-   hotfix-3.3.1: fix tuple import
    when existing value is falsey

3.3.0

Features

-   SVC-3180 allow filtering of
    devices by collector for export

Fixes

-   SVC-3279 unicode added as valid
    type
-   SVC-3279 logging for unknown type
-   SVC-3289 stop exporting relation to containing parent, import
    non-containing relations
-   SVC-3291 don't create properties when we just want to set values
-   SVC-3290 guard against missing and renamed triggers
-   SVC-3285 nonAQgetattr implementation
-   SVC-3281 use value from ExportedDataValue for perfServer, ignore
    some old-style attributes
-   SVC-3281 guard against missing perfServer
-   SVC-3295 allow None values to be exported
-   SVC-3295 several fixes for resolving and applying objects properly
-   SVC-3295 use trigger id instead of name and do not try to coerce
    None values

3.2.0

Fixes

-   SVC-3212 Common data value
    object for improved diff and apply, code consistency
-   SVC-3103 Change sorting approach for changeSets, Added auto re-apply
    for changeSets that failed apply
-   SVC-3207 Improve handling of attributes from ZenPack supplied
    objects
-   SVC-2965 Changed source_system_id and source_system_name
-   SVC-3168 Improve Chanagesets Cart behaviour when moving about UI
-   SVC-3229 Export to Local options documentation
-   SVC-3195 Added documentation about export checkbox 'Ignore objects
    installed by ZenPacks?'
-   SVC-3275 fixes from testing, avoid halting on unresolvable property
    types, fix tuple import, add doctring to ReportSelector, remove
    redundant path info from logging, do not compare hidden properties,
    ensure string compares are actually between strings, New flag to
    enable profiling dumps
-   SVC-3270 Fix issue with version 3.1.0 failing to install

Features

-   SVC-3193 Exporting and
    importing of RM Reports

3.1.0

Fixes

-   SVC-3107 Fix CPropImporter, multiple value type handling, list
    object compare
-   SVC-3108 Add 'description' field when applying cProps
-   SVC_3113 Fix object attribute processing
-   SVC-3116 Fix ListImporter to process itemDiffs in order of the list
-   SVC_3118 New ThresholdClassImporter to handle proper setup of
    'dsnames' attribute
-   SVC-3118 Update ListImporter to handle attributes
-   SVC-3120 Added check for unwanted acquisition objects
-   SVC-3123 New exporter for graphpoints
-   SVC-3124 Stop Comparator coercion of items to strings
-   SVC-3128 Reworked notification subscription export/import
-   SVC-3129 Reworked notification recipients export/import
-   SVC-3130 Export data from trigger subscribers tab
-   SVC-3131 Diff UI improvements in Changesets selectors panel
-   SVC-3134 Exporters and importers for process class & organizer for
    additional properties
-   SVC-3137 IpServiceClass importer for name
-   SVC-3138 Export title for services organizer and os process
-   SVC-3174 UI: paging for changePackage combobox
-   SVC-3209 Remove old reports

Features

-   SVC-3101 Fixed and extended selection criteria for userCommands to
    include Infrastructure user commands
-   SVC-3181 Allow setting of default collector for device imports where
    exported collector does not exist

3.0.2

Fixes

-   SVC-3093: correctly use
    [ExportedObjectReference.id](http://ExportedObjectReference.id){.external-link}
    when checking for existing objects
-   SVC-3087: allow sending of ServiceOrganizer and OSProcessOrganizer

3.0.1

Fixes

-   SVC-3076: include dependency on PS.Util ZP
-   SVC-2791: (cherry-picked) make changeset loading more robust

3.0.0

Features

-   Completely rewritten export/import functionality
    -   far more granular
    -   not reliant on ZenBatchDump/Load
    -   ZenPacks can define their own custom export/import/compare
        plugins
    -   more efficient export
    -   numerous bugs fixed/avoided
-   new comparison engine and UI
-   1-click and automated snapshot capabilities
-   auto-expire of change packages
-   local export directly to ImportedChangePackage
-   can select ChangeSets from existing ChangePackages to create new
    ChangePackages
-   re-ship existing ChangePackage to another server
-   (the above features are encompassed by SVC-2789)

2.5.3

Fixes

-   SVC-2862: BatchDeviceLoader fix if properties are greater than 255

2.5.2

Fixes

-   SVC-2711: Update config.zcml to prevent ETL from picking up
    ConfigMan related items

2.5.1

Fixes

-   Fix invalid character encodings causing issues with daemon startup

2.5.0

Features

-   SVC-2673 Support 'password' and 'boolean' zTypes

2.4.0

Features

-   SVC-1027: Add force_apply into UI
-   SVC-1027: Enhance logging
-   SVC-1027: Add \`\`Test Access\`\` for Targets and Sources
-   SVC-1027: Add export devices based on production state
-   SVC-2480: Remove DiffDeviceClassTree.py
-   SVC-2641: Add Globals to bin/zensyncer
-   SVC-2623: Enhance Device Dumper to omit non-serializable values
-   SVC-2639: Update routing key info
-   SVC-2646: Patch properties in zensyncer if CMDB zenpack is installed
-   SVC-2646: Fix testEmitDev test

2.3.0

Features

Templating facility

-   SVC-2093: Create Criteria Template entity
-   SVC-2093: Create Migration for criteria templates
-   SVC-2093: Create methods for criteria templates
-   SVC-2093: Implement UI for instantiate template
-   SVC-2093: Add information to template details page
-   SVC-2093: Fixes according review comments
-   SVC-2093: Fix selecting first template during loading page
-   SVC-2093: Move template creating from migration to install
-   SVC-2093: Fixed plugin name in templates.yaml and template id in
    router
-   SVC-2093: Remove addTemplate method from facade
-   SVC-2093: Fixed userAndGroup criteria name

Migration Wizard

-   SVC-2094: Add MigrationWizard dialog
-   SVC-2094: Add SelectTarget card into wizard
-   SVC-2094: Add SelectCriteriaGroups into wizard
-   SVC-2094: Add templates, groups, migration info
-   SVC-2094: Implement run button (MigrationWizard)
-   SVC-2094: Fix unsubscribe group problems, hide wizard's groups
-   SVC-2094: Add two default targets during install ZP
-   SVC-2094: Change the MigrationWizard size
-   SVC-2094: Change prefix for Wizard's groups
-   SVC-2094: Add tips on every step (Wizard)
-   SVC-2094: Fixed a grammatical error
-   SVC-2094: Add Remove Wizard Generation button
-   SVC-2094: Simplify removing Wizard Generations
-   SVC-2094: Change message in removeWizardGenerations
-   SVC-2094: Change distance between Wizard buttons
-   SVC-2094: Add validation for instantiating template
-   SVC-2094: Fix adding of default targets. Change template validation
-   SVC-2094: Update tips in Wizard, rename Remove Wizard Generations
    button

Fixes and Enhancements

-   SVC-1369: Implement migration of email notifications with inherited
    SMTP settings, fix migration of notification's password
-   SVC-1486: Fix empty user TZ after migration
-   SVC-1486: Set timezone after updating user
-   SVC-1492: Fix migrating more than 255 properties
-   SVC-1856: Fix importing trigger users
-   SVC-1921: Remove reports folder and files
-   SVC-1921: Add migration for removing reports, change remove method
-   SVC-1921: Remove the mentions about report
-   SVC-1921: Roll back the ImportedChangePackage and report plugins
-   SVC-2014: Fix creating extra locations after migration
-   SVC-2095: Add in many unit tests
-   SVC-2116: Fix error during looping over modes at setMode
-   SVC-2270: Prevent user and group creation in CZ
-   SVC-2270: Change log message
-   SVC-2094: Implement run button (MigrationWizard)
-   SVC-2094: Fix unsubscribe group problems, hide wizard's groups
-   SVC-2094: Add two default targets during install ZP
-   SVC-2094: Change the MigrationWizard size
-   SVC-2094: Change prefix for Wizard's groups
-   SVC-2094: Add tips on every step (Wizard)
-   SVC-2094: Fixed a grammatical error
-   SVC-2094: Add Remove Wizard Generation button
-   SVC-2094: Simplify removing Wizard Generations
-   SVC-2094: Change message in removeWizardGenerations
-   SVC-2094: Change distance between Wizard buttons
-   SVC-2094: Add validation for instantiating template
-   SVC-2094: Fix adding of default targets. Change template validation
-   SVC-2094: Update tips in Wizard, rename Remove Wizard Generations
    button

Fixes and Enhancements

-   SVC-1369: Implement migration of email notifications with inherited
    SMTP settings, fix migration of notification's password
-   SVC-1486: Fix empty user TZ after migration
-   SVC-1486: Set timezone after updating user
-   SVC-1492: Fix migrating more than 255 properties
-   SVC-1856: Fix importing trigger users
-   SVC-1921: Remove reports folder and files
-   SVC-1921: Add migration for removing reports, change remove method
-   SVC-1921: Remove the mentions about report
-   SVC-1921: Roll back the ImportedChangePackage and report plugins
-   SVC-2014: Fix creating extra locations after migration
-   SVC-2095: Add in many unit tests
-   SVC-2116: Fix error during looping over modes at setMode
-   SVC-2270: Prevent user and group creation in CZ
-   SVC-2270: Change log message

2.2.7

Features

-   SVC-1750: Use 'run -c' for service startup command
-   SVC-1750: Monkeypatch to disable sending collection metrics

2.2.6

Features

-   filter configs properly for zensyncd (unhandled exception: tag)
-   fix install on pre-5.2 RM
-   simplify property export filters and expand to fix a few more

## Attachments:

-   [ConfigMan_3.1.0.pdf](https://storage.googleapis.com/zenoss-doc-artifacts/ConfigurationManager/configman_3.1.0.pdf){.external-link}

