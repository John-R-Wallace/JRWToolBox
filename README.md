R-ToolBox
============================

Prologue

Any csv file, script (of any kind), or R fucntion, including those in this toolbox can be individually downloaded using the function gitAFile() found in this toolbox. (Which could intially be copied from the 'R' directory here and pasted into R.)

For example use:

    gitAFile('https://raw.githubusercontent.com/John-R-Wallace/R-ToolBox/master/R/lib.R') 
    # lib() is saved to .GlobalEnv

to download just the lib() function which replaces the two step process of install.packages('foo'); library(foo) with just one step: lib(foo).  If the foo package is already installed, then lib(foo) will only do library(foo), hence lib(foo) is all that is needed when installing and/or loading a package from CRAN.

Note, for the use of a raw GitHub URL see: http://rawgit.com/

Install or upgrade the package with:

    # Get devtools if you don't already have it.
    if (!any(installed.packages()[, 1] %in% "devtools"))  install.packages('devtools')  
    
    devtools::install_github("John-R-Wallace/JRWToolBox")

If you then want to load the package into R use:

    library(JRWToolBox)    

============================   
Highlights and Comments

The function lib() will install and update both GitHub and CRAN packages only if needed and regardless will load the package into the R session, if require = TRUE (the default).

Code to put on the top of a function to start using lib() and other functions in JRWToolBox would look like:

    if (!any(installed.packages()[, 1] %in% "devtools"))  install.packages('devtools')  
	
	devtools::install_github("John-R-Wallace/JRWToolBox", quiet = T)
	if (!any(installed.packages()[, 1] %in% "JRWToolBox"))
	    stop('JRWToolBox is not installed, an attempt to install failed (check for internet access)')
    require(JRWToolBox)
     
    # Examples 
    lib("John-R-Wallace/Imap") # GitHub
    lib(plyr) # CRAN

- %ino% preserves the order when using matching operators unlike %in%.  See my entry in Stack Overflow:
https://stackoverflow.com/questions/10586652/r-preserve-order-when-using-matching-operators-in


- gitHub_SHA() shows the current (full) SHA for a given repo.  A call is also given that can be used to revert to that commit in the future. Saving these calls for each relevant package with your current code insures you are using the commits that your code works with and that your results are reproducible. The date and call are also invisibly returned and hence can be used to install the commit at any time in the future:
      
      JRWToolBox.Commit <- gitHub_SHA("John-R-Wallace/R-ToolBox")

      SHA: a5820d8c1bc0b62e523440b847e027a8af655f81 from reference: master

      Current date and time and the call to revert to this Commit in the future:

      2017-11-17 14:29:23
      devtools::install_github('John-R-Wallace/R-ToolBox', ref = 'a5820d8c1bc0b62e523440b847e027a8af655f81')


      JRWToolBox.Commit
      $Date
      [1] "2017-11-17 14:29:23 PST"

      $Call
      [1] "devtools::install_github('John-R-Wallace/R-ToolBox', ref = 'a5820d8c1bc0b62e523440b847e027a8af655f81')"


      eval(parse(text = JRWToolBox.Commit$Call))
      Downloading GitHub repo John-R-Wallace/R-ToolBox@a5820d8c1bc0b62e523440b847e027a8af655f81 ...
      
      packageDescription('Imap')$RemoteSHA

============================   
All functions were written by me except for (this list is under construction):

- xlsxToR: Substantial fix and value added changes; see the fork off of xlsxToR: https://gist.github.com/John-R-Wallace/3eab07a93877e87ec968
- mvnorm, dmulti.norm, Inside.polygon, inside.xypolygon, & verify.xypolygon: submissions to various Splus user group website(s)
- Some panel.XX functions are value added versions from the ones in the lattice package, however panel.chull, panel.chull.2.peels, & panel.conf.pred.band are mine.
- ll() is value added from a function by Arni Magnusson found in the package 'gdata'.
- Symbols is an old version of pchShow given in the help of the points function.
 
   
Comments on functions:

- Ls() is a replacement for ls() to avoid seeing all the quotes on the object names.
- dir.use() is a wrapper function which creates a path of sub-directory given, if it doesn't already exist and then returns the      path: some.function(..., path = dir.use('c:/create_this_path_if_needed')
- showObject() shows an R object in an editor, edit the function to change the default editor for ease of use.
