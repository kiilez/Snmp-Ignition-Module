# Snmp-Ignition-Module
A module that allows the user to use snmp operations in scripts

This module has been migrated to gradle from Maven, so the namespace has changed.

As of now there are only four operations available. SNMP Get, GetV3, Walk and WalkV3. 
<br>Get can be called by using <code>system.snmp.get('address', port, ['OID1', 'OID2', ...], 'community')</code>. This will return a python list with the length equal to the number of OIDs provided.
<br>Walk can be called by using <code>system.snmp.walk('address', port, 'startOID', 'community')</code>. This will return a python list with all OIDs and their current values with the OID specified.
<br>GetV3 can be called by using <code>system.snmp.getV3('address', port, ['OID1', 'OID2', ...], authLevel, 'user', 'password', authProt, privProt)</code>. This will return a python list with the length equal to the number of OIDs provided.
<br>WalkV3 can be called by using <code>system.snmp.walk('address', port, 'startOID', authLevel, 'user', 'password', authProt, privProt)</code>. This will return a python list with all OIDs and their current values with the OID specified.

You can also specify other variables like the snmp version, timeout or retry count by adding 'var=value' as an extra parameter at the end.
<br>For example <code> system.snmp.get('address', port, ['OID1', 'OID2'], 'community', 'version=1', 'timeout=2000', 'retry=2') </code>.
<br>This will return a python list with the length of 2 containing the values of OID1 and OID2, or an error message.
It will perform the get operation on version 1, with a timeout of 2000ms and a retry count of 2.

If these variables are not given by the user it will use the defaults, meaning: version=2c, timeout=3000, retry=1.

SNMPv3 support has been added using GetV3 and WalkV3. Similarly to Get and Walk you may also specify other variables like timeout and retry by adding 'var=value' as an extra parameter at the end.
The version and community are not supported in V3 as it uses a username and password for authorization. 
<br>For example <code> system.snmp.getV3('address, port, ['OID1', 'OID2', ...], authLevel, 'user', 'password', authProt, privProt, 'timeout=2000', 'retry=2') </code>
<br>This will return a python list with the length of 2 containing the values of OID1 and OID2, or an error message.
It will perform the get operation on version 3, with the username/password provided and the authorization level specified with a timeout of 2000ms and a retry count of 2.

If these variables are not given by the user it will use the defaults, meaning: timeout=3000, retry=1

With v3 an authorization level must be specified as well as a username, password, authorization protocol and privacy protocol. 
The authLevel parameter expects an integer value of 1 - 3 and defaults to No authorization and not privacy if a value outside the range is specified.
<br>1 = no authorization and no privacy
<br>2 = authorization and no privacy
<br>3 = authorization and privacy

The authProt parameter selects the authorization protocol and expects an integer value of 1 - 6 and defaults to HMAC384SHA512 protocol if a value outside of the range is specified.
With no authorization selected in the authorization level this is still required, but will not be used.
<br>1 = MD5 (This is no longer safe and should not be used.)
<br>2 = SHA (This is no longer safe and should not be used.)
<br>3 = HMAC128SHA224
<br>4 = HMAC192SHA256
<br>5 = HMAC256SHA512
<br>6 = HMAC384SHA512

The privProt parameter selects the privacy protocol and expects an integer value of 1 - 4 and defaults to AES256 protocol if a value outside of the range is specified.
With no privacy selected in the authorization level this is still required, but will not be used.
<br>1 = DES
<br>2 = AES128
<br>3 = AES192
<br>4 = AES256







