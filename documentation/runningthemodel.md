---
layout: default
title: Running the model
parent: Documentation
nav_order: 4
permalink: /doc/runningthemodel
---

# Running the model

When the input data and the model configuration have been prepared, a model run can be started either
using the `openamundsen` command line utility (`openamundsen config_file.yml`), or from within
Python using the following syntax:

```python
import openamundsen as oa

config = oa.read_config('config_file.yml')  # read in configuration file
model = oa.OpenAmundsen(config)  # create OpenAmundsen object and populate unspecified parameters with default values
model.initialize()  # read in input data files, initialize state variables etc.
model.run()  # run the model
```
