# Open Trade Transfer Package
An structure that allows files to be generated to facilitate the exchange of data concerning trade. It can be utilized to exchange information on product specifications, requirements, defaults and restrictions as well as capabilities. It can also be used to exchange a material list or other needed related data.

Is meant to facilitate both XML and JSON creation.

## How to define the file as an Open Trade Transfer Package
Within the root level, you need to specify an element with the name of "open_trade_transfer_package":

#### Examples
```
{
  "open_trade_transfer_package": {
    "version": "0.1"
}
```

```
<?xml version = "1.0" encoding = "UTF-8"?>
<open_trade_transfer_package version="0.01">
</open_trade_transfer_package>
```

## Version
Current version is 0.1. This should stated in every file as shoed in the example above. 0.1 is the first released version, and there is no prior versions.

## Structure
Within the root level (open_trade_transfer_package) everything is divided into four groups and their subgroups:

- information
- products
  - product (can be many)
- profiles
  - defaults
  - enforced
  - restricted
- capability
  - summary
  - materials
- custom
  - colors
  - materials

## Possible elements in the "information" group

### company
The company that wants who owns the information in the XML

### person
The person responsible for the information in the XML

### editor_software
The software that has generated the XML

### created
The timestamp of the creation of the XML, in format YYYY-MM-DD HH:MM:SS

### updated
The timestamp of the last update of the XML, in format YYYY-MM-DD HH:MM:SS

### project
The name of the project included in the XML

### version
The version of the information included in the XML

### Examples
Look in the examples folder

## Projects using this package format:
Open Trade Transfer Package: Printed Circuits Fabrication Data
[Open Trade Transfer Package: Printed Circuits Fabrication Data](https://github.com/elmatica/OpenTrade_PrintedCircuitsFabricationData)
