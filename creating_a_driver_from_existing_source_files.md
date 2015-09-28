<span id="vsdriver.creating_a_driver_from_existing_source_files"></span>Creating a Driver From Existing Source Files
====================================================================================================================

Starting with Windows Driver Kit (WDK) 8, the WDK is fully integrated with Microsoft Visual Studio. The WDK now uses the same compiler and build tools that you use to build Visual Studio solutions and projects. [MSBuild](%20http://go.microsoft.com/fwlink/p/?linkid=262804) replaces the Windows Build Utility (Build.exe) that was used in previous versions of the WDK (prior to WDK 8). If you have a driver that you created using a previous version of the WDK, you can easily create a Visual Studio project and solution from your existing code.

**Important**  Projects and solutions created with WDK 8 must be upgraded to work with the Windows Driver Kit (WDK) 8.1 and Microsoft Visual Studio 2013. Before you open the projects or solutions, run the [ProjectUpgradeTool](devtest.projectupgradetool). The ProjectUpgradeTool converts the projects and solutions so that they can be built using WDK 8.1.

 

The WDK provides a conversion utility that generates Visual Studio solution and project files from your driver's *sources*, *dirs*, and *makefile.inc* files. The utility creates the Visual Studio solution and project files in the same directory as your existing *sources* files. The utility does not alter your source code or your earlier build files. If you need to support your driver on Windows XP, you can continue to use the former build system for Windows XP, and use WDK 8.1 or WDK 8 and Visual Studio project and solution files for Windows 8.1, Windows 8, Windows 7, and Windows Vista.

You have the following options for creating a Visual Studio driver project from existing source files:

-   Using Visual Studio and choosing to open and convert an existing driver project (based upon *sources* and *dirs* files).
-   Using a **Visual Studio Command Prompt** window and the WDK *sources* and *dirs* file converter (Nmake2MsBuild.exe).
-   *(Recommended)* Create a new Windows driver solution in Visual Studio using one of the provided Windows driver templates. If you start with a template for your driver model, the structure of the project will be in place and the correct platform tool set will be selected. You can then add your source files to the solution. For information about selecting templates, see [Creating a New Device Function Driver](creating_a_new_driver.htm), [Creating a New Filter Driver](creating_a_new_filter_driver.htm), or [Creating a New Software Driver](creating_a_new_software_driver.htm).

![](../common/wedge.gif)**To open and convert a driver project created with a previous version of the WDK (File &gt; Open)**

1.  Open Microsoft Visual Studio Ultimate 2012. From the **File** menu, click **Open** and then click **Convert Sources/Dirs**.
2.  In the **Open** dialog box, navigate to the directory that contains the *sources* or *dirs* file for your driver, select the file and click **Open**. The Output window in Visual Studio Ultimate 2012 shows informational messages about the conversion and creation of the Visual Studio project. For a detailed view of how elements in the *sources* file were converted, you can view the conversion log (Nmake2MsBuild\_sources.log). As part of the conversion, you will asked if you want to open and view the log file.
3.  Examine the project in Solution Explorer.

    See [Additional steps if you are converting a UMDF driver](#_additional_step_umdf).

![](../common/wedge.gif)**To create a driver project from existing code (Command Line)**

1.  Open a **Visual Studio Command Prompt** window. If your project is under %PROGRAMFILES%, you need to open the command prompt window using elevated permissions (**Run as administrator**).
2.  Run the [Nmake2MsBuild](devtest.nmake2msbuild) conversion utility (Nmake2MsBuild.exe) and specify the name and path to the *sources* or *dirs* file for your driver.

    You can specify more than one *sources* files at a time. All resulting projects will share the same Solution and Package Project.

    If you run the [Nmake2MsBuild](devtest.nmake2msbuild) utility on a *dirs* file, the utility traverses the directory tree for all *sources* files and and generates Visual Studio project files for each one.

    The conversion tool is located in the %PROGRAMFILES%\\Windows Kits\\8.0\\bin\\x86\\ directory.

    For example, to generate a Visual Studio project file for an existing *sources* file in the directory C:\\Myproj, you would enter the following command:

    ``` syntax
    Nmake2MsBuild.exe  c:\myProj\sources
    ```

3.  Verify the conversion by opening the project file (\*.vcxproj) or solution file (\*.sln) in Visual Studio. Start Visual Studio and click **Open** and then navigate to the directory where you converted your *sources* file. Try building your project, using the default build configurations.

    The utility creates a log file that you can use if you need to troubleshoot or verify the converted project file. The default log file is called Nmake2MSBuild\_sources.log. The log file will report errors and warnings and will also describe how elements in the sources file were interpreted and translated to their Visual Studio project equivalents.

    See [Additional steps if you are converting a UMDF driver](#_additional_step_umdf).

### <span id="Nmake2MsBuild_Utility"></span><span id="nmake2msbuild_utility"></span><span id="NMAKE2MSBUILD_UTILITY"></span>Nmake2MsBuild Utility

The conversion tool is located in the %PROGRAMFILES%\\Windows Kits\\8.0\\bin\\x86\\ directory. For information about using the conversion utility and its options, see [Nmake2MsBuild](devtest.nmake2msbuild).

### <span id="_additional_step_umdf"></span><span id="_ADDITIONAL_STEP_UMDF"></span>Additional steps if you are converting a UMDF driver

By default, the conversion utility configures the driver package project to use kernel debugger (Debugging Tools for Windows - Kernel Debugger). If you are converting a UMDF driver to a Visual Studio solution, you should change this setting so that you can use the user-mode (Remote) debugger instead.

![](../common/wedge.gif)**To specify the user-mode (Remote) debugger**

1.  Open the property pages for your driver project. Right-click the driver package project in **Solution Explorer** and select **Properties**.
2.  In the property pages for the driver package project, click **Configuration Properties** and then click **Debugging**.
3.  From the Debugger to launch drop-down menu, select **Debugging Tools for Windows - Remote Debugging**.

For information about configuring a target computer and setting up a debug cable, see [Setting Up Kernel-Mode Debugging in Visual Studio](debugger.setting_up_kernel-mode_debugging_in_visual_studio) and [Provision a computer for driver deployment and testing (WDK 8.1)](wdkgetstart.provision_a_target_computer_wdk_8_1).

**Note**  You can still use the kernel debugger to debug UMDF drivers, but the user-mode (Remote) debugger is more convenient. If you create a UMDF driver from a UMDF template, the user-mode debugger is already selected by default.

 

<span id="related_topics"></span>Related topics
-----------------------------------------------

[WDK and the Visual Studio build environment](devtest.wdk_and_visual_studio_build_environment)
[Nmake2MsBuild](devtest.nmake2msbuild)
[ProjectUpgradeTool](devtest.projectupgradetool)
[MSBuild](%20http://go.microsoft.com/fwlink/p/?linkid=262804)
[Walkthrough: Using MSBuild](%20http://go.microsoft.com/fwlink/p/?linkid=262807)
[Creating a New Device Function Driver](creating_a_new_driver.htm)
[Creating a New Filter Driver](creating_a_new_filter_driver.htm)
[Creating a New Software Driver](creating_a_new_software_driver.htm)
 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[VsDriver\vsdriver]:%20Creating%20a%20Driver%20From%20Existing%20Source%20Files%20%20RELEASE:%20(9/24/2015)&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/en-us/default.aspx. "Send comments about this topic to Microsoft")

© 2015 Microsoft. All rights reserved.
