# ESS Data Formats #

Twenty years ago, there were a large number of disparate formats for storing large data sets, and the transfer of data from one computing system to another was a big deal, often relying on frequent playing of the "find-the-continents" game.  Now, however, there are two general styles of dataset storage: 1) machine-independent self-documenting gridded datasets, and 2) relational data bases (e.g. MS Access, mySQL) (with common Excel formats (.csv, .xlsx) as special cases of database tables).  Gridded data sets are chiefly represented by the netCDF and HDF5 formats, which include self-documenting "attribute" data, with an older "binary" data format (GRIB2) still in widespread use for exachanging real-time weather forecasting data, and there is growing "interoperatability" among these formats.  Databases are in widespread use for storing data that may be heterogeneous in the sense of not being gridded, and possibly having multiple tables.

## netCDF ## 

netCDF (or Network Common Data Format) is the format most frequently used for storing climate-model output as well as some observational data.  There is a well-documented convention (CF, for Climate-and-Forecast) for arranging and internally documenting netCDF datasets, which further contributes to simple transfer of data from one system to another. 

- netCDF:  http://www.unidata.ucar.edu/software/netcdf/docs/index.html
- CF Conventions:  http://cfconventions.org/

There are several R packages for handling netCDF data.  Of these, the `ncdf4` and the related `ncdf.helpers` packages are the most useful in practice.

- ncdf4:  https://cloud.r-project.org/web/packages/ncdf4/index.html
- ncdf.helpers:  https://cloud.r-project.org/web/packages/ncdf4.helpers/index.html

## HDF ## 

HDF (or Hierarchical Data Format), like netCDF is a machine-independent self-documenting gridded dataset format, that is in common use for storing satellite and remote-sensing imagery data.  It currently exists in several formats (HDF4, HDF5, HDF-EOS) which can generally converted to one another.  (netCDF4 in fact uses the HDF5 format for storing data.)

- HDF:  https://www.hdfgroup.org/
- HDF Tools:  https://support.hdfgroup.org/tools/ (including conversion tools)
- HDFView:  https://support.hdfgroup.org/products/java/hdfview/ (and HDF viewer, but not as powerful as Panoply)
- HDF5 R tutorials:  http://neondataskills.org/HDF5/ 

Reading and writing HDF5 files in R is supported by the `rhdf5` package in the Bioconductor collection:

- rhdf5:  http://bioconductor.org/packages/release/bioc/html/rhdf5.html

The National Snow and Ice Data Center (NSIDC) as a nice tutorial on HDF-EOS:  [https://nsidc.org/data/hdfeos/intro.html](https://nsidc.org/data/hdfeos/intro.html)

NOAA's Coral Reef Watch [http://www.coralreefwatch.noaa.gov/satellite/hdf/index.php](http://www.coralreefwatch.noaa.gov/satellite/hdf/index.php) serves up a variety of HDF files for coral-bleaching monitoring.

## GRIB ##

GRIB (or GRIdded Binary / General Regularly-distributed Information in Binary form, https://en.wikipedia.org/wiki/GRIB)

- GRIB:  http://www.nco.ncep.noaa.gov/pmb/docs/grib2/grib2_doc.shtml 


## Relational Data Bases ##

Relational databases can be thought of as a set of linked tables that efficiently store data that, if stored as a single rectangular table would be inefficiently large and difficult to extract data from.  Nevertheless, there are multiple ESS data sets, usually collections of site-specific data (where the sites are irregularly distributed) that can be efficiently stored and queried

An example ESS dataset stored as a relational database:

- Global Charcoal Database:  http://paleofire.org/
- Analyzing the GCDv3:  http://geog.uoregon.edu/bartlein/GPWG/GPWGAnalysis/index.html

The gridded dataset formats described above are sometimes referred to as nonSQL databases, for the simple reason that they are not SQL databased (where SQL (pronounced "sequel") stands for Structured Query Language). The distinction between the two is described here:

- SQL:  https://en.wikipedia.org/wiki/SQL
- nonSQL:  https://en.wikipedia.org/wiki/NoSQL


# Getting, Reading and Displaying ESS Datasets #

## Panoply ##

Panoply is cross-platform application that can read and display netCDF, HDF and GRIB datasets.  See [Other Information](install_Panoply.html) on this web page for directions for installing Panoply.

## FTP ##

FTP (for File Transfer Protocol) is a now pretty-old traditional way of moving data around.  In its standard form, it's not very secrure (and hence IT service hate it), but it's still quite functional.  An ftp "site" has been created for this course, on a server here called "climate".  Here are the details -- host name:  climate.uoregon.edu  user name:  geog490user  password: (displayed in class).

The most widely used "client" for interacting with ftp sites is likely Filezilla [https://filezilla-project.org/](https://filezilla-project.org/)

## THREDDS and OPeNDAP ##

THREDDS (Thematic Real-time Environmental Distributed Data Services) Data Servers (TDS) provide a mechanism for making remote datasets (generally netCDF datasets) "visible" to local applications (like Panoply).  TDS display "catalogs" of multiple files that can, for example, be browsed by Panoply, and individual data sets can then be opened.  OPeNDAP provides a further mechanism for subsetting data sets, i.e. selecting an individual slice from a 3d or 4d data set.  Both THREDDS and OPeNDAP thus provide a way of avoiding downloading and storing data locally.  (Once data are downloaded to a local machine, they are in a sense "frozen".  By not storing datasets locally, and instead accessing them remotely, any updates are automatically included. 

THREDDS:  http://www.unidata.ucar.edu/software/thredds/current/tds/dd
OPeNDAP:  https://www.opendap.org/

Here is a local example of THREDDS-served data:

- USGS at OSU Regclim THREDDS catalog:  http://regclim.coas.oregonstate.edu:8080/thredds/catalog.html

# Some ESS Data Sources #

## Climate-model output ##

CMIP5 is the climate-modeling component of the IPCC AR5 assessment, and nearly all of the data are available online through the ESG (Earth System Grid).  Additional climate-simulation data are available from the National Center for Atmospheric Research (NCAR).

CMIP5: https://pcmdi.llnl.gov/search/esgf-llnl/ 
NCAR:  https://www.earthsystemgrid.org/home.html

## NOAA ESRL PSD ##

The NOAA Earth System Research Laboratory (formerly the Climate Diagnostics Center, CDC) provides an array of gridded data sets, both historical and observational, including the historical "reanalysis" data sets.

NOAA ESRL PSD: http://www.esrl.noaa.gov/psd/
THREDDS catalog:  http://www.esrl.noaa.gov/psd/thredds/catalog.html
OPenDAP:  http://www.esrl.noaa.gov/psd/data/gridded/using_dods.html

## Paleoclimatic datasets ##

There are two main repositories of paleoclimatic data, Pangaea (European) and NOAA Paleoclimatology:

- Pangaea:  https://www.pangaea.de/
- NOAA WDS Paleoclimatology:  https://www.ncdc.noaa.gov/data-access/paleoclimatology-data

Other sources of paleoclimatic data include:

- Neotoma: http://www.neotomadb.org/  

## General global-change data ##

- NASA Global Change Master Directory [http://gcmd.nasa.gov/](http://gcmd.nasa.gov/)

## Some "Big Data" initiatives ##

ICSU World Data System:  https://www.icsu-wds.org/
SciDataCon:  http://www.scidatacon.org/site/about/

EarthCube:  https://www.earthcube.org/ 
EarthCube netCDF:  https://www.earthcube.org/group/advancing-netcdf-cf


