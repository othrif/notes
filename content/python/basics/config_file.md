---
title: "Config file using click"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Using click with config file

Using the module `click_config_file` we can load the parameter file similar to this:

``` python 
import click
import click_config_file

@click.command()
@click.option('--name', default='World', help='Who to greet.')
@click_config_file.configuration_option()

def hello(name):
    click.echo('Hello {}!'.format(name))

hello()
```

the parameter file should read:
``` python
name='Othmane'
```

The command to use the config file is:
``` bash 
python main.py --config myconfig.txt 
```
