# myls_command

import os
import argparse


def parse_args():
    parser = argparse.ArgumentParser(description="List files in a directory")
    parser.add_argument('directory', type=str, nargs='?', default='.')
    parser.add_argument('--all', '-a', action='store_true', help='Include dotfiles in listing')
    parser.add_argument('--long', '-l', action='store_true', help='Show the longer detailed listing')
    return parser.parse_args()


def myls(args):
    dirs = os.listdir(args.directory)

    if args.all:
        dirs += [os.curdir, os.pardir]
    else:
        dirs = [dire for dire in dirs if dire[0] != '.']

    dirs.sort()

    if args.long:
        myls_long(args)
    else:
        for fn in dirs:
            print(fn)



def myls_long(args):
    

if __name__ == "__main__":
    try:
        arguments = parse_args()
        myls(arguments)
    except OSError as err:
        print(err)
