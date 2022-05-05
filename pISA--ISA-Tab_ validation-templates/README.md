# pISA -- ISA-Tab validation
pISA xml and ISA-Tab Investigation templates

## pISA assay types

at <https://github.com/NIB-SI/pISA-tree-assay-types/tree/main/Assay-types>


## external links

[Code Beautify](https://codebeautify.org/)

<https://github.com/ISA-tools/Configuration-Files/tree/master/isaconfig-default_v2015-07-02> source for investigation.xml

<https://github.com/ISA-tools/isa-api/blob/master/isatools/examples/validateISAtab.py>

<https://github.com/ISA-tools/isa-api/blob/master/isatools/isatab.py>

<http://www.ontobee.org/ontology/OBI?iri=http://purl.obolibrary.org/obo/OBI_0000911> 

... and more at [Ontobee](http://www.ontobee.org)


## generic notes

### DO 

tree/master/ to trunk/ - oneliner with subversion

```svn export https://github.com/ISA-tools/Configuration-Files/trunk/isaconfig-default_v2015-07-02```

### DO NOT

```wget https://github.com/ISA-tools/ISAvalidator-ISAconverter-BIImanager/releases/download/1.6.5/ISA-validator-1.6.5.zip```

### types

```type="xs:decimal"``` not supported

### add .xml templates

to isaconfig-default_v2015-07-02 subdir

and call for e.g. qPCR set

```
python3

>>> import os, json, isatools; from isatools import utils, isatab

>>> my_json_report = isatab.validate(open(os.path.join('directory_path', 'i__I_Test-extended.txt')), 'path-to/isaconfig-default_v2015-07-02')

>>> with open('report-i__I_Test-qPCR.txt', 'w') as report_file:
     report_file.write(utils.format_report_csv(my_json_report))
```


## general note

in <https://github.com/ISA-tools/isa-api/blob/master/isatools/isatab.py>, besides hardcoded 
```
Investigation Person Last Name
Investigation Person First Name
Investigation Person Mid Initials
Investigation Person Email
Investigation Person Phone
Investigation Person Fax
Investigation Person Address
Investigation Person Affiliation
Investigation Person Roles
Investigation Person Roles Term Accession Number
Investigation Person Roles Term Source REF
```

also ```'Source Name', 'Sample Name', 'Extract Name', 'Labeled Extract Name'``` are hardcoded/reserved to grep positions (and ignore all after),

plus be aware of

```

field_headers = [i for i in table.columns if
                         i.lower().endswith(' name') or i.lower().endswith(
                             ' data file') or i.lower().endswith(
                             ' data matrix file')]
        protos = [i for i in table.columns if i.lower() == 'protocol ref']
        if len(protos) > 0:
            last_proto_indx = table.columns.get_loc(protos[len(protos) - 1])

``` 
and which colnames will be even considered


doesnt parse well strings containing {[]}


