https://docs.python.org/2.7/library/argparse.html

mejora sobre optparse
A partir de python2.7

mirar docopt.md

mirar argh.md
Parece complicado

argparse nos autogenera los usage, pone valores por defecto, limita que valores podemos meter, etc.

import argparse

# Parse arguments, just config file
parser = argparse.ArgumentParser(prog="cyclops", description='Monitoring as a service')
parser.add_argument("-c", "--config", action="store", dest="input_config_file",
                            help="Path to the cyclops configuration file.", default=None)
args = parser.parse_args()

if args.input_config_file:
    config_file = args.input_config_file
else:
    config_file = "/etc/cyclops_agent.conf"



import argparse
parser = argparse.ArgumentParser()
parser.add_argument("-c", "--config", dest="input_config_file", help="Path to the cyclops configuration file.", default="/etc/cyclops_agent.conf")
parser.add_argument("-u", "--user", dest="user", help="Introduce user name.", default=None, required=True, choices=['maria', 'pepe'])


Parsear numeros (type=[float,int]):
  parser.add_argument('--timeout-cinder', '-C', help='Number of seconds to wait for volume creation before timeout',
      dest=OpenstackConstants.KEY_TIMEOUT_CINDER, action='store',required=False, default=OpenstackConstants.DEFAULT_TIMEOUT_CINDER,type=int)


p.add_argument("-G", "--no_graph", action="store_const", dest="graph", help="Not show graphic", default=True, const=False)
  Si ponemos '-G', la variable "graph" se pone a False, si no, True.


Si queremos que la ayuda muestre los valores por defecto:
http://stackoverflow.com/questions/12151306/argparse-way-to-include-default-values-in-help
parser = argparse.ArgumentParser(formatter_class=argparse.ArgumentDefaultsHelpFormatter)


# Subcomandos
Mirar parser_subcommands.py
