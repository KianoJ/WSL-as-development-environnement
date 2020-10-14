# Install .NET Core

```bash
# Add Microsoft package
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update

# Install the SDK
sudo apt-get install -y dotnet-sdk-3.1
```

How to use it : https://code.visualstudio.com/docs/languages/dotnet

## Tools

NuGet Gallery in VSCode : https://marketplace.visualstudio.com/items?itemName=patcx.vscode-nuget-gallery

---

Source : 

Install .Net Core for Ubuntu : https://docs.microsoft.com/en-gb/dotnet/core/install/linux-ubuntu
