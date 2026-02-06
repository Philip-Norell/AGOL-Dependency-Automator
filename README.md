AGOL Dependency Automator

Purpose: 
        This script is designed to automate almost all the work involved in creating a comprehensive data lineage for AGOL content.
    Moreoever, this script also documents feature services that are not consumed by webmaps for the purposes of data governance. 
    Ouput data is visualized in a series of Excel sheets formatted as sortable dependency matrices. 

Method:
        There are two avenues of data capture in this script.    
    First, it compiles a dictionary of all webmaps in AGOL and parses their related JSONs to extract the services they depend upon. 
    Those services are then matched to a dictionary of feature services and feature classes, producing a dictionary structured like
    {webmap : {service : [feature classes]}}. This is then transformed into a pandas dataframe, transposed, and then written as a 
    formatted Excel sheet. Second, the same process is performed on a dictionary of experiences, creating a dictionary strucutred as 
    {experience : {webmap : {service : [feature classes]}}.

Inputs:
        This script takes inputs from two sources. The first is directly from Portal/AGOL via the ArcGIS API, and the second is a 
    manually created document detailing which feature classes services consume. The second document must be created and maintained 
    manually, but such maintenance will only be required infrequently due to how seldom feature classes (as well as referenced services)
    are added or removed from SDE. The creation process for the feature class input sheet is detailed in the documentation. 

Limitations: 
        This script does not capture which services experiences consume directly without a webmap intermediary.
    To my knowledge, this is possible but may be difficult. Therefore, since our standard practice is for experiences to only
    consume webmaps, I didn't deem this necessary. Furthermore, the orphan services sheet produced does not account for services
    drawn upon by solutions. 

Misc:
        The dictionary-building code chunks will often return error text along the lines of "Service (ID String) does not exist."
    These are deleted services that retain their itemID but have all attributes such as title and URL erased. If the ID is plugged 
    into a standard AGOL/Portal item URL, it will say the service is deleted or unavailable. 
