---
title: 'WannaCry : I want to Cry'
date: 2017-05-22T18:33:00.001-05:00
draft: false
aliases: [ "/2017/05/wannacry-i-want-to-cry.html" ]
tags : [ransomware, Facts, WannaCry, Wcrypt]
---

The ransomware that took half the wolrd by storm and surprise, crippled critical infrastucture around the world and still raging ahead : WannaCry. By now there are a lot of information available for it, a lot of things have been said about it, and a staggering amount of people have analyzed it.  
My endevours in this post will be to aggregate them, analyze some of them. Specificllay point out some of the things you, as a infected user can do to prevent further spread,and if you are already infected, a way to recover your files.

Prevention
----------

Download English language security updates: [Windows Server 2003 SP2 x64](http://download.windowsupdate.com/d/csa/csa/secu/2017/02/windowsserver2003-kb4012598-x64-custom-enu_f24d8723f246145524b9030e4752c96430981211.exe), [Windows Server 2003 SP2 x86,](http://download.windowsupdate.com/c/csa/csa/secu/2017/02/windowsserver2003-kb4012598-x86-custom-enu_f617caf6e7ee6f43abe4b386cb1d26b3318693cf.exe) [Windows XP SP2 x64](http://download.windowsupdate.com/d/csa/csa/secu/2017/02/windowsserver2003-kb4012598-x64-custom-enu_f24d8723f246145524b9030e4752c96430981211.exe), [Windows XP SP3 x86](http://download.windowsupdate.com/d/csa/csa/secu/2017/02/windowsxp-kb4012598-x86-custom-enu_eceb7d5023bbb23c0dc633e46b9c2f14fa6ee9dd.exe), [Windows XP Embedded SP3 x86](http://download.windowsupdate.com/c/csa/csa/secu/2017/02/windowsxp-kb4012598-x86-embedded-custom-enu_8f2c266f83a7e1b100ddb9acd4a6a3ab5ecd4059.exe), [Windows 8 x86,](http://download.windowsupdate.com/c/msdownload/update/software/secu/2017/05/windows8-rt-kb4012598-x86_a0f1c953a24dd042acc540c59b339f55fb18f594.msu) [Windows 8 x64](http://download.windowsupdate.com/c/msdownload/update/software/secu/2017/05/windows8-rt-kb4012598-x64_f05841d2e94197c2dca4457f1b895e8f632b7f8e.msu)

Recovery Information
--------------------

If you are already infected with the ransomware, then your best bet is to try these tools. These are proven to work in Windows Xp - 7. You have to be running a **x86** version of windows for these to work. They try to extract the prime number generated in the memorey and recreate the private key for decryption. So in short, **run the tools ASAP and do not restart the machine.  
**

1.  **D**[**ownload wanakiwi here**](https://github.com/gentilkiwi/wanakiwi/releases)
2.  wanakiwi.exe will **automatically** look for the _00000000.pky_ file.
3.  Cross fingers that your prime numbers haven’t been overwritten from the process address space.

Courtesy: Kudos to the French security researchers [Adrien Guinet](https://twitter.com/adriengnt) and [Benjamin Delpy (@gentilkiwi)](https://twitter.com/gentilkiwi)for their fantastic work.

### More information:

*   **Virus Name**: WannaCrypt, WannaCry, WanaCrypt0r, WCrypt, WCRY
*   **Vector**: All Windows versions before Windows 10 are vulnerable if not patched for MS-17-010. It uses EternalBlue MS17-010 to propagate.
*   **Ransom**: between $300 to $600. There is code to 'rm' (delete) files in the virus. Seems to reset if the virus crashes.
*   **Backdooring**: The worm loops through every RDP session on a system to run the ransomware as that user. It also installs the DOUBLEPULSAR backdoor. It corrupts shadow volumes to make recovery harder. (source: malwarebytes)
*   **Kill switch**: If the website `www.iuqerfsodp9ifjaposdfjhgosurijfaewrwergwea.com` is up the virus exits instead of infecting the host. (source: malwarebytes). This domain has been sinkholed, stopping the spread of the worm. Will not work if proxied ([source](https://blog.didierstevens.com/2017/05/13/quickpost-wcry-killswitch-check-is-not-proxy-aware/)).

_update_: A minor variant of the virus has been found, it looks to have had the killswitch hexedited out. Not done by recompile so probably not done by the original malware author. On the other hand that is the only change: the encryption keys are the same, the bitcoin addresses are the same. On the other hand it is corrupt so the ransomware aspect of it doesn't work - it only propagates.

SECURITY BULLETIN AND UPDATES HERE: https://technet.microsoft.com/en-us/library/security/ms17-010.aspx

Microsoft first patch for XP since 2014: https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/

Killswitch source: https://blog.malwarebytes.com/threat-analysis/2017/05/the-worm-that-spreads-wanacrypt0r/ https://www.malwaretech.com/2017/05/how-to-accidentally-stop-a-global-cyber-attacks.html

Exploit details: https://zerosum0x0.blogspot.com/2017/04/doublepulsar-initial-smb-backdoor-ring.html

Vulnerable/Not Vulnerable
-------------------------

To be infected requires the SMB port (445) to be open, or the machine already infected with DOUBLEPULSAR (and killswitch not registered or somehow blocked, or the network accessing it through a proxy).

The MS17-010 patch fixes the vulnerability.

*   Windows XP: Doesn't spread. If run manually, can encrypt files.
*   Windows 7,8,2008: can spread unpatched, can encrypt files.
*   Windows 10: Doesn't spread. Even though Windows 10 [does have the faulty SMB driver](http://www.infoworld.com/article/3196825/microsoft-windows/how-to-make-sure-your-windows-pc-wont-get-hit-by-ransomware-like-wannacrypt.html).
*   Linux: Doesn't spread. If run manually with wine, can encrypt files.

Infections
----------

Till today

![](https://lh3.googleusercontent.com/-xT_YnCtR7fQ/WSN1LtUMx9I/AAAAAAABVEY/FhL1adnGpg8rrVegpicGrSkf2lHkQAVWACHM/s9999/Screen-Shot-2017-05-22-at-4.26.04-PM.png)

*   NHS (uk) turning away patients, unable to perform x-rays. ([list of affected hospitals](http://news.sky.com/story/nhs-cyberattack-full-list-of-organisations-affected-so-far-10874493))
*   Nissan (uk) http://www.chroniclelive.co.uk/news/north-east-news/cyber-attack-nhs-latest-news-13029913
*   Telefonica (spain) (https://twitter.com/SkyNews/status/863044193727389696)
*   power firm Iberdrola and Gas Natural ([spain](http://www.bbc.co.uk/news/technology-39901382))
*   FedEx (us) (https://twitter.com/jeancreed1/status/863089728253505539)
*   University of Waterloo ([ontario canada](https://twitter.com/amtinits))
*   Russia interior ministry & Megafon (russia) https://twitter.com/dabazdyrev/status/863034199460261890/photo/1
*   VTB (russian bank) https://twitter.com/vassgatov/status/863175506790952962
*   Russian Railroads (RZD) https://twitter.com/vassgatov/status/863175723846176768
*   [Portugal Telecom](http://imgur.com/a/rR3b9)
*   Сбербанк - Sberbank Russia ([russia](https://twitter.com/discojournalist/status/863162464304865280))
*   Shaheen Airlines (pakistan, [claimed on twitter](https://twitter.com/Beyhooda/status/863161471987068930))
*   Train station in frankfurt ([germany](https://twitter.com/Nick_Lange_/status/863132237822394369))
*   Neustadt station ([germany](https://twitter.com/MedecineLibre/status/863139139138531328))
*   the entire network of German Rail seems to be affected ([@farbenstau](https://twitter.com/farbenstau/status/863166384834064384))
*   in China secondary schools and universities had been affected ([source](http://english.alarabiya.net/en/News/world/2017/05/13/Russia-s-interior-ministry-says-computers-hit-by-virus-attack-.html))
*   A Library in Oman ([@99arwan1](https://twitter.com/99arwan1/status/863325279653171200))
*   China Yanshui County Public Security Bureau (https://twitter.com/95cnsec/status/863292545278685184)
*   Renault (France) (http://www.lepoint.fr/societe/renault-touche-par-la-vague-de-cyberattaques-internationales-13-05-2017-2127044\_23.php) (http://www.lefigaro.fr/flash-eco/2017/05/13/97002-20170513FILWWW00031-renault-touche-par-la-vague-de-cyberattaques-internationales.php)
*   Schools/Education (France) https://twitter.com/Damien\_Bancal/status/863305670568837120
*   University of Milano-Bicocca ([italy](http://milano.repubblica.it/cronaca/2017/05/12/news/milano_virus_ransomware_universita_bicocca-165302056/?ref=drnweb.repubblica.scroll-3))
*   A mall in singapore https://twitter.com/nkl0x55/status/863340271391580161
*   ATMs in china https://twitter.com/95cnsec/status/863382193615159296
*   norwegian soccer team ticket sales https://www.nrk.no/telemark/eliteserieklubber-rammet-av-internasjonalt-dataangrep-1.13515245
*   STC telecom ([saudia arabia](https://twitter.com/iPhone_Supp/status/863735059819442177), [more](https://twitter.com/mhooh300/status/863734116142985216), [more](https://twitter.com/bynfck/status/863734011188854784))
*   [All ATMs in india closed](http://newsable.asianetnews.tv/india/over-2-lakh-atms-in-the-country-to-remain-closed-to-deal-with-cyberattack)
*   US radiology equipment https://twitter.com/Forbes/status/864850749225934852
*   More at https://en.wikipedia.org/wiki/WannaCry\_cyber\_attack#List\_of\_affected\_organizations they seem to be cataloguing the infections faster/better.

Malware samples
---------------

*   hxxps://www.hybrid-analysis.com/sample/ed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa?environmentId=100
*   hxxps://transfer.sh/PnDIl/CYBERed01ebfbc9eb5bbea545af4d01bf5f1071661840480439c6e5babe8e080e41aa.EXE
*   hxxps://transfer.sh/ZhnxR/CYBER1be0b96d502c268cb40da97a16952d89674a9329cb60bac81a96e01cf7356830.EXE (main dll)

Binary blob in PE crypted with pass 'WNcry@2ol7', credits to ens!

*   parents https://pastebin.com/quvVH5hS (all known variants of the Wcry launcher containing eternalblue)
*   children https://pastebin.com/A2pxw49F (all variants of Wcry, the actual ransomware, being currently observed in the wild)

essentially the full known catalogue of samples. credit to errantbot and @codexgigassys

Informative Tweets
------------------

*   Sample released by ens: https://twitter.com/the\_ens/status/863055007842750465
*   Onion C&Cs extracted: https://twitter.com/the\_ens/status/863069021398339584
*   EternalBlue confirmed: https://twitter.com/kafeine/status/863049739583016960
*   Shell commands: https://twitter.com/laurilove/status/863065599919915010
*   Maps/stats: https://twitter.com/laurilove/status/863066699888824322
*   Core DLL: https://twitter.com/laurilove/status/863072240123949059
*   Hybrid-analysis: https://twitter.com/PayloadSecurity/status/863024514933956608
*   Impact assessment: https://twitter.com/CTIN\_Global/status/863095852113571840
*   Uses DoublePulsar: https://twitter.com/laurilove/status/863107992425779202
*   Your machine is attacking others: https://twitter.com/hackerfantastic/status/863105127196106757
*   Tor hidden service C&C: https://twitter.com/hackerfantastic/status/863105031167504385
*   FedEx infected via Telefonica? https://twitter.com/jeancreed1/status/863089728253505539
*   HOW TO AVOID INFECTION: https://twitter.com/hackerfantastic/status/863070063536091137
*   More of this to come: https://twitter.com/hackerfantastic/status/863069142273929217
*   C&C hosts: https://twitter.com/hackerfantastic/status/863115568181850113
*   Crypted files _will_ be deleted after countdown: https://twitter.com/laurilove/status/863116900829724672
*   Claim of attrib \[take with salt\]: https://twitter.com/0xSpamTech/status/863058605473509378
*   Track the bitcoins: https://twitter.com/bl4sty/status/863143484919828481
*   keys in pem format: https://twitter.com/e55db081d05f58a/status/863109716456747008
*   neel points out a similarity with another virus https://twitter.com/neelmehta/status/864164081116225536
*   shadowbrokers talk about responsible disclosure https://steemit.com/shadowbrokers/@theshadowbrokers/oh-lordy-comey-wanna-cry-edition
*   another factsheet https://www.secureworks.com/research/wcry-ransomware-analysis

Cryptography details
--------------------

*   Each infection generates a new RSA-2048 keypair.
*   The public key is exported as blob and saved to 00000000.pky
*   The private key is encrypted with the ransomware public key and saved as 00000000.eky
*   Each file is encrypted using AES-128-CBC, with a unique AES key per file.
*   Each AES key is generated CryptGenRandom.
*   The AES key is encrypted using the infection specific RSA keypair.

The RSA public key used to encrypt the infection specific RSA private key is embedded inside the DLL and owned by the ransomware authors.

*   https://haxx.in/key1.bin (the ransomware pubkey, used to encrypt the users private key)
*   https://haxx.in/key2.bin (the dll decryption privkey)  
    the CryptImportKey() rsa key blob dumped from the DLL by blasty.

https://pastebin.com/aaW2Rfb6 even more in depth RE information by cyg\_x1!!

Bitcoin ransom addresses
------------------------

3 addresses hard coded into the malware.

*   https://blockchain.info/address/13AM4VW2dhxYgXeQepoHkHSQuy6NgaEb94
*   https://blockchain.info/address/12t9YDPgwueZ9NyMgw519p7AA8isjr6SMw
*   https://blockchain.info/address/115p7UMMngoj1pMvkpHijcRdfJNXj6LrLn

C&C centers
-----------

*   `gx7ekbenv2riucmf.onion`
*   `57g7spgrzlojinas.onion`
*   `xxlvbrloxvriy2c5.onion`
*   `76jdd2ir2embyv47.onion`
*   `cwwnhwhlz52maqm7.onion`

Languages
---------

All language ransom messages available here: https://transfer.sh/y6qco/WANNACRYDECRYPTOR-Ransomware-Messages-all-langs.zip

m\_bulgarian, m\_chinese (simplified), m\_chinese (traditional), m\_croatian, m\_czech, m\_danish, m\_dutch, m\_english, m\_filipino, m\_finnish, m\_french, m\_german, m\_greek, m\_indonesian, m\_italian, m\_japanese, m\_korean, m\_latvian, m\_norwegian, m\_polish, m\_portuguese, m\_romanian, m\_russian, m\_slovak, m\_spanish, m\_swedish, m\_turkish, m\_vietnamese

File types
----------

There are a number of files and folders wannacrypt will avoid. Some because it's entirely pointless and others because it might destabilize the system. During scans, it will search the path for the following strings and skip over if present:

*   "Content.IE5"
*   "Temporary Internet Files"
*   " This folder protects against ransomware. Modifying it will reduce protection"
*   "\\Local Settings\\Temp"
*   "\\AppData\\Local\\Temp"
*   "\\Program Files (x86)"
*   "\\Program Files"
*   "\\WINDOWS"
*   "\\ProgramData"
*   "\\Intel"
*   "{0}quot;

The filetypes it looks for to encrypt are:

.doc, .docx, .xls, .xlsx, .ppt, .pptx, .pst, .ost, .msg, .eml, .vsd, .vsdx, .txt, .csv, .rtf, .123, .wks, .wk1, .pdf, .dwg, .onetoc2, .snt, .jpeg, .jpg, .docb, .docm, .dot, .dotm, .dotx, .xlsm, .xlsb, .xlw, .xlt, .xlm, .xlc, .xltx, .xltm, .pptm, .pot, .pps, .ppsm, .ppsx, .ppam, .potx, .potm, .edb, .hwp, .602, .sxi, .sti, .sldx, .sldm, .sldm, .vdi, .vmdk, .vmx, .gpg, .aes, .ARC, .PAQ, .bz2, .tbk, .bak, .tar, .tgz, .gz, .7z, .rar, .zip, .backup, .iso, .vcd, .bmp, .png, .gif, .raw, .cgm, .tif, .tiff, .nef, .psd, .ai, .svg, .djvu, .m4u, .m3u, .mid, .wma, .flv, .3g2, .mkv, .3gp, .mp4, .mov, .avi, .asf, .mpeg, .vob, .mpg, .wmv, .fla, .swf, .wav, .mp3, .sh, .class, .jar, .java, .rb, .asp, .php, .jsp, .brd, .sch, .dch, .dip, .pl, .vb, .vbs, .ps1, .bat, .cmd, .js, .asm, .h, .pas, .cpp, .c, .cs, .suo, .sln, .ldf, .mdf, .ibd, .myi, .myd, .frm, .odb, .dbf, .db, .mdb, .accdb, .sql, .sqlitedb, .sqlite3, .asc, .lay6, .lay, .mml, .sxm, .otg, .odg, .uop, .std, .sxd, .otp, .odp, .wb2, .slk, .dif, .stc, .sxc, .ots, .ods, .3dm, .max, .3ds, .uot, .stw, .sxw, .ott, .odt, .pem, .p12, .csr, .crt, .key, .pfx, .der

credit herulume, thanks for extracting this list from the binary.

more details came from https://pastebin.com/xZKU7Ph1 thanks to cyg\_x11

Some other interesting strings
------------------------------

*   BAYEGANSRV\\administrator
*   Smile465666SA
*   wanna18@hotmail.com

credit: nulldot https://pastebin.com/0LrH05y2

Encrypted file format
---------------------

```
typedef struct _wc_file_t {  
    char     sig[WC_SIG_LEN]     // 64 bit signature WANACRY!  
    uint32_t keylen;             // length of encrypted key  
    uint8_t  key[WC_ENCKEY_LEN]; // AES key encrypted with RSA  
    uint32_t unknown;            // usually 3 or 4, unknown  
    uint64_t datalen;            // length of file before encryption, obtained from GetFileSizeEx  
    uint8_t *data;               // Ciphertext Encrypted data using AES-128 in CBC mode  
} wc_file_t;  
  

```

credit for reversing this file format info: cyg\_x11.

Vulnerability disclosure
------------------------

The specific vulnerability that it uses to propagate is ETERNALBLUE.

This was developed by "equation group" an exploit developer group associated with the NSA and leaked to the public by "the shadow brokers". Microsoft fixed this vulnerability March 14, 2017. They were not 0 days at the time of release.

*   https://blogs.technet.microsoft.com/msrc/2017/04/14/protecting-customers-and-evaluating-risk/
*   https://technet.microsoft.com/en-us/library/security/ms17-010.aspx