Introduction
------------

The EDA-MimeTypes repository maintains MIME information about files used in the Electronic Design Automation (EDA) industry. [Many companies](http://en.wikipedia.org/wiki/List_of_EDA_companies) (vendors) operate in this field and each company typically has multiple products in their portfolio. Most of the time these products generate many output files and unfortunately in many cases these files are not properly classified by the vendors themselves.

The goal of this repository is to provide a central place to store MIME information about these files. Anyone can reference, contribute, file bugs against or comment on the list.

The aim is to complement the shared MIME-info database maintained by freedesktop.org, which lacks information about the files in the EDA industry. 

Background
----------

The idea of MIME types are nicely described by the __Shared MIME-info Database specification's__ description:

> Many programs and desktops use the MIME system to represent the types of files. Frequently, it is necessary to work out the correct MIME type for a file. This is generally done by examining the file's name or contents, and looking up the correct MIME type in a database.
>
> It is also useful to store information about each type, such as a textual description of it, or a list of applications that can be used to view or edit files of that type.
> 
> For interoperability, it is useful for different programs to use the same database so that different programs agree on the type of a file and information is not duplicated. It is also helpful for application authors to only have to install new information in one place.

For more information see [the specification itself](http://standards.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-latest.html/).

In our case, the goal of the EDA mime database is to bring together knowledge about files used in the field and store it in a central place where it can easily be referenced by individuals operating in the EDA-field. 

How It Works
------------

In order to classify the vast majority of files in the industry, we use the XML schema specified by freedesktop.org. Using this shema allows anyone to download the database xml file and use it on their local machine (see Using The Database). 

The database consists of a single XML file which contains a list of mime-type nodes. Each mime-type node describes a file type in detail and looks something like this:

```xml
<mime-type type="application/vnd.xilinx.ise.map_report">
	<comment xml:lang="en">MAP report</comment>
	<comment xml:lang="af">MAP verslag</comment>
	...
	<glob pattern="*.map"/>
</mime-type>
```

To organize things nicely, the repository uses a specific format for the __mime-type__ node's __type__ attribute that looks like this:
```xml
application/vnd.$VENDOR_NAME$.$VENDOR_PRODUCT$.$DESCRIPTION$
```
Where:
* __$VENDOR_NAME$__ = The name of the vendor
* __$VENDOR_PRODUCT$__ = The name of the vendor's product
* __$DESCRIPTION$__ = A description of the file

Note that we use all lowercase characters to describe the vendor's name and product for consistancy.

The above example is pretty simple, and can be extended. Again, you can reference the full specification [here](http://standards.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-latest.html#id2661973) for more information.

EDA Extensions
--------------

In addition to the standard items specified by the freedesktop.org specification, the following additional elements are specified in order to futher classify properties of files applicable to the EDA industry:

__<eda:generated>__ - Indicates if a file is generated. Thus, it should be ignored by version control systems and be cleaned in clean operations.

If you would like to add additional extension tags, please file a request on the issue tracker in order to pick up a discussion over there.

General Hints
-------------

When you encounter a file that you know belongs to a tool, however you don't know what the file represents, you can add it under an __internal__ group. For example:

```xml
<mime-type type="application/vnd.xilinx.map.internal">
	<comment xml:lang="en">Xilinx Map Internal Files</comment>
	<glob pattern="*.ngm"/>
	<glob pattern="*.mdf"/>	
	<eda:generated>true</eda:generated>
</mime-type>
```

Someone out there will know what it is, and in time internal files can be grouped into their own <mine-type> elements.

Using The Database
------------------

The database can simply be used as a reference if you want to quickly look up the meaning of a file, or you can download the database XML file and install it on your system as described [here](http://freedesktop.org/wiki/Specifications/AddingMIMETutor).

Licensing
---------
The database is available under the Creative Commons Attribution + Noncommercial license. Click [here](http://creativecommons.org/licenses/by-nc/3.0/) for more details.

Copyright (c) 2012-2012, Jaco Naude