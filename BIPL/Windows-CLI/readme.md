## Core Config
`sconfig`

## Active Directory
```bat
csvde -i -k -f .\patienten2.csv
ldifde -i -f .\patienten3.ldf
Import-Csv .\patienten5.csv | New-ADUser
dsquery user -stalepwd 10
dsquery user -disabled -limit 5000
dsmod user -disabled no -pwd "@dmin2020"
dsquery user "OU=Patienten,DC=bmc,DC=local"
```
## dsmove script
```bat
@echo Automated scripting
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc HA1 > HA1.txt
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc HA2 > HA2.txt
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc TA1 > TA1.txt
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc TA2 > TA2.txt
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc Fysiotherapie > Fysiotherapie.txt
dsquery user "ou=patienten,dc=bmc,dc=local" -limit 0 -desc Verpleegkundige > Verpleegkundige.txt

For /f "tokens=* delims=" %%a in (HA1.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=HA1,ou=huisartsen,dc=bmc,dc=local" >> HA1.bat)

For /f "tokens=* delims=" %%a in (HA2.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=HA2,ou=huisartsen,dc=bmc,dc=local" >> HA2.bat)

For /f "tokens=* delims=" %%a in (TA1.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=TA1,ou=tandartsen,dc=bmc,dc=local" >> TA1.bat)

For /f "tokens=* delims=" %%a in (TA2.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=TA2,ou=tandartsen,dc=bmc,dc=local" >> TA2.bat)

For /f "tokens=* delims=" %%a in (Fysiotherapie.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=Fysiotherapie,dc=bmc,dc=local" >> Fysiotherapie.bat)

For /f "tokens=* delims=" %%a in (Verpleegkundige.txt) Do (
@echo %%a
@echo dsmove %%a -newparent "ou=Verloskundigen,dc=bmc,dc=local" >> Verpleegkundige.bat)
PAUSE
```