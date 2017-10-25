# Monarco-HAT-library-for-CODESYS
CODESYS 3 Library for Monarco HAT

The Monarco HAT was lacking a CODESYS library, so I decided to write it myself.

I am not connected with Monarco in any way, I simply wrote this library out of hobbyism and for fun. 
I decided that maybe of use for other people. Therefore, I released it under the "Unlicense" agreement.


The main library components are;
- MonarcoHAT.devdesc.xml,
- .library file,
- example .project file

Also included in the release;
- .package file (CODESYS installer) which contains all above files in a user friendly installer, together with the "unlicense" agreement.


Prerequisitories;
- A Raspberry pi with the Monarco HAT,
- CODESYS IDE with Raspberry Pi .package installed,
- CODESYS runtime component installed on pi (Demo or licensed),


Installation;
1) Either install .package via package manager, or 
2) Install the loose components via the Library / Device Repository, both found under Tools menu option in IDE.
3) ENJOY!
