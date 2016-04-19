# Basic service management

To check state of all services:
```bash
svcs -a
```
To disable the service (stop it) -the name as it appears in scvs
```bash
svcadm disable -t network/nameofservice:default
```

To start a disabled service -the name as it appears in scvs
```bash
svcadm enable -t network/nameofservice:default
```

To create your own service create an xml file that lists the dependencies, start, stop and restart commands:
```xml
<?xml version="1.0"?>
<!DOCTYPE service_bundle
SYSTEM "/usr/share/lib/xml/dtd/service_bundle.dtd.1">
<service_bundle type='manifest' name='SAS:Metadata'>
<service
name='network/transmission'
type='service'
version='1'>
<create_default_instance enabled='true' />
<single_instance />
<dependency name='fs' grouping='require_all' restart_on='none'
type='service'>
<service_fmri value='svc:/system/filesystem/local'/>
</dependency>
<exec_method
type='method'
name='start'
exec='/usr/gnu/bin/transmission-daemon'
timeout_seconds='60'>
</exec_method>
<exec_method
type='method'
name='stop'
exec=':kill'
timeout_seconds='60' >
</exec_method>
<property_group name='startd' type='framework'>
<propval name='duration' type='astring' value='contract' />
</property_group>
</service>
</service_bundle>
```
Then add the xml file to the service manager with
```bash
sudo svccfg import nameofservice.xml
```
To remove a service from the manager first make sure it is disabled then

```bash
sudo svccfg delete network/service:default
```

This will auto start on boot as ROOT unless you specify otherwise.You can change the user by adding in method credentials into the start, stop or restart exec_methods.
```xml
<method_context> <method_credential user='sas' /> </method_context>
```

More hints/info here:
* http://www.oracle.com/us/products/servers-storage/solaris/solaris-smfmanifest-wp-167902.pdf
* http://discuss.joyent.com/viewtopic.php?id=12802
* http://www.sun.com/bigadmin/content/selfheal/smf-quickstart.jsp
* http://www.sun.com/bigadmin/features/articles/smf_example.jsp

credit for these docs go to [/u/127b](https://www.reddit.com/user/127b)
