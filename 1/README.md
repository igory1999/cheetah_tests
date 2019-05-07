# Environment

  Laptop with Ubuntu 18.04, Anaconda3/2019.03

## Python
  ```
  $ module load Anaconda3
  $ python
  Python 3.7.3 (default, Mar 27 2019, 22:11:17) 
  [GCC 7.3.0] :: Anaconda, Inc. on linux
  Type "help", "copyright", "credits" or "license" for more information.
  >>>
  ```
  ```
  $ which python
  /usr/local/Anaconda3-2019.03/bin/python
  $ which python3
  /usr/local/Anaconda3-2019.03/bin/python3
  $ which pip
  /usr/local/Anaconda3-2019.03/bin/pip
  ```

## virtualenv
  ```
  $ cd
  $ mkdir test1
  $ cd test1
  $ git clone https://github.com/CODARcode/cheetah.git
  ...
  $ cd cheetah
  $ git branch
  * master
  $ git checkout node-layout
  $ git branch
  master
  * node-layout
  $ python3 -m venv venv-cheetah
  $ source venv-cheetah/bin/activate
  (venv-cheetah) $ pip install --editable .
  ...
  Successfully installed cheetah
  You are using pip version 19.0.3, however version 19.1.1 is available.
  You should consider upgrading via the 'pip install --upgrade pip' command.                                                                                                          ``` 

# Tests
  ```
  $ pip install nose
  $ export CODAR_APPDIR=fake
  $ tests/run-all.sh




