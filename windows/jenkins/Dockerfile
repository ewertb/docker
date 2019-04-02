FROM microsoft/dotnet-framework:4.7.2-sdk-20190212-windowsservercore-ltsc2016

ADD ./git.inf C:/git/git.inf
ADD https://github.com/git-for-windows/git/releases/download/v2.21.0.windows.1/Git-2.21.0-64-bit.exe C:/git/Git-2.21.0-64-bit.exe
RUN ["C:\\git\\Git-2.21.0-64-bit.exe", "/SP-", "/SILENT", "/SUPPRESSMSGBOXES", "/FORCECLOSEAPPLICATIONS", "/LOADINF=C:/git/git.inf"]
RUN Powershell.exe -Command Remove-Item C:/git –Recurse

ADD https://download.microsoft.com/download/E/E/D/EEDF18A8-4AED-4CE0-BEBE-70A83094FC5A/BuildTools_Full.exe C:/msbuild/BuildTools_Full.exe
RUN ["C:\\msbuild\\BuildTools_Full.exe", "/SILENT"]
RUN Powershell.exe -Command Remove-Item C:/msbuild –Recurse

ADD https://dist.nuget.org/win-x86-commandline/latest/nuget.exe C:/nuget.exe

RUN Powershell.exe -Command Add-WindowsFeature Web-Server
ADD https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.6/ServiceMonitor.exe C:/ServiceMonitor.exe

ADD http://mirrors.jenkins-ci.org/windows-stable/jenkins-2.150.3.zip C:/jenkins/jenkins-2.150.3.zip
RUN Powershell.exe -Command Expand-Archive "C:/jenkins/jenkins-2.150.3.zip" -DestinationPath "C:/jenkins/"
RUN ["msiexec.exe", "/i", "C:\\jenkins\\jenkins.msi", "/qn"]
RUN Powershell.exe -Command Remove-Item C:/jenkins –Recurse

EXPOSE 8080
ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]