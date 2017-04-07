# Open Trade Transfer Package
A structure that allows files to be generated to facilitate the exchange of data concerning trade. It can be utilized to exchange information on product specifications, requirements, defaults and restrictions as well as capabilities. It can also be used to exchange a material list or other needed related data.

Is meant to facilitate both XML and JSON creation.

## How to define the file as an Open Trade Transfer Package
The root level should be an element with the name of "open_trade_transfer_package":

#### Examples
```
{
  "open_trade_transfer_package": {
    "version": "0.1",
    {content here}
}
```

```
<?xml version = "1.0" encoding = "UTF-8"?>
<open_trade_transfer_package version="0.01">
  {content here}
</open_trade_transfer_package>
```

## Version
Current version is 0.1. This should stated in every file as showed in the example above. 0.1 is the first released version, and there are no prior versions.

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

## Data formats
When possible subelements are documented, they need to specify what format to use. Possible formats are:

- Percentage - Denotes a percentage - all percentages are expressed as percent out of 100- for example 10.4% is written as "10.4" and not "0.104"
- List - The data has only a fixed number of values that are selected from the list in the description table for the tag.  These items are case sensitive, and no other values are allowed.
- Text - The data is free format text.  For multiline entries, line breaks will be preserved where possible and the text may be truncated on import if the text is too long for the importing program to store.  Multiline entries may be split with either a newline (Unix format) or a carriage return – newline combination (DOS format).  Importing programs should accept either.
- Boolean - May be either TRUE or FALSE, with TRUE and FALSE in capitals.  A default value should be specified for optional fields - the default is used if the value is not present.
- Integer - An integer number with no decimal point.  May include negative values - examples include ...-3, -2, -1, 0, 1, 2, 3,...
- Floating Point - A floating point number, usually expressed in its simplest form with a decimal point as in "1.2", "0.004", etc...  Programs shall endeavor to store as many significant digits as possible to avoid truncating or losing small values.

## Possible elements in the "information" group

### company
The company that wants who owns the information in the file

### person
The person responsible for the information in the file

### editor_software
The software that has generated the file

### created
The timestamp of the creation of the file, in format YYYY-MM-DD HH:MM:SS

### updated
The timestamp of the last update of the file, in format YYYY-MM-DD HH:MM:SS

### project
The name of the project included in the file

### version
The version of the information included in the file

### Examples
Look in the examples folder

## Projects using this package format:
- Open Trade Transfer Package: Printed Circuits Fabrication Data
[Open Trade Transfer Package: Printed Circuits Fabrication Data](https://github.com/elmatica/Open-Trade_Printed_Circuits_Fabrication_Data)
