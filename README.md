# Jupyter-Notebook-Tunelling

### Quick Description

The following quick-guide follows a procedure which allows remote working with Jupyter notebooks, which are located on a **private remote host** inside the network of CERN. The procedure follows a process of ssh hops from the home computer (outside the network of CERN), to the lxplus via `username@lxplus.cern.ch` and to the private remote host. This method is mostly useful whenever there is no direct access via `ssh` from a network outside CERN, to the private node. 

# Variables
host_A : username@lxplus.cern.ch

host_B: username@private_host.cern.ch

port_number: The port number on which the local computer
# Commands
From the private remote server, which is assumed that it can be accessed from inside CERN network, initiate a Jupyter session from the directory of the desired notebook:

```bash
jupyter notebook --no-browser --port=$port_number
```

The --no-browser option is not mandatory but it will prevent Jupyter poping-up on the default browser. 

From the personal computer @ home, type in a terminal for the ***ssh tunel*** : 
  
```shell
ssh -L $port_number:localhost:$port_number $host_A ssh -L $port_number:localhost:$port_number -N $host_B
```
The tunel is from host_A to host_B. Note that this comes in handy in cases where there is no access to the remote private server from outside CERN, but there is from host_A to host_B.

The home computer will now listen to `port_number`. As a result, there will be access to the Jupyter enviroment of the private remote machine.

At home computer, open a browser, go to `localhost:$port_number`. Jupyter will prompt you to insert the token for accessing the remote directory and the notebook. For this step, go to the terminal where the Jupyter enviroment was initiated, copy the token number and paste it in the Jupyter token field at the home computer.

If everything went well, you can now work with the remote Jupyter notebook, while using also all the libraries that are loaded already @ the private remote machine, at your place outside CERN.

Happy coding :-) !
