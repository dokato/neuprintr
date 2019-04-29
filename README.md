<!-- README.md is generated from README.Rmd. Please edit that file -->
[![Travis-CI Build Status](https://api.travis-ci.org/jefferislab/neuprintr.svg?branch=master)](https://travis-ci.org/jefferislab/neuprintr) [![Docs](https://img.shields.io/badge/docs-100%25-brightgreen.svg)](http://jefferislab.github.io/neuromorphr/reference/)

neuprintr
=========

The goal of *neuprintr* is to provide R client utilities for interacting with the neuPrint connectome analysis service. neuPrint is set of tools for loading and analysing connectome data into a Neo4j database. You can find [neuprint](https://github.com/connectome-neuprint/neuPrint) on Github. There is also a great python client available from Philipp Schlegel, [neuprint-python](https://github.com/schlegelp/neuprint-python) if that's your thing. neuPrint is currently being used for connectome analysis in aid of neuronal reconstruction efforts at Janelia Research Campus. Using this R package in concert with the [nat](https://github.com/jefferis/nat) ecosystem developed primarily by Greg Jefferis is highly recommended.

Installation
------------

``` r
# install
if (!require("devtools")) install.packages("devtools")
devtools::install_github("jefferislab/neuprintr")

# use 
library(neuprintr)
```

Authentication
--------------

In order to use *neuprintr* you will need to be able to login to a neuPrint server and be able to access it underlying Neo4j database. Currently this means you have to be on the network, SECURE WiFi or have a VPN for the Janelia network, and have an authorised account.

![access your bearer token](https://raw.githubusercontent.com/jefferislab/neuprintr/master/inst/images/bearertoken.png)

To make life easier, you can then edit your R.environ file to contain information about the neuPrint server you want to speak with, your token and the dataset hosted by that server, that you want to read. For detailed instructions use:

``` r
?neuprint_login
```

To get started quickly, all you need to do is

``` r
conn = neuprint_login(server= "https://emdata1.int.janelia.org:11000",
   token= "asBatEsiOIJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImIsImxldmVsIjoicmVhZHdyaXRlIiwiaW1hZ2UtdXJsIjoiaHR0cHM7Ly9saDQuZ29vZ2xldXNlcmNvbnRlbnQuY29tLy1QeFVrTFZtbHdmcy9BQUFBQUFBQUFBDD9BQUFBQUFBQUFBQS9BQ0hpM3JleFZMeEI4Nl9FT1asb0dyMnV0QjJBcFJSZlI6MTczMjc1MjU2HH0.jhh1nMDBPl5A1HYKcszXM518NZeAhZG9jKy3hzVOWEU")
# nb this token is a dummy
```

Example
-------

Now we can have a look at what is available

``` r
# What data sets are available?
neuprint_datasets()

# What's the underlying database
neuprint_database()

# What are the regions of interrst in your default datasest (specified in R.environ, see ?neuprint_login)
neuprint_ROIs()
```

Use the client to request data from neuprint. The method will run an arbitrary cypher query against the database. For information about the neuprint data model, see the neuprint explorer web help: <https://emdata1.int.janelia.org:11000/help>.

Some cyphers and other API endpoints have been explored by this package. Have a look a the functions, for example, that give you neuron skeletons, synapse locations, connectivity matrices, etc.

``` r
?neuprint_get_adjacency_matrix
?neuprint_ROI_connectivity
?neuprint_get_synapses
?neuprint_read_neurons
```
