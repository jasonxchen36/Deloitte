|Member Firm  | Name Convention |Valid Answer |Reflecte in Content |Notes|
|--|--|--|--|--|
|Australia|AUXXXYZA0001, WHERE XXX = Site code ie syd, mel, etc… Y =  defines the security zone : Internal represented by the letter i or DMZ represented by the letter d, Z = defines the Production state:  Production represented by the letter p or Development/non-prod by the letter d,  A = Represents the server purpose based on a number as defined below (DC = 0, App = 6, Web = 5, DB = 3, Citrix = 9) /// Based on this all DMZ server would start with the following: AusyddXXXXXXX, aumeldXXXXXXX, aumel9XXX (Old naming convention), ausyd9XXX  (Old naming convention) |Yes|No||
|Belgium|BE DAC 0X00 / BE UAT 0X00 / BE WTS 0X00 - For the number ranges we use the Global standards. E.g. 0100 is AD / 0400 is Exchange etc.|Yes|No||
|BR| <BR><DC><XXX> Server in datacenter, <BR><BH><XXX> Server in Belo Horizonte, <BR><CP><XXX> Server in Campinas, <BR><FO><XXX> Server in Fortaleza, <BR><PA><XXX> Server in Porto Alegre, <BR><RE><XXX> Server in Recife, <BR><RJ><XXX> Server in Rio de Janeiro, <BR><SP><XXX> Server in São Paulo, <BR><SV><XXX> Server in Salvador |Yes|No|| 
|CA| Workstations: CAWxxxxxx (where xxxxxx is the Deloitte asset tag number), Servers: CAHOSTxxxx, CANATxxxx, CADMZxxxx |Yes|No||
|CE|ALTIA - Albania, BASJJ -Bosnia-Herzegovina, BGOSF - Bulgaria, HRZAG - Croatia, CZPRG/CZBRQ/CZOST - Czech Republic, EETLL - Estonia, HUBUD2XXX - AZURE, HUBUD4XXX - DMZ HUNGARY, HUBUD - HUNGARY, KOPRN - Kosovo, LVRIX - Latvia, LVTNO - Lithuania, MKSKP - Macedonia, MKDIV - Moldova, METGD - Montenegro, PLWAW/CESSC/PLGDN/PLKRK/PLLDS/PLLDZ/PLPOZ/PLSZZ/PLWAW/PLWLK/PLWLK/PLWRC/PLWRO - POLAND, SPBNX - Republika Srpska, ROBUH/ROERD/ROCLJ/ROTSR - Romania, RSBEG - Serbia, SKBTS/SKILZ/SKKSC - Slovakia, SILJV - Slovenia |Yes|No||
|China|Regarding the User Machine, We use the CN+ Machine Serial number as naming convention /// Regarding the Server . Use “CN0HKGZ12P0001” as template: The first 2 bytes indicate China MF which shall be mandatory, The 3rd byte for ITS or function team servers, The 4th to 6th bytes for city codes for China, The 7th byte for server location, The 8th and 9th bytes for server type, The 10th byte for server status, The 11th byte reserved for future attribute, The 12th to 14th bytes for server sequential numbers, from 001 to 999|Yes|No||
|CL| Workstations: CL is changing to align with CA.  CL workstations are now starting to us CLWxxxxxx |Yes|No||
|DME|Country-City-UserName/Server roll. Examples: BHMANSCCM1,EGCAISCCM01,AESHASCCM01,LBBEIAATFS01, CYLIMAAT01, KWKUWDHCP,AEABUGEMS01,EGCAIMRAMSIS,CYLIMLAP20156,CYNICLAP15359,JOAMMLABDIN|Yes|No||
|East Africa|For Kenya is (KENBI****) , for Uganda this is (UGKAM***) , For Tanzania this is  (TZDAR***)|Yes|No||
|France| PP VVV SS nc tndn: PP = Country code - 2 alphabet characters , VVV = City code - 3 characters - alphabetic - Besides cloud (AZU > Cloud Azure / AWS > Amazon Web Services / GCP > Google Cloud Platform, SS = OS Type (NT = Windows / LX = Linux / MC = MacOS / HV = Hyper-V / VW = VMware / UC = Windows Skype / AP = Applicance, nc = Application code Valeurs possibles: 1 > Database / 2 > Infrastructure / 3 > Application / 4 > Exchange / 5 > Skype / 6 > Web / 7 > Citrix / 8 > Test / 9 > Management tndn = Increment  3 numeric characters (nc hundred / nd ten / nu unit (parity depending on location)|Yes |No||
|Germany|DE<DCA/DCB><0000…1999>|Yes|No||
|India|Hostname INMUMCLOUD0377, INMUMCLOUD0378, INMUMCLOUD0379|Yes|No||
|Ireland|<country><Technology><number>, e.g., IEESXI15, IENTX01|Yes|No||
|Israel|Laptop: IL0xxxx , Servers: ILTLV|Yes|No||
|Japan|<country><city>＜Server Category(Server,Cluster,Public Cloud)><Environment (PR,Staging) etc>< Application (Web Server etc)><Number> example:  JP + TYO + S + P + WB + 0001|Yes|No||
|Korea|<KR><SEL><Number>(-vm) (e.g. KRSEL0354 or KRSEL0345-vm), <KR><SEL><HV><Number>(e.g. KRSELHV01)|Yes|No||
|Luxembourg|LULUX####|Yes|No||
|Mauritius|MUEBNXXXXXX for production and MUARXXXXXX for DR|Yes|No||
|Netherlands|NLAMSxxxxxx, NLRTDxxxxxx|Yes|No|Azure need to check|
|Nordics|Sweden: Workstations: SE+[PRODUCT ID] Example: SE5CG937659M, Servers: SE+City+Function+Last part of IP. For example: SESTOEM075 /// Denmark/Finland: dk<city><function><number> for example DKCPHDFS01|Yes|No||
|Portugal|<country><application><environment><seq number>  (ex. PTDCTP01 - PT Dcontact Production 01) Environment = P (Production), Q (Quality), D (Develpment)|Yes|No||
|South Africa|ZAJNB0500 ZA – Domain/Country (Southern and Central Africa), JNB – City – Airport Code, 0500 – Security managed Server|Yes|No||
|Turkey| < TR><CITY><Number> for example:TRIST0776|Yes|No||
|UK|<country><asset number>|Yes|No||
|West Africa|GHXXusername, NGXXusername|Yes|No||
