# pkg-ifscript 
Run conditional package scripts

![terminal](https://i.ibb.co/MSCMDpT/image.png)

> Yarn and npm are supported.
> Prefixes are not supported (now).

## Documentation
### Conditions
#### Platform (platform)
Specifies operating system. 
##### Type
`String` or `String Array`.
##### Values
- aix
- android
- darwin
- freebsd
- linux
- openbsd
- sunos
- win32
- unix <sup>1</sup>
- posixlike <sup>2</sup>

<sup>1</sup> non-win32 platforms<br>
<sup>2</sup> unix and windows if environment is cmder, cygwin or mingw.

#### Architecture (arch)
Specifies CPU architecture. 
##### Type
`String` or `String Array`.
##### Values
- arm
- arm64
- ia32
- ppc
- ppc64
- s390
- s390x
- x32
- x64

#### Shell (shell)
Specifies default shell. Only base name is used. For example:
    
    $ npm config get script-shell
    /usr/bin/sh

The value is `sh`.
##### Type
`String` or `String Array`.
##### Values
- sh
- bash
- dash
- zsh
- fish
- tcsh
- ksh
- mksh
- cmd
- powershell

and others...

#### Environment (env)
Specifies environment variables.
##### Type
`Object`

## Example
*package.json*

    {
        ...
        "scripts": {
            "test": "pkg-ifscript"
        },
        ...
        "pkg-ifscript": {
            "test": [
                {
                    "platform": "posixlike",
                    "script": "echo 'runs on unix and windows (cmder, cygwin, mingw etc. only)'"
                },
                {
                    "script": "echo runs everywhere"
                },
                {
                    "platform": "unix",
                    "script": "echo runs on non-windows systems"
                },
                {
                    "script": "echo runs on windows, linux and x64 cpu",
                    "platform": [
                        "win32",
                        "linux"
                    ],
                    "arch": "x86"
                },
                {
                    "env": {
                        "XDG_MENU_PREFIX": "gnome-",
                        "LANG": "en_US.UTF-8"
                    },
                    "script": "echo runs if DE is gnome and language is english"
                }
            ]
        }
    }