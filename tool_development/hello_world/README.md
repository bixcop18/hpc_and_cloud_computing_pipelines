### A hello world example for Galaxy

This is a very simple "hello world" tool wrapper for [Galaxy](https://www.galaxyproject.org/).

#### Steps to use:

1. Make a working directory such as `hello_world/` (`mkdir hello_world`)
2. Change directory into this directory (`cd hello_world`)
3. Download the tool wrapper:
```
wget https://raw.githubusercontent.com/bixcop18/hpc_and_cloud_computing_pipelines/master/tool_development/hello_world/hello_world.xml
```
4. Make a `test-data` directory (`mkdir test-data`)
5. Download the test data file to this directory:
```
wget -O test-data/output.txt https://raw.githubusercontent.com/bixcop18/hpc_and_cloud_computing_pipelines/master/tool_development/hello_world/test-data/output.txt
```

To work with this install [planemo](https://planemo.readthedocs.io/en/latest/).

To test that the file is correct, use the `planemo lint --skip 'citations'` command. You should see:

```
Applying linter tests... CHECK
.. CHECK: 1 test(s) found.
Applying linter output... CHECK
.. INFO: 1 outputs found.
Applying linter inputs... CHECK
.. INFO: Found 1 input parameters.
Applying linter help... CHECK
.. CHECK: Tool contains help section.
.. CHECK: Help contains valid reStructuredText.
Applying linter general... CHECK
.. CHECK: Tool defines a version [0.0.1].
.. CHECK: Tool defines a name [hello].
.. CHECK: Tool defines an id [hello].
.. CHECK: Tool targets 16.01 Galaxy profile.
Applying linter command... CHECK
.. INFO: Tool contains a command.
Applying linter tool_xsd... CHECK
.. INFO: File validates against XML schema.
```

To run automated tests: `planemo test`

And to run a Galaxy server with this as the only tool available, `planemo serve`