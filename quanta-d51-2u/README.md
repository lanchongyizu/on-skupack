# Quanta D51 skupack

## BIOS firmware upgrade
- The BIOS firmware files should be acquired from the vendor.  The BIOS image and BIOS upgrade executable are then extracted into the /static/bios location of the skupack and the config.json should be updated with the md5sum of the firmware image.
- A valid BMC or BIOS firmware image is made up of path and filename like bios/file.img. Image filename should end with .bin, .BIN, .zip, .img or .ima. Image path should be "bios/", "bmc/" or empty value. Other format of image will be recognized as incorrect by schema validator.
- The following vendor versions have been validated with this skupack
 1. S2B_3A19.DDN02.BIN
 2. S2B_3A21.BIN

**Run a BIOS upgrade against a node**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.BIOS"
}
```

**Run a BIOS upgrade against a node without rebooting at the end**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.BIOS",
    "options": {
        "when-reboot-at-end": {
            "rebootAtEnd": "false"
        }
    }
}
```
**Run a BIOS upgrade against a node with an image file override**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.BIOS",
    "options": {
        "upgrade-bios-firmware": {
            "imageFile": "file.img"
        }
    }
}
```
The image file should be uploaded to the RackHD instance with the Files API before
invoking the workflow and the "imageFile" property should be set to the value of
the resource name specified in the files URI. It only works when the default
API is 2.0 version, meaning no ''"versionBase": "1.1"'' specified in config file
```
curl -X PUT -T file.img http://localhost:8080/api/current/files/file.img
```
## BMC firmware upgrade
- The BMC firmware files should be acquired from the vendor.  The BMC image and BMC upgrade executable are then extracted into the /static/bmc location of the skupack and the config.json should be updated with the md5sum of the firmware image.
- A valid BMC or BIOS firmware image is made up of path and filename like bios/file.img. Image filename should end with .bin, .BIN, .zip, .img or .ima. Image path should be "bios/", "bmc/" or empty value. Other format of image will be recognized as incorrect by schema validator.
- The following vendor versions have been validated with this skupack
 1. 3.32
 2. 3.42

**Run a BMC upgrade against a node**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.Bmc"
}
```

**Run a BMC upgrade against a node without rebooting at the end**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.Bmc",
    "options": {
        "when-reboot-at-end": {
            "rebootAtEnd": "false"
        }
    }
}
```
**Run a BMC upgrade against a node with an image file override**
```
POST
/api/current/nodes/<id>/workflows
{
    "name": "Graph.Flash.Quanta.Bmc",
    "options": {
        "upgrade-bmc-firmware": {
            "imageFile": "file.img"
        }
    }
}
```
The image file should be uploaded to the RackHD instance with the Files API before
invoking the workflow and the "imageFile" property should be set to the value of
the resource name specified in the files URI. It only works when the default
API is 2.0 version, meaning no ''"versionBase": "1.1"'' specified in config file
```
curl -X PUT -T file.img http://localhost:8080/api/current/files/file.img
```

## NVRAM firmware upgrade
- The NVRAM image should be built following the vendor provided instructions.  Once built, the NVRAM configuration file and the NVRAM upgrade executable should be placed in the /static/bios location of the skupack and the config.json should be updated with the md5sum of the firmware image.
