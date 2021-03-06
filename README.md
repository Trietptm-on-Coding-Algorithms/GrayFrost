#GrayFrost

GrayFrost is a C++ DLL delivery system for C# payloads. Once compiled, GrayFrost can be injected into .NET applications using any DLL injection technique you wish!

GrayFrost operates in two rounds, GrayFrostCpp and GrayFrostCSharp. The former is a C++ -> .NET Common Language Runtime bootstrapper. It:
	
- Creates or injects into the 4.0 runtime
- Pivot into the 2.0 runtime if needed
- Contains raw payload

Once the bootstrapping process finishes and GrayFrostCpp lands in the proper runtime version the C# payload will be executed through GrayFrostCSharp.

##Build Process:

To build GrayFrost, [AutoFrost](https://github.com/GrayKernel/AutoFrost) is recommended. This tool will auto-bundle the two byte arrays (the raw C# payload and the GrayFrostCSharp round) into the C++ DLL. There is both a GUI tool and a python script for automation. 

##Manual Build Process: 

1.) Obtain a C# byte array for your C# payload (as an executable) and place it in *GrayFrostCSharp\payload.cs* with the following syntax: 

```cs
namespace GrayFrostCSharp 
{ 
	class payload 
	{ 
 		public static byte[] g_bInjectCode = new byte[] 
		{ <BYTE ARRAY HERE> };
	}
}
```
2.) Compile GrayFrostCSharp.

3.) Obtain a C++ byte array for the GrayFrostCSharp executable and place it in *GrayFrost\slate.h* with the following syntax

```cpp
#define SIZE <SIZE HERE> 
unsigned char data[<SIZE HERE>] = { <BYTE ARRAY HERE> };
```

4.) Compile GrayFrost

5.) Inject GrayFrost{32,64} into target application. 

##Recommendations

In order to achive maximum efficiency compile your C# payload in version 2.0 of the CLR. This will ensure your payload, if universal, can be delivered into any runtime. If you know ahead of time your targets CLR version you can use that instead (2.0/4.0). Also, if wanting to target both 32/64 bit programs use the "Any CPU" option for the platform as the CLR will determine it at runtime. Again, feel free to use your targets archietcture if known.  

There is currently no support for arguments in your payloads main at this time so use a generic public static void Main(). 

##Support:

GrayFrost was built by [Topher Timzen](https://tophertimzen.com) with the help of [DigitalBodyGuard](https://www.digitalbodyguard.com/) and is currently under active support. If you have any issues or pull requests, do not hesitate to submit them.
