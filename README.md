# MasterScript

MasterScript is a utility to easily import Qlik Sense master items from an external table via the Qlik application data model. For those situation where a bulk load of master items is necessary to load a business data dictionary to your application, then MasterScript is the tool for you!

## How to get started?
1. Install the extension via QMC
1. Load your metadata in the format outlined below to your application data model
1. Add the MasterScript extension to your application sheet
1. Open MasterScript
1. Click "Import Master Items"
1. Check the status
1. Delete the MasterScript extension from your application sheet
1. Build your application

## Loading metadata
The metadata required by the extension must be in a pre-defined format, the easiest way to load this is with the sample spreadsheet which has all the required column headers in a single table. It is also possible to use the data transformation capabilities in Qlik Sense to convert to this format once loaded in a different structure.

The format is designed for ease of manual completion in a spreadsheet, hence the flat nature of the data structure.

The fields have a "_" prefix so this can be combined with the ___set HidePrefix = '\_'___ option

### The data format
* _MasterItemID
  * A unique ID for the master item, this will be used to apply updates, so the name of a master item can be changed
* _MasterItemType
  * A value of either "Measure" or "Dimension"
* _MasterItemName
  * The name for the master item, this will be displayed in the master items panel
* _MasterItemDescription
  * The contents for the Description field seen when creating a master item
* _MasterItemColor
  * The HEX code to define the master items color. Must be in the format of "#000000"
* _MasterItemTags
  * A list of tags to be applied to the master item. tags should be listed using the ";" as a delimiter
* _MasterItemLabel
    * The label expression to be displayed on chart axis when using the master item (Qlik Sense September 2017 Onwards)
* _MasterItemExpression1
  * The Field name or expression for the measure or dimension
* _MasterItemExpression(2...n)
  * Additional fields, when required for a Drill-down Dimension should be added as extra columns using a sequential number in the field title
* _MasterItemNumberFormat
  * You can specify a number format in the form \<qType\>|\<qFmt\> (only works in master measures)  
  Valid options (combinations must match, so for example "D|$#,##0.00" won´t work)
    * qType:
    	* "U" - unknown (qFmt is ignored) 
    	* "F" - Numbers 
    	* "M" - Money
    	* "D" - Dates and Timestamps 
    	* "IV" - Interval (Time only) 
    	* "R" - Real numbers/user defined 
    * qFmt:
    	* "$#,##0.00;($#,##0.00)"
    	* "YYYY-MM-DD h:mm:ss[.fff]" 
    	* "h:mm:ss" 
    	* "0.00%" 
    	* ...other possible format strings

## Once Imported
When you have imported, the extension can be deleted, you can also remove the data table from your script too. If you need to update the master items, just load the extension again (if you have deleted it from the sheet) and update from the source data.

The master items will be updated based upon the _MasterItemID column.

There are no dependencies in your app for the extension, or when you share the application for the recipient server to have MasterScript installed. This is just used to importing master items.
