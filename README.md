# desktopentryparse
https://github.com/wbin01/desktopentryparse

Python lib to find and provide easy access to desktop files values.

Follows the specification from freedesktop.org: www.freedesktop.org/wiki/Specifications/basedir-spec/

No dependencies, just use the standard library.
### Definitions overview
See the [documentation](#) for details.
```
desktopentryparse.FileLocations()
    ulrs: list
    ulrs_by_priority: list
    file_dirs: list

desktopentryparse.DesktopFile(url: str)
    as_dict: dict
    url: str
```
Locate desktop file folders, and get the URL addresses of those files

```python
>>> local = FileLocations()
>>> local.file_dirs
['/home/user/.local/share/applications',
 '/usr/local/share/applications',
 '/usr/share/applications',
 '/home/user/.local/share/flatpak/exports/share/applications',
 '/var/lib/flatpak/exports/share/applications',
 '/var/lib/snapd/desktop/applications']
>>>
>>> local.ulrs_by_priority
['/home/user/.local/share/applications/jetbrains-pycharm-ce.desktop',
 '/usr/local/share/applications/vim.desktop',
 '/usr/share/applications/org.inkscape.Inkscape.desktop',
 '/usr/share/applications/vlc.desktop',
 '/usr/share/applications/python3.10.desktop',
 '/home/user/.local/share/flatpak/exports/share/applications/org.gimp.GIMP.desktop',
 '/var/lib/flatpak/exports/share/applications/com.obsproject.Studio.desktop',
 '/var/lib/snapd/desktop/applications/ohmygiraffe_ohmygiraffe.desktop',
 ...
 ]
```
Get the contents of a desktop file

```python
>>> desktop_file = DesktopFile(url='/usr/share/applications/firefox.desktop')
>>> desktop_file.as_dict['[Desktop Entry]']['Name']
'Firefox Web Browser'
>>> desktop_file.as_dict['[Desktop Entry]']['Type']
'Application'
>>> for key in desktop_file.as_dict.keys():
...     print(key)
...
[Desktop Entry]
[Desktop Action new-window]
[Desktop Action new-private-window]
>>>
>>> desktop_file.as_dict['[Desktop Action new-window]']['Name']
'Open a New Window'
```
## Tests
Download the Git repository and with the terminal enter the 
project directory.

#### unittest
Standard library unit tests can be run as follows
```console
python3 -m unittest discover
```

#### coverage
Test coverage can be verified using the "coverage" lib. 
Use pip to install it.
```console
pip3 install --upgrade pip
pip3 install coverage
```
Then run the unit tests using the "coverage" command and then use the 
"report" argument to get the test coverage status.
```console
coverage run -m unittest discover
coverage report -m
```