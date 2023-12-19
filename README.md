![Houdini Logo](https://static.sidefx.com/images/ui/sfx_logo.svg)

![Unreal Logo](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/logo/UE_Logo_horizontal_unreal-engine_white.svg)

![Python Logo](https://github.com/97AlexNguyen/Alex_Houdini_Things/blob/main/logo/python_and_qt_logo.svg)

![Main Logo](https://github.com/97AlexNguyen/Alex_Houdini_Things/blob/main/logo/Main_logo.svg)

<p align="center">
   <a href="https://github.com/97AlexNguyen">
    <img alt="Website" src="https://img.shields.io/website?label=main%20project&up_message=Community%20Projects&url=https%3A%2F%2Fgithub.com%2Fnitzan-treg%2Fcommunity_projects">
  </a>
  <a href="https://github.com/97AlexNguyen/Alex_Houdini_python">
    <img alt="GitHub repo size" src="https://img.shields.io/github/repo-size/97AlexNguyen/Alex_Houdini_python">
  </a>
</p>

## Authors

- [@97AlexNguyen](https://github.com/97AlexNguyen)

<h3 align="center">🔭 This is a document that I created for my personal use. It includes Python scripts , VEX , python qt , VFX like RBD sim , Vellum Sim , and working with unreal engine as well. You can find a lot of useful information here, such as Python scripts for working with HDA, tips and tricks for parameter settings like toggle and button strip and etc. Please note that this document is not yet complete, but I will update it whenever I have some free time </h3>

 
<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://fb.com/nguyenvuquocan" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/facebook.svg" alt="nguyenvuquocan" height="30" width="40" /></a>
<a href="https://www.youtube.com/@anquoc/videos" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="uczhcuz1wi4wwsmvauvmigbq" height="30" width="40" /></a>
</p>

- 📫 How to reach me **8197alexnguyen@gmail.com**

- 👯 Pm me If you want to collaborate on [this repo](https://github.com/97AlexNguyen/Alex_Houdini_Things/tree/main) 

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://unrealengine.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/kenangundogan/fontisto/036b7eca71aab1bef8e6a0518f7329f13ed62f6b/icons/svg/brand/unreal-engine.svg" alt="unreal" width="40" height="40"/> </a> <a href="https://www.sidefx.com/" target="_blank" rel="noreferrer"> <img src="https://github.com/97AlexNguyen/Alex_Houdini_Things/blob/main/logo/sidefx_badge.png" alt="houdini" width="40" height="40"/> </a> </a> <a href="https://www.qt.io/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/0/0b/Qt_logo_2016.svg" alt="qt" width="40" height="40"/> </a></p>

<div align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs?username=97AlexNguyen&locale=en&hide_title=false&layout=compact&card_width=320&langs_count=5&theme=dracula&hide_border=false" height="150" alt="languages graph"  />
</div>



# $\color[RGB]{122, 255, 253} A \ : \ Houdini \ HDA \ and \ Python \ Module$ 

> All examples you can find in "Test HDA"
>To use test packages, download the latest version of the repo and extract all files to the "packages" folder. All folders and files should be directly inside the "packages" folder, not within a subfolder of the "packages" folder.

## 1 : Create a [Houdini packages](https://www.sidefx.com/docs/houdini/ref/plugins.html)

>This is a method that enables loading of specific Python modules to Houdini without requiring any modification to the system environment variables. It utilizes a relative path technique which allows it to function on any computer and with any version of Houdini, as long as the Python version being used is compatible with that particular version of Houdini. Additionally, this method is easier to manage, especially when there are multiple Houdini packages involved.

A Houdini Package is like a main document where you can store HDAs, toolbars, Python modules, include codes, and more. This method is extremely helpful for those who want to maintain a clean Houdini document and wish to easily re-install it at a later time or share the package with someone who needs to use it.

To create a Houdini package, you need to create a json file that saves the path to the package and loads it into Houdini. This json file is essential for using and sharing the package. The json file working with relative path so we dont need to care about name of pc or houdini version.


Create a json file , :

```json
{
    "enable": true,
    "path": "$HOUDINI_PACKAGE_PATH/test_packages",    
    "env": 
    [
        {
            "HOUDINI_OTLSCAN_PATH": "$HOUDINI_PACKAGE_PATH/test_packages/hda;"
        }
    ]
}
```
[See Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/houdini_packages_json.png)




## 2 : Auto Load Python module in every houdini session (Relative path)
In Houdini, there is a script file named is [456.py](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/load_456py.png).
Houdini runs this script whenever a scene file is loaded (including when Houdini starts up with a scene file).
We can use this method to load a module python to every session houdini . 
Create a 456.py then put it in houdini.xx\packages\test_packages\scripts

In [456.py](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/test_packages/scripts/456.py) 
```python
import os
import sys
import hou
## Retrieve the current Houdini version when a Houdini session is opened.
hou_version = hou.applicationVersion()
hou_int_version = str(hou_version[0]) + "." + str(hou_version[1])
houdini_split_version = "houdini"+hou_int_version


## Get Relative Path of Documents.
current_document = os.path.join(os.environ['USERPROFILE'], 'Documents')
current_document.replace("\\","/")
houdini_document = current_document + "/" + houdini_split_version

##  Get Relative Path of houdini packages.
## Read about houdini packages form here https://www.sidefx.com/docs/houdini/ref/plugins.html
houdini_packages_document = houdini_document + "/packages/test_packages"

## All python module here . 
python_lib = houdini_packages_document + "/Python/site-packages"

## load python module via sys append.
sys.path.append(python_lib)
```
Test import module [See image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/test_load_module.png)

>You can find many Python scripts for Houdini Digital Assets (HDAs) here, such as callback scripts, working with button strips, toggles, dynamic UI, and PyQt5 as well.

## 3 : Call a definition using callback script .

Create a definition in PythonModule (scripts tab).

```Python
def a_test(kwargs):
    print("a_test")

def b_test(kwargs):
    print("b_test")
```
[Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/create_a_def.png)

Dont know what "kwargs" meaning ? . [Read this](https://www.sidefx.com/docs/houdini/hom/locations.html)

Then create a Button > Callback script (Work with any parameter like a float , int , toggle...)
```Python
hou.pwd().hdaModule().a_test(kwargs)
```
Can call a multi def like this :

```Python
hou.pwd().hdaModule().a_test(kwargs);hou.pwd().hdaModule().b_test(kwargs)
```
[Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/callback_script.png)

## 4 : Read paramater and get the value of parameter . 

> In the HDA module’s code, you can get a reference to the HDA’s node name using:

```Python
node = kwargs["node"]
```
Test with callback script :
In python module : 
```
def _kwargs(kwargs):
    node = kwargs["node"]
    print(node)
```
In callback script of button :
```Python
hou.pwd().hdaModule()._kwargs(kwargs)
```
[Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/kwargs_node.png)

## 5 :Get the value of parameter: 
> "All parameters need to be identified by their 'name' rather than their 'label'."

Create float and int parameters named "float_test" and "int_test".
Create a def in PythonModule :
```Python
def load_parm(kwargs):
    node = kwargs["node"]
    _float = node.parm("float_test").eval()
    _int = node.parm("int_test").eval()
    print(_float)
    print(_int)
```
Create a Button and in "Callback Script":
```Python
hou.pwd().hdaModule().load_parm(kwargs)
```
[Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/load_parm_hda.png)


## 6 : Set the value of parameter: 

Create float and int parameters named "float_test_for_set" and "int_test_for_set".
Now we are using value of float_test and int_test to set value for float_test_for_set and int_test_for_set.

```Python
def set_parm_value(kwargs):
    node = kwargs["node"]
    _float = node.parm("float_test").eval()
    _int = node.parm("int_test").eval()
    ## Set value
    node.parm("float_test_for_set").set(_float)
    node.parm("int_test_for_set").set(_int)    
```
Then in callback script of a button :
```Python
hou.pwd().hdaModule().set_parm_value(kwargs)
```
[Image](https://github.com/97AlexNguyen/Alex_Houdini_python/blob/main/tutorial_image/set_parm.png)

 
# $\color[RGB]{122, 255, 253} B \ : \ Python Qt \ for \ Houdini$ 


# $\color[RGB]{122, 255, 253} C \ : \ RBD \ in \ Houdini$ 


# $\color[RGB]{122, 255, 253} D \ : \ Vellum \ sim \ in \ Houdini$ 


# $\color[RGB]{122, 255, 253} E \ : \ Houdini \ for \ Unreal Engine$ 




$\mathscr{\color{red}{Updating...}}$













