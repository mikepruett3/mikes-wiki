# [PowerShell Scripting Best Practices](https://blogs.technet.microsoft.com/pstips/2014/06/17/powershell-scripting-best-practices/)

For the past few years, I’ve picked up a several best practices for PowerShell scripting. Some of them are “borrowed” from Ed Wilson (aka the Microsoft Scripting Guy), Don Jones, and other PowerShell MVPs and PFEs @ Microsoft.

Note: For more PowerShell best practices, check the **PowerShellPracticeAndStyle** github repository

1. Start your scripts with a standard set of comments (name, date, author, purpose and keywords) to easily find them later.
2. Add comments as much as possible, but not too much.
3. Use the **[#Requires](http://technet.microsoft.com/en-us/library/hh847765)** tag for the minimum version of Windows PowerShell required, required Modules, PSSnapin or Administrative rights.
4. Use the **[Set-StrictMode](http://technet.microsoft.com/en-us/library/hh849692) -Version Latest** command to ensure that you cannot reference things such as  uninitialized variables and non-existent properties of an object.
5. Use simple but meaningful variable names. **[camelCase](https://en.wikipedia.org/wiki/Camel_case)** is the best practice. (e.g. $serviceName or $counterName, and not $s and $c). Note that this is for variables inside a script or function, not for parameter names (see #17 for parameter names best practices).
6. Place user-defined variables at the top of script. It makes it easier for you or anyone making changes to those script variables.
7. Use code signing (and the **RemoteSigned** or **AllSigned** **[execution policy](http://technet.microsoft.com/en-us/library/hh847748)**).
8. **[Don't use aliases in scripts](http://blogs.technet.com/b/pstips/archive/2015/02/04/don-t-use-aliases-in-your-scripts.aspx)**. Use the full cmdlet name with its named **[parameters](http://technet.microsoft.com/en-us/library/hh847824)**.
9. Avoid using backticks, they are easy to miss since they might look like dirt on the screen. Instead, use the pipeline (|) character where appropriate, or even **[splatting](http://technet.microsoft.com/en-us/library/jj672955)** the parameters to the cmdlet.
10. **["Filter left, format right"](http://technet.microsoft.com/en-us/magazine/2009.09.windowspowershell.aspx)**.
11. Add the .exe extension to external commands and applications (e.g. there is a big difference between **sc** and **sc.exe**).
12. Don’t turn off pipeline errors ($ErrorActionPreference = "SilentlyContinue"). Implement structured error handling by using **[Try+Catch+Finally](http://technet.microsoft.com/en-us/library/hh847793)** (or **[Trap](http://technet.microsoft.com/en-us/library/hh847742)**) to handle errors.
13. Do not "pollute" the Windows PowerShell environment by changing **[preference variables](http://technet.microsoft.com/en-us/library/hh847796)** **[globally](http://technet.microsoft.com/en-us/library/hh847849)** (e.g. $ConfirmPreference, $WhatIfPreference, etc.).
14. Use **[cmdletBinding](http://technet.microsoft.com/en-us/library/hh847872)** and add support for the **-WhatIf**, **-Verbose** and **-Debug** parameters.
15. Use **[Advanced Functions](http://technet.microsoft.com/en-us/library/hh847806)**.
16. Use the **Verb-Noun** naming convention for your functions and filters. When picking out verbs, always use **[standard verbs}(http://msdn.microsoft.com/en-us/library/ms714428)**. Use **[Get-Verb](http://technet.microsoft.com/en-us/library/hh852690)** to see what verbs are available.
17. Use standard parameter naming (e.g. **ComputerName** and not **Machine** or **Server**), and set them a default value if relevant (e.g. **$ComputerName = $ENV:ComputerName**).
18. A function should do one thing, and do it well.
19. A function should always return an object or array of objects, not formatted text.
20. **[Avoid using the Return keyword](http://mikefrobbins.com/2015/07/23/the-powershell-return-keyword/)**. Functions automatically return output to the calling process through the pipeline.
21. ~~Avoid using Write-Host. It writes to the host, not the pipeline.~~ Prefer using **[Write-Output](https://technet.microsoft.com/en-us/library/hh849921.aspx)** over using **[Write-Host](http://technet.microsoft.com/en-us/library/hh849877)**. Write-Host writes to the host, not the pipeline.
22. Use **[comment-based help](http://technet.microsoft.com/en-us/library/hh847834)**. The minimum items to add are the Synopsis, Description, and Example nodes.
23. Use **[Test-Connection](http://technet.microsoft.com/en-us/library/hh849808)** (with the **-Quiet** switch) to ensure a computer is online prior to connecting to it.
24. Make sure your script is lined up, indented properly, and easy to read. If you can read and understand your script, you will simplify your debugging process.
25. Keep your script independent from the place you run it (Use **$myInvocation.MyCommand.Path** or **$PSScriptRoot** for PowerShell 3.0 and above).
26. Make sure you test your functions and scripts in a clean environment with no dependencies on profiles, admin rights, and versions to ensure compatibility.
27. Test scripts in test environment before they are released to production.
28. Re-use scripts (Package **[modules](https://msdn.microsoft.com/en-us/library/dd878340)**, create a script **[repository](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/)**).
29. Implement some processes around script lifecycle (change process)
    * Who can request the creation of scripts?
    * Who is responsible for writing the scripts?
    * Who is responsible for maintaining the scripts?
    * Who is responsible for reviewing (quality control) the scripts?
30. Follow a simple but organized script flow:
    * #Requires comments
    * Define your params
    * Create your functions
    * Setup any variables
    * Run your code
    * Comment based help
 
If you have any other best practice you’d like to share, use the comments box below. I’ll add it to the list and mention your name too (if you want).

\Martin.