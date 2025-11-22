⚠️ Issue: Ubuntu 22.04 LTS Installing Only .NET SDK 6 Instead of SDK 8

While setting up the development environment on Ubuntu 22.04 LTS, an issue occurred where the system only allowed installation of .NET SDK 6, even when attempting to install .NET SDK 8.0.
This happened because older or conflicting .NET packages were already present on the system.

🔧 Solution

The fix was to completely remove all existing .NET installations and then reinstall the correct SDK.

🛠️ Commands Used

# Remove all existing dotnet packages
sudo apt-get remove --purge 'dotnet-*'

# Remove any remaining dotnet directories
sudo rm -rf /usr/share/dotnet

# Clean unused dependencies
sudo apt-get autoremove

After cleaning:

# Update package lists with forced IPv4 (useful for some network issues)
sudo apt-get update -o Acquire::ForceIPv4=true

# Install the correct .NET 8 SDK
sudo apt-get install -y -o Acquire::ForceIPv4=true dotnet-sdk-8.0

✅ Verification

dotnet --list-sdks
dotnet --version

