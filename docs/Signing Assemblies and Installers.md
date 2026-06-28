---
title: Signing Assemblies and Installers
tags:
- Development
- Support
- Signing
description: Signing acts as a reassurance that executable programs (and their installers
  and components) come from a legitimate source. Windows platforms and…
created: '2020-09-08'
modified: '2026-03-09'
original_url: https://codislimited.sharepoint.com/sites/Wiki/Pages/Signing%20Assemblies%20and%20Installers.aspx
---

Signing acts as a reassurance that executable programs (and their installers and components) come from a legitimate source.   Windows platforms and Excel can have restrictions that inhibit or prevent the installation or loading of programs that aren't signed.  

Codis installers (exes and msis) and the assemblies they install should all be signed.  


Excel can be configured to disallow unsigned assemblies to load as Add\-ins.   Note: Excel will not be concerned about the installers, rather the assemblies loaded adxloader.dll (and possibly others).  
  
**Developers's Notes below are all out\-of\-date.** Assemblies are now signed using this process: [How to sign files with Azure Sign Tool \- Trustzone](https://trustzone.com/knowledge-base/how-to-sign-files-with-azure-sign-tool/).  


If you've found these page because DevOps signing steps are failing with a message like:  
"Failed to retrieve certificate Code\-Signing\-2025 from Azure Key Vault. Please verify the name of the certificate and the permissions to the certificate. Error message: ClientSecretCredential.."   
  
And below that:  
  
"ResponseBody: \{"error":"invalid\_client","error\_description":"AADSTS7000222: The provided client secret keys for app '\*\*\*' are expired."  


then the application registration "DevOpsCodeSigning" needs to have its client secret ID updating.    You can create a new secret.  You then replace the SigningClientSecret in the Code Signing library in devops with the secret **value**.

  


  


  


  


NOTES below are all out\-of\-date  


  


# Developers' Notes

## Signing Assemblies

  


Signing of assemblies is best achieved from the Addin project.  Signing is supported using the Codis.Certificates package.  As well as including the certificate, it adds a targets that will run the signing, but it needs a couple of changes to activate this.

The Codis package Codis.Certificates v. 1\.3\.0 has to be referenced.  

The nuget.org package signtool has to be added.  Note the GeneratePathProperty.  This is used by the Codis.Certificates targets code.

  \<ItemGroup\>    \<PackageReference Include\="signtool" GeneratePathProperty\="true" \>      \<Version\>10\.0\.17763\.132\</Version\>    \</PackageReference\>  \</ItemGroup\>  


Add the line:

\<SignOutput\>true\</SignOutput\>  


to your project.  Possibly just for the release configuration.  


## Signing MSIs and Installation EXEs

WIX can be configured to sign MSIs and Installation EXEs.  WIX only supports early msbuild tools \- package references are not supported.  Also, WIX does not seem to recognise properties and targets set in the build part of the Codis.Certificate 1\.3\.0 package.   Paths to the signtools have to be explicit but as PackageReferences are not supported, packages are installed in the path pointed to be the "repositoryPath" setting in the nuget.config file it should be possible to specify a relative path.  


The package reference has to be set in the package.config file.  


In order to sign the output of WIX MSI or bootstrapper projects, the wixproj file has to have an import of Codis.Certificates.props at the beginning and an import of Codis.Certificates.targets at the end of the project:  


 \<Import Project\="..\\..\\packages\\Codis.Certificates.1\.3\.0\\build\\Codis.Certificates.props" Condition\="Exists('..\\..\\packages\\Codis.Certificates.1\.3\.0\\build\\Codis.Certificates.props')" /\>   
and  


\<Import Project\="..\\..\\packages\\Codis.Certificates.1\.3\.0\\build\\Codis.Certificates.targets" Condition\="Exists('..\\..\\packages\\Codis.Certificates.1\.3\.0\\build\\Codis.Certificates.targets')" /\>and it needs to set the property 

\<SignOutput\>true\</SignOutput\>  


The targets in the Codis.Certificates targets depend on the property Pkgsigntool to point to the folder where the signtool package is.  


In CodisDevelopment, the Directory.Build.props are used in the WIXInstallers folder.  The Directory.Build.prop in the folder also loads the one in the folder above, which specifies a $(RepoRootDir) property which can be used as a base to source packages.  The Directory.Build.props in the WIXInstaller folder uses this:  
  


\<Import Project\="$(\[MSBuild]::GetPathOfFileAbove('Directory.Build.props', '$(MSBuildThisFileDirectory)../'))" /\>    \<PropertyGroup\>      \<Pkgsigntool\>$(RepoRootDir)\\packages\\signtool.10\.0\.17763\.132\</Pkgsigntool\>    \</PropertyGroup\>  


These can then be used in the wix setup and bootstrapper projects:  
  


 \<Exec Command\="\&quot;$(SignToolPath)\&quot; sign /d \&quot;App Setup\&quot; /f \&quot;$(CertificatePath)\&quot; /p Alph@C0di$ /t http://timestamp.digicert.com /a \&quot;$(TargetPath)\&quot;" /\>
