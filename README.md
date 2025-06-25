# Expanded Topbar Framework
This is a framework for mods to add elements to the topbar.

## Steam Page
TBD

## How to Use
### Adding a new Topbar element
> **NOTE:** all of this should be configured in your own mod!

There is a built-in scripted effect to add new topbar elements for modders `add_com_topbar_element`.
As input (`element_name`), it requires a localization key.
```
add_com_topbar_element = {
    element_name = com_topbar_element_prestige
}
```
The localization key needs to refer to an existing localization key.
The following localization keys need to be setup for the element to work correctly (`<element name>` is a placeholder and needs to be replaced with your own name):
- **Required:** `<element name>` this is the element name referenced by `add_com_topbar_element` and it needs to contain the element name itself
- **Required:** `<element name>_icon` this is the icon shown in the topbar. It should be a text icon.
- **Required:** `<element name>_value` this is the value shown in the topbar
- **Required:** `<element name>_tooltip` this is the tooltip when hovering the topbar element
- **Required:** `<element name>_source` this will be shown in the configuration window and should contain the name of your mod
- **Required:** `<element name>_source_tooltip` this tooltip will be shown when hovering over the `source` in the configuration window
- **Optional:** `<element name>_window` if set this value will be set as a gui variable for `com_window_open` when the topbar element is clicked and can be checked like this: `[GetVariableSystem.HasValue('com_open_window', 'text in <element name>_window')]`

Here is an example for `com_topbar_element_prestige` as used above:
```
l_english:
 # Prestige
 com_topbar_element_prestige: "com_topbar_element_prestige"
 com_topbar_element_prestige_icon: "@prestige!"
 com_topbar_element_prestige_value: "[GetPlayer.GetPrestige|v]"
 com_topbar_element_prestige_tooltip: "#header [concept_prestige]#!\n$concept_prestige_desc$"
 com_topbar_element_prestige_source: "Victoria 3"
 com_topbar_element_prestige_source_tooltip: "This element is part of the default Expanded Topbar Framework."
```

Lastly, there needs to be an SGUI configured that has the same name as the element (`<element name>`).
Only the `is_shown` attribute is parsed by the framework.
This can be used to show or hide specific elements for specific countries.

Here is an example for `com_topbar_element_prestige` as used above:
```
com_topbar_element_prestige = {
    scope = country

    is_shown = {
        always = yes
    }
}
```