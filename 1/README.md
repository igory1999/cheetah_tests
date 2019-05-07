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
  test_cheetah.test_model.test_bad_scheduler_options ... ok
  test_cheetah.test_model.test_default_scheduler_options ... ok
  test_cheetah.test_model.test_codes_ordering ... ERROR
  test_cheetah.test_model.test_error_campaign_undefined_code ... ok
  test_cheetah.test_model.test_error_campaign_missing_adios_xml ... ok
  test_cheetah.test_model.test_error_nodes_too_small ... ok
  test_cheetah.test_model.test_nodes_sosflow ... ERROR
  test_cheetah.test_model.test_node_layout_repeated_code ... ERROR
  test_cheetah.test_model.test_node_layout_bad_ppn ... ok
  test_cheetah.test_model.test_node_layout_bad_codes_per_node ... ok
  test_cheetah.test_model.test_node_layout_bad_shared_nodes ... ok
  test_cheetah.test_model.test_error_missing_app_dir ... ok
  test_cheetah.test_parameters.test_instance_nprocs_only ... ok
  test_cheetah.test_parameters.test_derived_params ... ok
  test_cheetah.test_parameters.test_derived_params_cross_code ... ok
  Failure: ModuleNotFoundError (No module named 'codar.workflow') ... ERROR
  Failure: ModuleNotFoundError (No module named 'codar.workflow') ... ERROR
  ```
  ```
  ERROR: test_cheetah.test_model.test_codes_ordering

  Traceback (most recent call last):
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/igor/test1/cheetah/tests/nose/test_cheetah/test_model.py", line 89, in test_codes_ordering
    fobs.append(json.loads(line))
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/json/__init__.py", line 348, in loads
    return _default_decoder.decode(s)
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/json/decoder.py", line 337, in decode
    obj, end = self.raw_decode(s, idx=_w(s, 0).end())
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/json/decoder.py", line 355, in raw_decode
    raise JSONDecodeError("Expecting value", s, err.value) from None
    json.decoder.JSONDecodeError: Expecting value: line 2 column 1 (char 2)

  ERROR: test_cheetah.test_model.test_nodes_sosflow

  Traceback (most recent call last):
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/igor/test1/cheetah/tests/nose/test_cheetah/test_model.py", line 208, in test_nodes_sosflow
    c.make_experiment_run_dir(out_dir, _check_code_paths=False)
  File "/home/igor/test1/cheetah/codar/cheetah/model.py", line 353, in make_experiment_run_dir
    run_dir_setup_script=self.run_dir_setup_script)
  File "/home/igor/test1/cheetah/codar/cheetah/launchers.py", line 101, in create_group_directory
    machine.processes_per_node)
  File "/home/igor/test1/cheetah/codar/cheetah/model.py", line 810, in insert_sosflow
    working_dir=self.run_path)
  TypeError: __init__() missing 1 required positional argument: 'sched_args'

  ERROR: test_cheetah.test_model.test_node_layout_repeated_code

  Traceback (most recent call last):
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/case.py", line 198, in runTest
    self.test(*self.arg)
  File "/home/igor/test1/cheetah/tests/nose/test_cheetah/test_model.py", line 216, in test_node_layout_repeated_code
    nl = NodeLayout(layout)
  File "/home/igor/test1/cheetah/codar/savanna/node_layout.py", line 39, in __init__
    self._validate()
  File "/home/igor/test1/cheetah/codar/savanna/node_layout.py", line 90, in _validate
    raise ValueError("{} found in node-layout multiple "
  AttributeError: 'ValueError' object has no attribute 'format'

  ERROR: Failure: ModuleNotFoundError (No module named 'codar.workflow')

  Traceback (most recent call last):
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/failure.py", line 39, in runTest
    raise self.exc_val.with_traceback(self.tb)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/loader.py", line 418, in loadTestsFromName
    addr.filename, addr.module)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/importer.py", line 47, in importFromPath
    return self.importFromDir(dir_path, fqname)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/importer.py", line 94, in importFromDir
    mod = load_module(part_fqname, fh, filename, desc)
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/imp.py", line 234, in load_module
    return load_source(name, filename, file)
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/imp.py", line 171, in load_source
    module = _load(spec)
  File "<frozen importlib._bootstrap>", line 696, in _load
  File "<frozen importlib._bootstrap>", line 677, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 728, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "/home/igor/test1/cheetah/tests/nose/test_workflow/test_model.py", line 4, in <module>
    from codar.workflow.model import Pipeline, Run, srun, aprun
  ModuleNotFoundError: No module named 'codar.workflow'

  ERROR: Failure: ModuleNotFoundError (No module named 'codar.workflow')

  Traceback (most recent call last):
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/failure.py", line 39, in runTest
    raise self.exc_val.with_traceback(self.tb)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/loader.py", line 418, in loadTestsFromName
    addr.filename, addr.module)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/importer.py", line 47, in importFromPath
    return self.importFromDir(dir_path, fqname)
  File "/home/igor/test1/cheetah/venv-cheetah/lib/python3.7/site-packages/nose/importer.py", line 94, in importFromDir
    mod = load_module(part_fqname, fh, filename, desc)
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/imp.py", line 234, in load_module
    return load_source(name, filename, file)
  File "/usr/local/Anaconda3-2019.03/lib/python3.7/imp.py", line 171, in load_source
    module = _load(spec)
  File "<frozen importlib._bootstrap>", line 696, in _load
  File "<frozen importlib._bootstrap>", line 677, in _load_unlocked
  File "<frozen importlib._bootstrap_external>", line 728, in exec_module
  File "<frozen importlib._bootstrap>", line 219, in _call_with_frames_removed
  File "/home/igor/test1/cheetah/tests/nose/test_workflow/test_scheduler.py", line 5, in <module>
    from codar.workflow.scheduler import JobList
  ModuleNotFoundError: No module named 'codar.workflow'

  Ran 17 tests in 0.072s
  FAILED (errors=5)
  ```



