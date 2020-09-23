<div align="center">

## Interprocess Communication via Semaphores


</div>

### Description

<B>New version 1.1</B><br><br>

+ <B>Added </B>IsSemaphore function to quickly test for the existence of a semaphore<br>

+ <B>Added </B>HandleSecurity feature which prevents the closing of the semaphore handle via CloseHandle<br>

+ <B>Added </B>caching of ValidateDLL result to improve speed<br>

+ <B>Started Adding</B> QueryHandleCount function; if anyone can fix it please let me know<br>

- <B>Fixed </B>logic error in getting the semaphore global state if we opened an existing semaphore on initialize call

<br><br>

---<br>

Ah, semaphores, the staple of any good operating system. I searched for a VB6 example implementing the semaphore functions and came up mostly empty-handed. This class attempts to fill that missing gap in the world of VB6 examples.

<BR><BR>

In developing this class, I initially thought it would be simple to create a global semaphore that all users would have access to. After all, the documentation states that: "<i>The semaphore name can have a "Global\" or "Local\" prefix to explicitly create the object in the global or session name space.</i>" Little did I know that I would have to delve into the depths of Windows security functions in order to actually provide *true* Global semaphore functionality. After many failed attempts, approaches and cryptic error messages (The revision level is unknown. WTF?), I believe that the infamous ACL dragon has, for our intentions at least, been slayed.

<BR><BR>

I took the advice of one Anne Gunn and implemented some additional security for our global semaphore, so rogue applications can't steal our lunch money completely.

<br><br>

The majority of the trial and error took place in finding the proper way to call and declare the security APIs. I thought I was 98% done, so I tested on XP to see if it worked there, as I figured if I could get it to work on Windows 7-64 bit, surely it would work in the UAC-less environment of XP. Well, it worked fine in the IDE, but spit out an invalid memory access error when compiled. I had gotten a similar error while testing in Windows 7 and tracked it down to using the actual struct when calling CreateSemaphore rather than the pointer. So I had to go back through each call and test to see which one needed the actual struct instead of the pointer. Turns out it was SetSecurityDescriptorDacl that needed to accept an actual SECURITY_DESCRIPTOR rather than a pointer to one. After the 2nd such discovery, I went back and used the actual structs whenever possible as a precaution.

<br><br>

The class was lightly tested on Windows 2000, XP, Vista and Windows 7. If you come across any issues or have any improvements or suggestions please let me know.

<br><br>

Credits:<br>

<a href="http://undocumented.ntinternals.net/">http://undocumented.ntinternals.net/</a> for information on the undocumented NtQuerySemaphore API function and the (also undocumented) SEMAPHORE_QUERY_STATE permission constant.

<br><br>

Anne Gunn for her excellent, thorough and well written article and accompanying code on creating a not-quite-null dacl, and explaining the benefits of doing so.<br>

<a href="http://www.codeguru.com/cpp/w-p/win32/tutorials/article.php/c4545">http://www.codeguru.com/cpp/w-p/win32/tutorials/article.php/c4545</a>

<br><br>

Matts_User_Name of the SysInternals forums for the QueryName function.<br>

<a href="http://forum.sysinternals.com/handle-name-help-ntqueryObject_topic14435_page2.html">http://forum.sysinternals.com/handle-name-help-ntqueryObject_topic14435_page2.html</a>

<br><br>

IrfanAhmad on the MSDN forums for his thread on how to share a semaphore:<br>

<a href="http://social.msdn.microsoft.com/Forums/en/windowssdk/thread/335db156-b1f7-45e2-b3d1-f0e79e386744">http://social.msdn.microsoft.com/Forums/en/windowssdk/thread/335db156-b1f7-45e2-b3d1-f0e79e386744</a>
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |2010-12-28 18:01:56
**By**             |[Joe Jordan](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/joe-jordan.md)
**Level**          |Advanced
**User Rating**    |5.0 (45 globes from 9 users)
**Compatibility**  |VB 6\.0
**Category**       |[Windows API Call/ Explanation](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/windows-api-call-explanation__1-39.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[Interproce21952212282010\.zip](https://github.com/Planet-Source-Code/joe-jordan-interprocess-communication-via-semaphores__1-73623/archive/master.zip)








