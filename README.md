# Open Trade Transfer Package
A structure that allows files to be generated to facilitate the exchange of data concerning trade. It can be utilized to exchange information on product specifications, requirements, defaults and restrictions as well as capabilities. It can also be used to exchange a material list or other needed related data.

Is meant to facilitate both XML and JSON creation.

## How to define the file as an Open Trade Transfer Package
The root level should be an element with the name of "open_trade_transfer_package":

#### Examples
```
{
  "open_trade_transfer_package": {
    "version": 1.0,
    {content here}
}
```

```
<?xml version = 1.0 encoding = "UTF-8"?>
<open_trade_transfer_package version="1.0">
  {content here}
</open_trade_transfer_package>
```

## Version
Current version is 1.0. This should stated in every file as showed in the example above. 1.0 is the first released version, and there are no prior versions.

## Structure
Within the root level (open_trade_transfer_package) everything is divided into four groups and their subgroups:

- information
- products
  - product (can be many)
- profiles
  - defaults
  - enforced
  - restricted
- capabilities
  - summary
  - materials
- custom
  - colors
  - materials

# JSON schema
JSON schema is available in the versions folder. To link to it, please use the raw link. The schema allows you to validate your OTTP file syntax. An example of how this is done in Ruby with the [json-schema GEM](https://github.com/ruby-json-schema/json-schema) below:

```
ottp = '{
  "open_trade_transfer_package": {
    "version": 1.0,
    "information": {
      "company": "Elmatica as",
      "created": "2017-04-03T08:00:00Z"
    },
    "profiles": {
      "restricted": {
        "generic": {
          "version": 1.0,
          "country_of_origin": {
            "nato_member": false
          }
        }
      }
    }
  }
}'

puts JSON::Validator.validate!('https://raw.githubusercontent.com/elmatica/Open-Trade-Transfer-Package/master/v1/ottp_schema.json', ottp)
```

## Data formats
When possible subelements are documented, they need to specify what format to use. Possible formats are:

- Percentage - Denotes a percentage - all percentages are expressed as percent out of 100- for example 10.4% is written as "10.4" and not "0.104"
- List - The data has only a fixed number of values that are selected from the list in the description table for the tag.  These items are case sensitive, and no other values are allowed.
- Text - The data is free format text.  For multiline entries, line breaks will be preserved where possible and the text may be truncated on import if the text is too long for the importing program to store.  Multiline entries may be split with either a newline (Unix format) or a carriage return – newline combination (DOS format).  Importing programs should accept either.
- Boolean - May be either TRUE or FALSE, with TRUE and FALSE in capitals.  A default value should be specified for optional fields - the default is used if the value is not present.
- Integer - An integer number with no decimal point.  May include negative values - examples include ...-3, -2, -1, 0, 1, 2, 3,...
- Float - A floating point number, usually expressed in its simplest form with a decimal point as in "1.2", "0.004", etc...  Programs shall endeavor to store as many significant digits as possible to avoid truncating or losing small values.
- Range - contains two values separated by three dots. E.g. "1...3". If a range is allowed, then the kind of format that the range can contain must also be specified. Decimals are allowed, e.g. "1.2...4.2".
- Stringlist - several values separated by a comma, e.g. "1,TEST,TEST2"

## Possible elements in the "information" group

### company
A string wih the company who owns the information in the file

### person
A string with the person responsible for the information in the file

### editor_software
Astring with the software that has generated the file

### created
The timestamp of the creation of the file, in format RFC 3339 date-time

### updated
The timestamp of the last update of the file, in format RFC 3339 date-time

### project
A string with name of the project included in the file

### version
A number with the version of the information included in the file

### Description
A string representing the description of the content

## Possible generic elements in the products/profile/capability sections.
If you want to place generic information in the file, you should enclose the information within a section called "generic". E.g. if you wanted to create a profile indicating that no products can be manufactures outside NATO countries, you could do it like this:

```
{
  "open_trade_transfer_package": {
    "version": 1.0,
    "information": {
      "company": "Elmatica as",
      "created": "2017-04-03T08:00:00Z"
    },
    "profiles": {
      "restricted": {
        "generic": {
          "version": 1.0,
          "country_of_origin": {
            "nato_member": false
          }
        }
      }
    }
  }
}
```

### Standards and Requirements ("standards")
If the format is boolean and nothing is stated other than the name of the standard in the Description column, it should be understood as follows: Are to be met (if Specification), required/restricted/default (in Profile) or possible (in Capability)

Data tag | Format | Description
---------|--------|---|---|---|-------------
*ul* | Boolean | Indicating if UL is required for the board. Can not be used as a capability, as this will be indicated on each material
*c_ul* | Boolean | Indicating if Canadian UL is required for the board. Can not be used as a capability, as this will be indicated on each material
*rohs* | Boolean | RoHS
*itar* | Boolean | ITAR
*dfars* | Boolean | DFARS

E.g. this would indicate that UL approval should be handled as a default if not otherwise instructed:
```
{
  "open_trade_transfer_package": {
    "version": 1.0,
    "information": {
      "company": "Elmatica as",
      "created": "2017-04-03T08:00:00Z"
    },
    "profile": {
      "default": {
        "generic": {
          "version": 1.0,
          "standards": {
            "ul": true
          }
        }
      }
    }
  }
}
```

### Country of Origin ("country_of_origin")

Data tag | Format | S | P | C | Description
---------|--------|---|---|---|-------------
*iso_3166_1_alpha_3* | String | A three letter string representation of the Country of origin according too ISO 3166-1
*iso_3166_1_alpha_2* | String | A two letter string representation of the Country of origin according too ISO 3166-1
*nato_member* | Boolean | Indicates if the COO is a NATO member state (or needs to be if used as a profile)
*eu_member* | Boolean | Indicates if the COO is a European Union member state (or needs to be if used in a profile)

## The custom elements
This element is where you place description of colors or materials

### Colors

Data tag | Format | S | P | C | Description
---------|--------|---|---|---|-------------
*name* | String | Any name to describe the colour
*value_type* | String | Can be any of "hex", "rgb", "cmyk" or "name"
*value* | String | If value_type is hex, the value needs to be a \"#\" + 6 hexadecimals (e.g. \"#FFFFFF\"). for \"rgb\" the format is \"rgb(0, 255, 255)\", for \"cmyk\" the format is \"cmyk(100%, 0%, 0%, 0%)\". The name is just a string.

**Example:**
```
...
  "custom": {
    "colors": [
      {
        "name": "orange",
        "value_type": "hex",
        "value": "#f4ad42"
      }
    ]
  }
...
```

## Examples
Look in the examples folder

## Projects using this package format:
- Open Trade Transfer Package: Printed Circuits Fabrication Data
[Open Trade Transfer Package: Printed Circuits Fabrication Data](https://github.com/elmatica/Open-Trade_Printed_Circuits_Fabrication_Data)
