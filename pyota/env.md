# PYOTA

For those new to Python, here are tips for installing [PYOTA](https://github.com/iotaledger/iota.lib.py), the Python API for IOTA

## Environment

PyOTA is compatible with Python 3.6, 3.5, and 2.7.  For this example, PYOTA will be installed on Ubuntu 18.04 LTS, also called Bionic Beaver.  Python 3.6.5 will be used; however, both Python 2.7 and Python 3.6.5 come pre-installed along with pip 9.0.1.  By default, pip points to Python 2.7 at: /usr/lib/python2.7/dist-packages

### Installing pip3 ###

One easy way to keep track of which python version is being used, is to install pip3.  Thus, ```pip``` points to Python 2.7 and ```pip3``` points to Python 3.6.5.  To install pip3:

```sudo apt install python3-pip ```

### Install git ###

Git doesn't come installed by default.  In order to install PYOTA from source, git must be installed so the repo (repository) can be copied or "cloned"

```sudo apt install git```


## Installing PYOTA from Source ##

Assumptions:
- Clean Ubuntu 18.04 LTS install
- Python3 plus pip3
- Virtual environment in a folder called ```python-VE```

### Create [virtual environment](https://realpython.com/python-virtual-environments-a-primer/) ###

Virtual environments are used to isolate python projects.  First, install the python 3 venv.  Next, make a folder called ```python-VE```.  Create the virtual environment and activate it. 

```
sudo apt-get install python3-venv
mkdir python -VE && cd python-VE
sudo python3 -m venv env
source env/bin/activate			
```

Use ```deactivate``` to leave the virtual environment

### Clone PYOTA ###

```git clone https://github.com/iotaledger/iota.lib.py.git```

This will copy PYOTA to a folder called ```iota-lib-py```

```
cd iota-lib-py
pip install -e .
```

** NOTICE:  remember to add the period (.) at the end of this command **

### Run Unit Tests (optional) ###

To fully test the installation, run unit tests:

``` sudo python3 setup.py test ```


### Run hello_world.py ###

Hello_world.py will connect to an IOTA node and print node statistics such as name, version, neighbours, and milestones.  

#### Additional Installs and Upgrades ####

From your home directory install the ```requests``` module

```sudo apt-get install python3-requests```

Update the [cryptography](https://cryptography.io/en/latest/installation/) module so the version is >=2.2.1

```pip3 install cryptography```

#### Select IRI Node ####

The default node is ```localhost:14265```.  Override this by executing hello_world.py with the ```--uri``` flag plus the address of your node.  For example, to access the Devnet Tangle use, https://nodes.devnet.iota.org:443 as shown below:

```sudo python3 examples/hello_world.py --uri https://nodes.devnet.iota.org:443```

Here are the results:

```
Hello https://nodes.devnet.iota.org:443!
{'appName': 'IRI Testnet',
 'appVersion': '1.5.5',
 'duration': 0,
 'jreAvailableProcessors': 8,
 'jreFreeMemory': 12723434776,
 'jreMaxMemory': 51469877248,
 'jreTotalMemory': 31622422528,
 'jreVersion': '1.8.0_181',
 'latestMilestone': TransactionHash(b'U9RSQVPT9JYVHYMKUOUTNFVLJZ9CNGXLGFM9LV9J9QSYXEKAC9TITOTKEEZIALCSUKFYHUKVJFRXKH999'),
 'latestMilestoneIndex': 972867,
 'latestSolidSubtangleMilestone': TransactionHash(b'U9RSQVPT9JYVHYMKUOUTNFVLJZ9CNGXLGFM9LV9J9QSYXEKAC9TITOTKEEZIALCSUKFYHUKVJFRXKH999'),
 'latestSolidSubtangleMilestoneIndex': 972867,
 'milestoneStartIndex': 434525,
 'neighbors': 7,
 'packetsQueueSize': 0,
 'time': 1544210022173,
 'tips': 2687,
 'transactionsToRequest': 2}
 ```
