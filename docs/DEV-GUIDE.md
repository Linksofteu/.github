# Development guide
This document will guide you through the process of creation and development of new modules for the LinkSoft public repositories.

## Creating local nuget repository
1) Start with creating a local folder which will act as a local nuget repository. Let's call it ~/Packages.
2) Open terminal of your choice and run the following command:
```bash
dotnet nuget add source ~/Packages
```