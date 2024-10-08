Welcome to urbanpy's documentation!
===================================

**A library to download, process and visualize high resolution urban
data in an easy and fast way.**

UrbanPy is an open source project to automate data extraction,
measurement, and visualization of urban accessibility metrics.

Functional goals
----------------

-  [x] Download open source spatial data (Limits & Points of Interests)
-  [x] Allow for the use of a grid system or administrative boundaries
   as spatial units
-  [x] Origin-destination matrix calculation by any mode using a routing
   API
-  [x] Obtain travel time from spatial units to the closest facilities
-  [x] Consolidate the results as tables and/or shapefiles (georeferenced datasets)
-  [x] Visualise the results as maps

UX goals
--------

-  [ ] Atomic functions (one purpose per function)
-  [x] Use the power of Python Geospatial Ecosystem under the hood
-  [x] Allow to flexible processing pipelines (custom layer/metrics
   aggregations)
-  [x] Clear documentation with usage and examples
-  [x] Clear and replicable example notebooks

Main modules
------------

-  download: Main functions for data download from Nominatin API,
   OverPass API and HDX population data
-  geom: Spatial operations, grid partitioning, spatial filtering and
   street network statistics
-  plotting: Visualization wrappers for plotly interactive choropleth
   maps
-  routing: Distance matrix computations (may require your own API keys)
-  utils: Data handling helpers

Installation
------------

For users
~~~~~~~~~

To install the urbanpy library you can use:

.. code:: sh

    $ pip install urbanpy

Then use ``import urbanpy`` in your python scripts to use the library.

If you plan to use the `OSRM Server <http://project-osrm.org/>`__ route
or distance matrix calculation functionalities\* you must have Docker
installed in your system, refer to Docker
`Installation <https://www.docker.com/products/docker-desktop>`__.

Additional Dependecies Notes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  It is important to note that for travel time computation, if needed,
   a method is implements the Open Source Routing Machine (OSRM). This
   method pulls, extracts and adds graph weights to the downloaded
   network and runs the routing server. Make sure to have docker
   installed for the library to work correctly.

-  Urbanpy provides a simple approximation with nearest neighbor search
   using a BallTree and haversine distance, but the difference between
   real travel time and the approximation may vary from city to city.

-  Additionally, the use of spatial libraries like osmnx, geopandas and
   h3 require certain extra packages. Specifically, for rtree (spatial
   indexing to allow spatial joins) libspatialindex is required. OSMnx
   and Geopandas requiere GDAL as well. If not handled by installing
   geopandas's dependencies, installing fiona, pyproj and shapely should
   satisfy the requirements. Another way to ensure all dependencies are
   met, installing osmnx via conda should suffice. H3 requires cc, make,
   and cmake in your $PATH when installing, otherwise installation will
   not be successful. Please refer to `h3's
   documentation <https://github.com/uber/h3>`__ for a more detailed
   guide on installation options and requirements.

Examples
~~~~~~~~

UrbanPy lets you download and visualize city boundaries extremely easy:

.. code:: python

    import urbanpy as up

    boundaries = up.download.nominatim_osm('Lima, Peru', expected_position=2)
    boundaries.plot()

Since ``boundaries`` is a GeoDataFrame it can be easily plotted with the
method ``.plot()``. You can also generate hexagons to fill the city
boundaries in a oneliner.

.. code:: python

    hexs, hexs_centroids = up.geom.gen_hexagons(resolution=9, city=boundaries)

Also check our `example notebooks </notebooks>`__, and if you have
examples or visualizations of your own, we encourage you to share
contribute.

For developers
~~~~~~~~~~~~~~

If you plan to contribute or customize urbanpy first clone this repo and
cd into it. Then, we strongly recommend you to create a virtual
environment. You can use conda, this installation manage some
complicated C spatial library dependencies:

.. code:: sh

    $ conda env create -n urbanpy -f environment.yml python=3.6
    $ conda activate urbanpy

Or if you are more confident about your setup, you can use pip:

.. code:: sh

    $ python3 -m venv .env
    $ source .env/bin/activate
    (.env) $ pip install -r requirements.txt


Authors
-------

UrbanPy's original authors are Claudio Ortega
(`socials <https://www.linkedin.com/in/claudioortega27/>`__) and Andrés
Regal (`socials <https://www.linkedin.com/in/andrés-regal/>`__).

\*Current support is tested on Linux Ubuntu 18.04 & Mac OS Catalina,
coming soon we will test and support Windows 10.

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


.. toctree::
   :caption: Table of Contents
   :maxdepth: 4

   usage/installation
   usage/quickstart
   urbanpy
   license
   contributing
   code_of_conduct
