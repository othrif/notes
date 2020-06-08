---
title: "Parsing command line options"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
``` python
import argparse

parser = argparse.ArgumentParser(description='Program to analyze something.')
parser.add_argument(dest='filenames', metavar='filename', nargs='*')
parser.add_argument('-i', '--input', metavar='input_file', required=False, dest='input_file', action='store', default='./input/dummy.csv', help='Input csv file')
parser.add_argument('-o', '--output', metavar='output_file', required=False, dest='output_file', action='store', default='./output/out_dummy.csv', help='Output csv file with results')
parser.add_argument('--choice', dest='mychoice', action='store', choices='{'slow','fast'}', default='slow', help='my speed choice')
parser.add_argument('-p', '--pat', metavar='pattern', required=True, dest='mychoice', action='append', help='can append to the list of arguments here')
parser.add_argument('-v', '--verbose', dest='verbose', action='store_true', help='Verbose mode')
args = parser.parse_args()
```


```python

```
