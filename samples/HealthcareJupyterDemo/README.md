# Healthcare Python Streaming Application Demo
This application demonstrates how users can develop Python Streaming Applications from a Jupyter Notebook. The Jupyter Notebook ultimately submits two Streams applications to a local Streams cluster. The first application is a pre-compiled SPL application that simulates patient waveform and vital data, as well as publishes the data to a topic. The second application is a Python Topology application written using the Streams Python API. This application subscribes to the topic containing the patient data, performs analysis on the waveforms and sends all of the data, including the results of the analysis, to the Streams view server.

Submitting the Python application from the Notebook allows for connecting to the Streams view server in order to retrieve the data. Once the data has been retrieved, it can be analyzed, manipulated or visualized like any other data accessed from a notebook. In the case of this demo, waveform graphs and numerical widgets are being used to display the healthcare data of the patient. 

This sample is built using the [BioSPPy](http://biosppy.readthedocs.io/en/stable/) Signal Processing Libraries.

The following diagram outlines the architecture of the demo.  

![Demo Architecture](images/architecture_diagram.jpg)

## VM Image Setup

  1. Download Anaconda 3.5 and install. Allow Anaconda to update your .bashrc. You will also need
  to update the version of the Bokeh library installed

      ```
      wget https://repo.continuum.io/archive/Anaconda3-4.1.1-Linux-x86_64.sh
      bash Anaconda3-4.1.1-Linux-x86_64.sh
      conda install bokeh
      ```

  2. Setup the .bashrc to point to the Python install directory and the topology toolkit python packages.
  The Topology Toolkit is included as part of the demo package so there is no need to download from GitHub.
  Also, make sure to set the LD_LIBRARY_PATH, otherwise the python app will not run.

      Set the following in .bashrc:

      ```
      export PYTHONPATH=/home/streamsadmin/HealthcareJupyterDemo/ext/streamsx.topology/com.ibm.streamsx.topology/opt/python/packages:/home/streamsadmin/HealthcareJupyterDemo/ext/biosppy_streaming
      export LD_LIBRARY_PATH=/home/streamsadmin/anaconda3/lib
      ```

  3. Restart the domain and instance to pickup the new environment variables

      ```
      source ~/.bashrc
      st stopinstance
      st stopdomain
      st startdomain
      st startinstance
      ```

  5. In the home directory, clone the git repository, navigate to *streamsx.health/samples/HealthcareJupyterDemo* and run `ant` to build the demo for your platform (< 5 minutes):

      ```
      git clone <repo>
      cd /home/streamsadmin/streamsx.health/samples/HealthcareJupyterDemo
      ant
      ```

  6. Start the Jupyter notebook from *streamsx.ecgdemo/samples/HealthcareJupyterDemo*:

      ```
      ./start.sh
      ```

  7. In the web browser, open the *notebooks/HealthcareDemo.pynb* notebook

  8. Run each cell individually. The following graphs should be displayed and updating in real-time. 

    ![Screen capture of Healthcare Demo](images/Healthcare_Demo.png "Screen capture of Healthcare Demo")

  9. If the graphs do not appear, verify that the Streams applications are running (and tuples are flowing) by opening the [Streams Console](https://localhost:8443/streams/domain/console#application/dashboard/Application%20Dashboard)
