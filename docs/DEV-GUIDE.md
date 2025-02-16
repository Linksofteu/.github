# Development guide
This document will guide you through the process of creation and development of new modules for the LinkSoft public repositories.

> ℹ️ **Note**  
> You can also use Visual Studio Package Manager to manage your local NuGet packages and sources.

## 1) Creating local nuget repository
1) Start with creating a local folder which will act as a local nuget repository. Let's call it ~/Packages.
2) Open terminal of your choice and run the following command:
```bash
dotnet nuget add source ~/Packages
```

## 2) Developing a nuget package
1) Create a project according to the repository documentation.
2) You can then directly reference the project outside of a folder structure for the solution that you're testing the nuget package in. You can do this by running the following command:
```bash
dotnet sln add <path-to-project>
```
3) You can then reference the project from individual project files in the solution.

The project that is outside the solution's folder structure will be added to the root of the solution. You can remove it once you're done developing the nuget package.

## 3) Creating a local nuget package
1) Navigate to the folder with the nuget package and run the following command:
```bash
dotnet build --configuration Release
dotnet pack --configuration Release --output ./packages
```
2) This will create a nuget package in the target folder. Copy contents of the target folder to the local nuget repository that you created earlier.
> ⚠️ **Warning**  
> If you are referencing another package from the built package, even as a project reference, you need to build it and copy it to the local nuget repository as well.
3) Delete all the project references we have created in step 2.
4) Add package reference to the .csproj file you need to reference the nuget package in. It should look like this:
```xml
<PackageReference Include="<package-name>" Version="<version>" />
```
You can usually find the version number in the common/common.props file in the root of the target repository.

> 💡 **Tip**  
> You can also use the command:
> ```bash
> dotnet add package <package-name> --version <version>
> ```
> to add a package reference to the .csproj file from the local repository, but this approach may lead to issues with repository certificate.