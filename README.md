# ADQL
ADQL

0) Use the FITS file of the survey or create your own file, 
Include the 2MASS designation and the target ID of the survey, add a header with the column names, e.g.:

# APOGEE_ID, 2MASS_ID
2M00000002+7417074, 00000002+7417074

1) Go to the GAIA archive and SIGN IN 
(top right corner, this is important for uploading data and storage limits), my username is ‘sbuder’.

2) Then go to SEARCH, ADQL FORM and click on the button ‘Upload user table’ and upload your table as ASCII 
Remember the name you gave it (I choose ’ness’ for the following example). 
It should then appear in the bottom of the left tree under User tables:
user_sbuder.ness with one column ‘apogee_id'

3) QUERY and only get the columns from gaia/tmass than you want - 
in this example I am really only selecting the first 10 results of your input apogee_id and the gaia soruce_id:

SELECT TOP 10 ness.apogee_id, gaia.source_id
FROM gaiadr1.gaia_source AS gaia
INNER JOIN gaiadr1.tmass_best_neighbour AS xmatch
	ON gaia.source_id = xmatch.source_id
INNER JOIN gaiadr1.tmass_original_valid AS tmass
	ON tmass.tmass_oid = xmatch.tmass_oid
INNER JOIN user_sbuder.ness AS ness
	ON tmass.designation = ness.apogee_id

However, the sky is the limit, so you can as easily also just use 'SELECT *’ 
and run that to get all results and all columns of your input file, GAIA and 2MASS.

The Job will get a telephone number and will be shown in the bottom of the server
You can also change the name e.g. into 'APOGEE_GAIA X-match’ in case you plan to submit more jobs. 
Once it is finished (indicated by an arrow on the left), you can either just continue within the server to show data.
You can also select this job, change the download format e.g. to FITS and click on the button ‘Download results’ on the right hand side.

![alt text](ADQL_overview.png "Screenshot of Gaia archive")