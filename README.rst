Geoengine
========================

(GeoEngine)EO Data Exploitation and Visualization Tool is a web based application developed with a goal
of providing new working techniques that ease data collection, access,
analysis and visualization. Collection of large EO datasets and analysis of
the data using the random forest algorithm is done on one front-end interface.
The proposed tool also integrates with Geoserver as a backend. EO Data Exploitation and Visualization Tool is a climate change analysisTool that utilizes pre-processed imagery to discover actionable insights. Climate change has greatly affected many countries across the globe and poses a big challenge in terms of strategic planning and sound decision-making processes. The solution will provide new working techniques that ease data collection, access, analysis and visualization. This will play a key role in analyzing satellite data and presenting the results to key stakeholders. EO Data Exploitation and Visualization Tool will consume Landsat-8 data and training areas shape files which will be used for the classification process. The proposed too will be used to analyze earth observation data of 30 m spatial resolution and a temporal resolution of 16 days. Data will loaded to the application using robust geoserver rest api endpoints that allow creating of workspaces, authentication and serving of both classified and unclassified images. Access to the classification tool will be available on the front-end ( using a very user-friendly interface) but, the process will run in the background. The analysis will produce classified Land Cover imagery which will be saved for current and future reference. Resolution of the outputs will also have a spatial resolution of 30m




Create a custom project
-----------------------

Note: You can call your geonode project whatever you like following the naming conventions for python packages (generally lower case with underscores (``_``). In the examples below, replace ``my_geonode`` with whatever you would like to name your project.

Using a Python virtual environment
++++++++++++++++++++++++++++++++++

To setup your project using a local python virtual environment, follow these instructions:

1. Prepare the Environment

  .. code:: bash

    git clone https://github.com/GeoNode/geonode-project.git -b 2.10.x
    mkvirtualenv my_geonode
    pip install Django==1.11.21

    django-admin startproject --template=./geonode-project -e py,rst,json,yml,ini,env,sample -n Dockerfile my_geonode

    cd my_geonode

2. Setup the Python Dependencies

  .. code:: bash

    pip install -r requirements.txt --upgrade
    pip install -e . --upgrade

    GDAL_VERSION=`gdal-config --version`
    PYGDAL_VERSION="$(pip install pygdal==$GDAL_VERSION 2>&1 | grep -oP '(?<=: )(.*)(?=\))' | grep -oh $GDAL_VERSION\.[0-9])"
    pip install pygdal==$PYGDAL_VERSION

    # Using Default Settings
    DJANGO_SETTINGS_MODULE=my_geonode.settings paver reset
    DJANGO_SETTINGS_MODULE=my_geonode.settings paver setup
    DJANGO_SETTINGS_MODULE=my_geonode.settings paver sync
    DJANGO_SETTINGS_MODULE=my_geonode.settings paver start

    # Using Custom Local Settings
    cp my_geonode/local_settings.py.sample my_geonode/local_settings.py

    vim my_geonode/wsgi.py
    --> os.environ.setdefault("DJANGO_SETTINGS_MODULE", "my_geonode.local_settings")

    DJANGO_SETTINGS_MODULE=my_geonode.local_settings paver reset
    DJANGO_SETTINGS_MODULE=my_geonode.local_settings paver setup
    DJANGO_SETTINGS_MODULE=my_geonode.local_settings paver sync
    DJANGO_SETTINGS_MODULE=my_geonode.local_settings paver start

3. Access GeoEngine from browser::

    http://localhost:8000/

.. note:: default admin user is ``admin`` (with pw: ``admin``)

Start your server
-----------------

You need Docker 1.12 or higher, get the latest stable official release for your platform.

1. Prepare the Environment

  .. code:: bash

    git clone https://github.com/GeoNode/geonode-project.git -b 2.10.x
    mkvirtualenv my_geonode
    pip install Django==1.11.21

    django-admin startproject --template=./geonode-project -e py,rst,json,yml,ini,env,sample -n Dockerfile my_geonode

    cd my_geonode




Recommended: Track your changes
-------------------------------

Step 1. Install Git (for Linux, Mac or Windows).

Step 2. Init git locally and do the first commit:

    git init

    git add *

    git commit -m "Initial Commit"

Step 3. Set up a free account on github or bitbucket and make a copy of the repo there.

Hints: Configuring Requirements.txt
-----------------------------------

You may want to configure your requirements.txt, if you are using additional or custom versions of python packages.  For example::

    Django==1.11.21
    six==1.10.0
    django-cuser==2017.3.16
    django-model-utils==3.1.1
    pyshp==1.2.12
    celery==4.1.0
    Shapely>=1.5.13,<1.6.dev0
    proj==0.1.0
    pyproj==1.9.5.1
    pygdal==2.2.1.3
    inflection==0.3.1
    git+git://github.com/<your organization>/geonode.git@<your branch>


Hints: Using Ansible
--------------------

You will need to use Ansible Role in order to run the playbook.

In order to install and setup Ansible, run the following commands::

    sudo apt-get install software-properties-common
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get install ansible

A sample Ansible Role can be found at https://github.com/GeoNode/ansible-geonode

To install the default one, run::

    sudo ansible-galaxy install GeoNode.geonode

you will find the Ansible files into the ``~/.ansible/roles`` folder. Those must be updated in order to match the GeoNode and GeoServer versions you will need to install.

To run the Ansible playbook use something like this::

    ANSIBLE_ROLES_PATH=~.ansible/roles ansible-playbook -e "gs_root_password=<new gs root password>" -e "gs_admin_password=<new gs admin password>" -e "dj_superuser_password=<new django admin password>" -i inventory --limit all playbook.yml


Configuration
=============
