---
title: "CLI arguments and config with click"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Basic usage of click

Command line arguments get passed to a function that you then call later on.

``` python
import click

@click.command()
@click.option('-f', '--first', default='first')
@click.option('-s', '--second', default=10)


def test(first, second):
    print('First', first)
    print('Second', second)


test()
```


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
