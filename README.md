# SeisPos_Import
This is a QGIS plugin to import Seismic Positioning Data.
The file imports Seismic Navigation files (SPS, P1/11, P190 files). 

The following can be imported:
Receiver SPS
Source SPS
P190 S Records
P190 V Records
P190 E Records
P190 Custom Records Import (Custom Filter to be chosen - For example ^E for E records only)
P190 Preplot Import
P111 S Record Import
P111 Custom Record Import (Custom Filter to be chosen - For example ^P1 for P1 records)


Further more, each import has a schema associated which is available in schema folder. This schema file defines the data type for each of the fields and can be modified.

Schema for Seismic_Importer QGIS plugin 

 

 

The default schema files for Px/90, Px/11 and SPS files are installed with the plugin. However, these can be modified to suit any changes. 

 

## Accessing Schema files 

 

In QGIS menu, go to Settings->User Profiles -> Open Active Profile Folder as shown below: 

<img width="431" alt="Screenshot 2021-10-03 at 11 22 05 pm" src="https://user-images.githubusercontent.com/10369790/135773335-84274cc6-187d-42a4-8478-2dba2b1fe97c.png">


In the opened folder, go to python/plugins/seismic_importer 

These are the installation files of seismic_importer. Browse to schema/ folder. Here are all the schema files. 

**CAUTION**: When a schema file is changed, the plugin needs to be re-imported. This can be done by restarting QGIS or using another plugin called “Plugin Reloader”. Install it from QGIS plugins and reload SPS importer every time you change the schema file. 

 

## Modifying Schema files 

 

A sample schema file for SPS source looks like below: 
 
sourceSPSSchema.txt -

```#LineDirectionFrom should contain the name of the field with line direction, there should be a field with names X and Y 

schema:sourceSPS 

type:fixedWidth 

filter:^S 

LineDirectionFrom:pointnum 

field:Linename:2:17:str 

field:pointnum:18:22:int 

field:X:47:55:float 

field:Y:56:65:float 

field:code:27:28:str 

field:depth:41:46:float 

field:tide:66:71:float 

field:dayofyear:72:74:int 

field:time:75:80:str
```



You can use # to comment out any field. The mandatory fields are Linename, pointnum, X and Y. Rest of the fields can be commented out if not needed. 

Some common errors: 

- Field name is not in the provided SPS file – comment out that field and then import. 

- The field is float or int in schema, but is not importable as it contains letters 

- Change the field to str instead of int or float. (X and Y should be floats). 

- A field does not exist: Add a new field with the same syntax as below: 
field:[fieldname]:[firstColumn]:[lastColumn]:[type] 

Where fieldname = any name without spaces you want to call the field 

firstColumn, lastColumn = first and last columns.  
	type: can be int, str or float 

- Filter is used to remove any rows that you are not interested in. This is a standard regular expression. For example ˆS means any line starting with an S. 

 

