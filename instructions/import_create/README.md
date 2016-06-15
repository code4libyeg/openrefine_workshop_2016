###Create New Project in OpenRefine

A few options are available to import dataset into OpenRefine. You can import files in formats including:
  * TSV/CSV, or other values separated by a custom separator you specify 
  * Excel files (.xls, xlsx)
  * XML, RDF as XML
  * JSON
  * Google Spreadsheets in your Google Drive (requires you to authorize)
  * RDF N3 triples

 ![Create a project with Open Refine](../screenshots/create_project.png "Create Project")

 
You can also create new project by importing an archive file (with extension .zip, .tar.gz, .tgz, .tar.bz2, .gz or .bz2), OpenRefine detects the most common file extension in it and loads all files with that extension into a single project. This can be used to import an existing Refine project from another instance. 

Once imported, the data is stored in OpenRefine's own format, and the original data file is left undisturbed.

####To import data for the workshop (import an existing OpenRefine project)
  * download the compressed file from: https://github.com/code4libyeg/openrefine_workshop_2016/blob/master/Data/Peel-Postcards-and-Maps-16-paths.openrefine.tar.gz
  * Click 'Import Project'
  * upload the file you just downloaded in the following screen 

 ![Import project with Open Refine](../screenshots/import_project.png "Import Project")

  * You can rename the project if you like
  * Click 'Import Project' to proceed. The project should appear with full history from previous work on that project.  

####To import data from other format
  * Click 'Create Project'
  * Choose to upload from a local file or a file available online (use the Web Addresses option).

####To import data from an API call
  * Click 'Create Project'
  * Choose 'Web Addresses (URLs)'
  * Paste in your API call URL to the address box and click 'Next'
    eg: An API request to Google Places to search places of type "food" within 200 meter radius of University of Alberta:  https://maps.googleapis.com/maps/api/place/nearbysearch/json?location=53.5235571,-113.5239325&radius=200&types=food&key=AIzaSyD-aV4ZDVgfqqNMC78UiKjpp65VOOmGrDM
    

Depending on the type of data, you will need to choose a 'record' delimiter field. OpenRefine uses this to create the records/rows tabular output. 
  ![Specify Record Delimiter](../screenshots/parse_data.png "Record Parsing") 

