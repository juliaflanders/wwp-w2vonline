# Women Writers Vector Tool

This repository is the code base for the Women Writers Vector Tool, a Shiny application for exploring word vector models. The app includes the models generated from the Women Writers Online collection.

## Running the application

To run the Shiny app on your own machine, you’ll need R, a programming language available at <https://www.r-project.org/>.

### Getting the code

You’ll also need a copy of the code from this GitHub repository.

The simplest method for obtaining the code is also the simplest way of running the app. In an R console or in RStudio’s console, install the “shiny” package, then use it to run the application via GitHub.

	install.packages("shiny")
	library(shiny)
	runGitHub("wwp-w2vonline", "NEU-DSG", ref="with-selector")

If you plan to do any customization of the code, you should instead download the code yourself.

If you do plan to make edits, and want to put those edits under version control, you can clone the repository in the command line.

	git clone --branch with-selector https://github.com/NEU-DSG/wwp-w2vonline.git

Alternatively, you can download and decompress this file: <https://github.com/NEU-DSG/wwp-w2vonline/archive/with-selector.zip>.


### Running a local copy with RStudio

Open RStudio and make sure the following packages are installed:

* “shiny”
* “shinyjs”
* “magrittr”
* “DT”
* “rjson”
* “tidyverse” (this package has a lot of dependencies and will take a long time to install)
* Benjamin Schmidt’s “wordVectors”, available at <https://github.com/bmschmidt/wordVectors>

With the exception of “wordVectors”, these libraries are available on the Comprehensive R Archive Network (CRAN) and can be downloaded by running the following in RStudio’s console window:

	install.packages(c("shiny", "shinyjs", "magrittr", "DT", "rjson", "tidyverse"))

To install “wordVectors”, first install and load “devtools”.

	install.packages("devtools")

If “devtools” installed successfully, use it to install “wordVectors” from GitHub.

	library("devtools")
	devtools::install_github("bmschmidt/wordVectors")

**Note:** If “devtools” won’t install, use the “remotes” package instead.

	install.packages("remotes")
	library("remotes")
	remotes::install_github("bmschmidt/wordVectors")

With the required libraries present, you can simply open `app.R`, and select the “Run App” button in RStudio’s editor pane. The application will open in a separate window by default.

### Publishing to Shinyapps.io

*I haven’t done this part myself, but [the instructions](http://shiny.rstudio.com/articles/shinyapps.html) seem pretty straightforward.*


## Customizing the application

When run, the Women Writers Vector Tool will read in models from the “data” folder, and make them available for querying. Models are only published, however, if (1) they have a corresponding entry in the catalog [“data/wwoToolKit\_catalog\_json.json”](https://github.com/NEU-DSG/wwp-w2vonline/blob/with-selector/data/wwoToolKit_catalog_json.json), and (2) that entry is marked “public”.

To add your own pre-generated model(s), place them in the “data” directory. Then edit “data/wwoToolKit\_catalog\_json.json”. Here's a sample entry:

	"WWO Corpus": {
		"shortName": "WWO Corpus",
		"location": "data/wwo_xquery-nonreg_allTexts.bin",
		"shortDescription" : "All texts from the WWO",
		"public" : "true",
		"description": "This is the entire corpus of the WWO. Texts have been prepared using XSLT and XQuery processes that clean and regularize the corpus."
	}

Each model in the catalog has a descriptive “short name”, which is used to populate the dropdown menu of queryable models. The “location” field gives a relative filepath to the model’s BIN file. The two description fields can be left as empty strings, since they aren’t yet in use. Finally, the “public” field is marked “true” (if the model should be published in the browser), or “false” (if the model should not be published).

To add your own entries to the catalog, follow the template above, making sure to separate entries with commas. You may also want to change which of the existing models are published to the Tool interface.
