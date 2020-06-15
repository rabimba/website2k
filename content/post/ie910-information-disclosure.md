---
title: 'IE9/10 information disclosure vulnerability'
date: 2013-07-29T11:43:00.001-05:00
draft: false
aliases: [ "/2013/07/ie910-information-disclosure.html" ]
---

IE memory garbage collection ( Mark Sweep algorithm ) object address leak vulnerability

  

Information disclosure, Windows IE9/10

  

Description:

  

Since IE9, Javascript date uses 1 bit to mark \***num**\* and \***object**\* pointer. However, in most object structures, there are data field that does not use the bit to mark. IE Mark Sweep algorithm JSCRIPT9!Recycler::ProcessMark will mark the object in the structure. Because this is a general class, it cannot process correctly the num in the object structure that does not have the marked bit. Therefore, JSCRIPT9!Recycler::ProcessMark will wrongly think these num are object pointers and mark the wrong tag. This will cause some objects cannot be released correctly, and may also leak the object address to bypass ASLR. If the garbaby collection contains the code to \***defrag**\* memory blocks, it might lead to potential more serious issues such as buffer overrun due to the incorrect operation of the object pointers (which should be a num).

Details：

  

  

gc.html:

  

    </span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var myarray = new Array(0x12340);</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; myarray\[0\]=1;</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;alert("begin!");</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; JSON.stringify(new Array(0x100000));</span><span style="color: black;"></span></p><p style="margin: 0cm 0cm 0pt; padding: 0px; color: rgb(69, 69, 69); font-family: tahoma, helvetica, arial; font-size: 14px; line-height: 21px; background-color: rgb(255, 255, 255);"><span style="font-size: 10pt; font-family: 'Courier New'; color: black;">&nbsp;&nbsp;&nbsp;

  

  

  

Poc creates an object array. Alert is for tracking. JSON.stringify allocates lots of memory to trigger gc. Observe how gc handles object array.

  

Object array process code:

  

0:008:x86> u JSCRIPT9!Js::JavascriptArray::NewInstance

JSCRIPT9!Js::JavascriptArray::NewInstance:

63138d83 8bff            mov     edi,edi

63138d85 55              push    ebp

63138d86 8bec            mov     ebp,esp

63138d88 83e4f8          and     esp,0FFFFFFF8h

63138d8b 83ec1c          sub     esp,1Ch

63138d8e 53              push    ebx

63138d8f 56              push    esi

63138d90 8b7508          mov     esi,dword ptr \[ebp+8\]

63138d93 8b4e04          mov     ecx,dword ptr \[esi+4\]

63138d96 8b4104          mov     eax,dword ptr \[ecx+4\]

63138d99 57              push    edi

63138d9a 8b7804          mov     edi,dword ptr \[eax+4\]

63138d9d 8b8f34020000    mov     ecx,dword ptr \[edi+234h\]

63138da3 ba00040000      mov     edx,400h

63138da8 e8ac00f7ff      call    JSCRIPT9!ThreadContext::IsStackAvailable (630a8

e59)

63138dad 84c0            test    al,al

63138daf 0f84b77b0c00    je      JSCRIPT9!Js::JavascriptArray::NewInstance+0x37e

(6320096c)

63138db5 8b450c          mov     eax,dword ptr \[ebp+0Ch\]

63138db8 a900000008      test    eax,8000000h

63138dbd 0f85ba1a1c00    jne     JSCRIPT9!memset+0x31b37 (632fa87d)

63138dc3 25ffffff00      and     eax,0FFFFFFh

63138dc8 83f802          cmp     eax,2

63138dcb 0f82f9000000    jb      JSCRIPT9!Js::JavascriptArray::NewInstance+0x18a

(63138eca)

63138dd1 0f854d030000    jne     JSCRIPT9!Js::JavascriptArray::NewInstance+0x27f

(63139124)

63138dd7 8b5d14          mov     ebx,dword ptr \[ebp+14h\]

63138dda f6c301          test    bl,1

63138ddd 0f84fc1a1c00    je      JSCRIPT9!memset+0x31b98 (632fa8df)

63138de3 d1fb            sar     ebx,1

63138de5 8b4604          mov     eax,dword ptr \[esi+4\]

63138de8 0f88c91a1c00    js      JSCRIPT9!memset+0x31b71 (632fa8b7)

63138dee 8b7804          mov     edi,dword ptr \[eax+4\]

63138df1 68fc760a63      push    offset JSCRIPT9!Recycler::Alloc (630a76fc)

63138df6 ff770c          push    dword ptr \[edi+0Ch\]

63138df9 6a20            push    20h

63138dfb e86fe9f6ff      call    JSCRIPT9!operator new (630a776f)

63138e00 8bf0            mov     esi,eax

63138e02 83c40c          add     esp,0Ch

63138e05 85f6            test    esi,esi

63138e07 0f843b43feff    je      JSCRIPT9!Js::JavascriptArray::NewInstance+0x3a8

63138e73 8b4604          mov     eax,dword ptr \[esi+4\]

63138e76 c706c82d0a63    mov     dword ptr \[esi\],offset JSCRIPT9!Js::JavascriptA

rray::\`vftable' (630a2dc8)

63138e7c c7461c00000000  mov     dword ptr \[esi+1Ch\],0

63138e83 8b4004          mov     eax,dword ptr \[eax+4\]

63138e86 8b4004          mov     eax,dword ptr \[eax+4\]

63138e89 8b9064040000    mov     edx,dword ptr \[eax+464h\]

63138e8f 895e10          mov     dword ptr \[esi+10h\],ebx

63138e92 85db            test    ebx,ebx

  

  

  

  

0:008:x86> g  63138e76

Breakpoint 1 hit

JSCRIPT9!Js::JavascriptArray::NewInstance+0xf3:

63138e76 c706c82d0a63    mov     dword ptr \[esi\],offset JSCRIPT9!Js::JavascriptA

rray::\`vftable' (630a2dc8) ds:002b:05384580={JSCRIPT9!Js::DynamicObject::\`vftabl

e' (630a27d8)}

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0xf9:

63138e7c c7461c00000000  mov     dword ptr \[esi+1Ch\],0 ds:002b:0538459c=00000000

  

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0x100:

63138e83 8b4004          mov     eax,dword ptr \[eax+4\] ds:002b:05388aa4=00b0fb03

  

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0x103:

63138e86 8b4004          mov     eax,dword ptr \[eax+4\] ds:002b:03fbb004=98a9b502

  

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0x106:

63138e89 8b9064040000    mov     edx,dword ptr \[eax+464h\] ds:002b:02b5adfc=f0b1b

502

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0x10c:

63138e8f 895e10          mov     dword ptr \[esi+10h\],ebx ds:002b:05384590=000000

00

0:008:x86> t

JSCRIPT9!Js::JavascriptArray::NewInstance+0x10f:

63138e92 85db            test    ebx,ebx

  

  

0:008:x86> d esi l 20

05384580  c8 2d 0a 63 a0 8a 38 05-00 00 00 00 03 00 00 00  .-.c..8.........

05384590  40 23 01 00 00 00 00 00-00 00 00 00 00 00 00 00  @#..............

  

0:008:x86> u poi(esi)

JSCRIPT9!Js::JavascriptArray::\`vftable':

630a2dc8 89750a          mov     dword ptr \[ebp+0Ah\],esi

630a2dcb 6389750a6389    arpl    word ptr \[ecx-769CF58Bh\],cx

630a2dd1 750a            jne     JSCRIPT9!Js::JavascriptArray::\`vftable'+0x15 (6

30a2ddd)

630a2dd3 63857d0a637a    arpl    word ptr \[ebp+7A630A7Dh\],ax

630a2dd9 2028            and     byte ptr \[eax\],ch

630a2ddb 63642028        arpl    word ptr \[eax+28h\],sp

630a2ddf 634312          arpl    word ptr \[ebx+12h\],ax

630a2de2 1963a2          sbb     dword ptr \[ebx-5Eh\],esp

0:008:x86> u poi(poi(esi))

JSCRIPT9!JsUtil::BackgroundJobProcessor::AssociatePageAllocator:

630a7589 c20400          ret     4

  

Esi is the pointer of object array. 0x630a2dc8 points to vtable Js::JavascriptArray::\`vftable'

  

poi(esi+0x10) is the array length, which can be controlled by the attacker. We can see later that in GC’s collection algorithm, it marks the entire objects when doing marking, instead of check details inside object layout.

  

  

  

0:008:x86> ba r4 esi

0:008:x86> ba r4 esi+10

  

Set breakpoint of array object vtable and length, run g, ignore intermediate breakpoint till alert pops up.

  

You can see GC algorithm try to mark the vtable and length and other num values to be object type.

  

  

Breakpoint 0 hit

JSCRIPT9!Recycler::ProcessMark+0x82:

631026b5 895c2418        mov     dword ptr \[esp+18h\],ebx ss:002b:07e0f9d8=d01f03

01

  

GC algorithm reads the vtable pointer

  

0:017:x86> u eip-4

JSCRIPT9!Recycler::ProcessMark+0x79:

631026b1 8bc3            mov     eax,ebx

631026b3 8b1f            mov     ebx,dword ptr \[edi\]

631026b5 895c2418        mov     dword ptr \[esp+18h\],ebx

631026b9 81fb00000100    cmp     ebx,10000h

631026bf 726b            jb      JSCRIPT9!Recycler::ProcessMark+0xf9 (6310272c)

631026c1 f7c30f000000    test    ebx,0Fh

631026c7 7563            jne     JSCRIPT9!Recycler::ProcessMark+0xf9 (6310272c)

631026c9 8bc3            mov     eax,ebx

  

  

0:017:x86> d edi l 20

05384580  c8 2d 0a 63 a0 8a 38 05-00 00 00 00 03 00 00 00

05384590  40 23 01 00 10 00 e9 02-10 00 e9 02 00 00 00 00

  

You can see Recycler::ProcessMark now handle the object array

  

  

  

  

  

0:017:x86> g

Breakpoint 1 hit

JSCRIPT9!Recycler::ProcessMark+0x82:

631026b5 895c2418        mov     dword ptr \[esp+18h\],ebx ss:002b:07e0f9d8=030000

00

0:017:x86> r

eax=053845a0 ebx=00012340 ecx=02b5b1f0 edx=00000400 esi=02ba3660 edi=05384590

eip=631026b5 esp=07e0f9c0 ebp=07e0f9f0 iopl=0         nv up ei ng nz na pe cy

cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000287

JSCRIPT9!Recycler::ProcessMark+0x82:

631026b5 895c2418        mov     dword ptr \[esp+18h\],ebx ss:002b:07e0f9d8=030000

00

  

Continue, GC algorithm processes the array length field which is totally controlled by the attacker.

  

Analyze Recycler::ProcessMark：

  

Check if it is object pointer (〉0x10000, lower 4 bit is 0). If it is object pointer, check list till the mark table of the object and mark the object. If it is marked, then it means there are pending references so the sweep would release the object.

  

  

0:017:x86> u JSCRIPT9!Recycler::ProcessMark

JSCRIPT9!Recycler::ProcessMark:

63102638 8bff            mov     edi,edi

6310263a 55              push    ebp

6310263b 8bec            mov     ebp,esp

6310263d 83e4f8          and     esp,0FFFFFFF8h

63102640 83ec24          sub     esp,24h

63102643 807d0c00        cmp     byte ptr \[ebp+0Ch\],0

63102647 53              push    ebx

63102648 56              push    esi

63102649 57              push    edi

6310264a 0f859e210000    jne     JSCRIPT9!Recycler::ProcessMark+0x42b (631047ee)

63102650 f6058053336320  test    byte ptr \[JSCRIPT9!Microsoft\_JScriptEnableBits

(63335380)\],20h

63102657 0f85e99a1000    jne     JSCRIPT9!memset+0x15667 (6320c146)

6310265d 8b4d08          mov     ecx,dword ptr \[ebp+8\]

63102660 8b99506f0000    mov     ebx,dword ptr \[ecx+6F50h\]

63102666 895c242c        mov     dword ptr \[esp+2Ch\],ebx

6310266a 8b81306f0000    mov     eax,dword ptr \[ecx+6F30h\]

63102670 85c0            test    eax,eax

63102672 0f8408010000    je      JSCRIPT9!Recycler::ProcessMark+0x1a8 (63102780)

63102678 8b91286f0000    mov     edx,dword ptr \[ecx+6F28h\]

6310267e 3bd0            cmp     edx,eax

63102680 0f84ee000000    je      JSCRIPT9!Recycler::ProcessMark+0x19c (63102774)

63102686 8b4208          mov     eax,dword ptr \[edx+8\]

63102689 8b78f8          mov     edi,dword ptr \[eax-8\]

6310268c 8b70fc          mov     esi,dword ptr \[eax-4\]

6310268f 8bc2            mov     eax,edx

63102691 834008f8        add     dword ptr \[eax+8\],0FFFFFFF8h

63102695 8b91286f0000    mov     edx,dword ptr \[ecx+6F28h\]

6310269b 8d4210          lea     eax,\[edx+10h\]

6310269e 394208          cmp     dword ptr \[edx+8\],eax

631026a1 0f84e6350000    je      JSCRIPT9!Recycler::ProcessMark+0x2f1 (63105c8d)

631026a7 c1ee02          shr     esi,2

631026aa 8d1cb7          lea     ebx,\[edi+esi\*4\]

631026ad 895c2410        mov     dword ptr \[esp+10h\],ebx

631026b1 8bc3            mov     eax,ebx

  

631026b3 8b1f            mov     ebx,dword ptr \[edi\]

631026b5 895c2418        mov     dword ptr \[esp+18h\],ebx

631026b9 81fb00000100    cmp     ebx,10000h

631026bf 726b            jb      JSCRIPT9!Recycler::ProcessMark+0xf9 (6310272c)

  

/\*

  > 0x10000

\*/

631026c1 f7c30f000000    test    ebx,0Fh

631026c7 7563            jne     JSCRIPT9!Recycler::ProcessMark+0xf9 (6310272c)

/\*

  Lower 4 bit is not 0?，object pointer

\*/

631026c9 8bc3            mov     eax,ebx

631026cb c1e814          shr     eax,14h

631026ce 8bb481bc000000  mov     esi,dword ptr \[ecx+eax\*4+0BCh\]

631026d5 85f6            test    esi,esi

631026d7 0f84c3000000    je      JSCRIPT9!Recycler::ProcessMark+0x195 (631027a0)

/\*

  Level-1 table

  

\*/

631026dd 8bc3            mov     eax,ebx

631026df c1e80c          shr     eax,0Ch

631026e2 25ff000000      and     eax,0FFh

0:017:x86> u

JSCRIPT9!Recycler::ProcessMark+0xb4:

631026e7 8b748604        mov     esi,dword ptr \[esi+eax\*4+4\]

631026eb 89742414        mov     dword ptr \[esp+14h\],esi

631026ef 85f6            test    esi,esi

631026f1 7435            je      JSCRIPT9!Recycler::ProcessMark+0xf5 (63102728)

  

/\*

  Level-2 table

\*/

  

631026f3 0fbf4604        movsx   eax,word ptr \[esi+4\]

631026f7 83f801          cmp     eax,1

631026fa 7540            jne     JSCRIPT9!Recycler::ProcessMark+0x1c8 (6310273c)

/\*

  Object pool type？

\*/

  

631026fc 8bc3            mov     eax,ebx

631026fe c1e804          shr     eax,4

63102701 25ff000000      and     eax,0FFh

63102706 8bc8            mov     ecx,eax

63102708 83e11f          and     ecx,1Fh

6310270b ba01000000      mov     edx,1

63102710 89442428        mov     dword ptr \[esp+28h\],eax

63102714 d3e2            shl     edx,cl

63102716 c1e805          shr     eax,5

63102719 8d0486          lea     eax,\[esi+eax\*4\]

6310271c 855038          test    dword ptr \[eax+38h\],edx

6310271f 0f840d050000    je      JSCRIPT9!Recycler::ProcessMark+0x109 (63102c32)

63102725 8b4d08          mov     ecx,dword ptr \[ebp+8\]

  

63102728 8b442410        mov     eax,dword ptr \[esp+10h\]

6310272c 83c704          add     edi,4

/\*

  Next pointer

\*/

6310272f 3bf8            cmp     edi,eax

63102731 7580            jne     JSCRIPT9!Recycler::ProcessMark+0x80 (631026b3)

0:017:x86> u

JSCRIPT9!Recycler::ProcessMark+0x100:

63102733 8b5c242c        mov     ebx,dword ptr \[esp+2Ch\]

63102737 e92effffff      jmp     JSCRIPT9!Recycler::ProcessMark+0x32 (6310266a)

  

6310273c 83e802          sub     eax,2

6310273f 0f8557040000    jne     JSCRIPT9!Recycler::ProcessMark+0x25b (63102b9c)

63102745 c1eb04          shr     ebx,4

63102748 81e3ff000000    and     ebx,0FFh

6310274e 0fb7c3          movzx   eax,bx

63102751 8bc8            mov     ecx,eax

63102753 83e11f          and     ecx,1Fh

63102756 ba01000000      mov     edx,1

6310275b d3e2            shl     edx,cl

6310275d 8b4d08          mov     ecx,dword ptr \[ebp+8\]

63102760 c1e805          shr     eax,5

63102763 8d0486          lea     eax,\[esi+eax\*4\]

63102766 855038          test    dword ptr \[eax+38h\],edx

63102769 75bd            jne     JSCRIPT9!Recycler::ProcessMark+0xf5 (63102728)

6310276b 095038          or      dword ptr \[eax+38h\],edx

/\*

  mark

\*/

6310276e 66ff462c        inc     word ptr \[esi+2Ch\]

63102772 ebb4            jmp     JSCRIPT9!Recycler::ProcessMark+0xf5 (63102728)

  

  

  

0:017:x86> u  63102c32

JSCRIPT9!Recycler::ProcessMark+0x109:

63102c32 095038          or      dword ptr \[eax+38h\],edx

  

/\*

  mark

\*/

  

63102c35 66ff462c        inc     word ptr \[esi+2Ch\]

63102c39 8b4c2428        mov     ecx,dword ptr \[esp+28h\]

63102c3d 8b461c          mov     eax,dword ptr \[esi+1Ch\]

63102c40 0fb70448        movzx   eax,word ptr \[eax+ecx\*2\]

63102c44 8a843088000000  mov     al,byte ptr \[eax+esi+88h\]

63102c4b 0fb74e24        movzx   ecx,word ptr \[esi+24h\]

63102c4f 8844240f        mov     byte ptr \[esp+0Fh\],al

  

  

Other objects, the object reference area inside object such as the value of the array, during object’s own processing, it would mark the lower bits of these values to be object pointer (last bit 0) or num (last bit 1). However, object itself does not differentiate the object reference area and internal member. GC mark algorithm mistakenly marks the object internal member as object type. The attacker can control directly or indirectly the object member variable, via Fuzz, so that GC will not mark correctly. This will cause some objects cannot be released correctly, and may also leak the object address to bypass ASLR. If the garbaby collection contains the code to \***defrag**\* memory blocks, it might lead to potential more serious issues such as buffer overrun due to the incorrect operation of the object pointers.