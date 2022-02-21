
![SailPoint](https://files.accessiq.sailpoint.com/modules/builds/static-assets/perpetual/sailpoint/logo/1.0/sailpoint_logo_color_228x50.png)

# IdentityNow Attribute Sync Simulator

Date: 2021-12-01

Author: Guillermo Fernández

## Overview
 
This tool is thought to be used as an IdentityNow pre-Go Live activity. The tool simply performs a simulation of the IdentityNow attribute synchronization process. As a reminder, IdentityNow attribute sync will push identity attributes values into account attribute values on the sources where this functionality is enabled. 

The tool takes as input data:

* Extracted CSV file from the source where attribute sync will be enabled.
* Extracted CSV file of Identity data from IdentityNow Search Engine.


The tool can work with any kind of IdentityNow source set of data but has been successfully tested with Active Directory and Workday.

Note: It is recommended to run aggregation on authoritative source and sources where attributes will be synchronized, before extract the CSV files. So, the tool will perform the simulation with the latest updated set of data.

This project has been developed with IntelliJ DEA (Community Edition) and it is a straightforward to import it directly in this development framework. You will only need to add the lib folder to the project class path. The lib folder includes all required libraries. 

 
## Release Notes
 
### Version 1.0

* Initial Release
 
This utility has limited support from SailPoint.  If you have any issues, bugs, or feature requests, please send them to <guillermo.fernandez@sailpoint.com>.


## Configuration
 
The configuration is done in a properties file (account_sync.properties). The project contains example input files and it is ready to be executed with this example set of data. The tool will search account_sync.properties file only. Other properties file has been provided as examples.

![alt text](https://github.com/guillermo-fernandez-sp/IDNAttSyncSimulator/blob/master/img/account_sync.properties.png?raw=true)



Some tips on how to extract the input files:

* inputFileNameIDN: 
1. Go to IdentityNow Search Engine.
2. Filter on Identity population that will be sync.
3. Columns to select are the correlation attribute and the attributes that will be synced.
4. Generate report.

![alt text](https://github.com/guillermo-fernandez-sp/IDNAttSyncSimulator/blob/master/img/inputFileNameIDN.png?raw=true)

* outputFileName
1. Go to Account section in the source where attribute synchronization will be enabled.
2. Extract CSV account report
3. Open the CSV file in MS Excel and remove duplicates selecting a column with a unique identifier (for example, distinguishedName in Active Directory sources). 

![alt text](https://github.com/guillermo-fernandez-sp/IDNAttSyncSimulator/blob/master/img/outputFileName.png?raw=true)

Once input files have been generated, just copy them into the input folder and update the file names in the account_sync.properties file. Output file name is also set in the properties file and will be placed in the output folder.

The tool also generates a log file called trace.log located in the log folder. Log setting can be configured in log4j.properties file, where INFO and DEBUG options are allowed. 

![alt text](https://github.com/guillermo-fernandez-sp/IDNAttSyncSimulator/blob/master/img/log.png?raw=true)


## Limitations

This tool works consuming both input files performing first a correlation process and then a comparison process on the selected attributes. Calculation time will directly depend on the size of the files and the computer resources, where it is executed. Below results took around 1 hour of execution time:

```

Total: 2775 identities in Active Directory
Total: 3065 identities in IdentityNow with attribute: EmployeeID provisioned
Total: 2715 Active Directory accounts found in IdentityNow
Total: 1678 attributes will be synchronized


```


