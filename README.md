[![Build Status](https://dev.azure.com/AvaloniaUI/avaloniaui.net/_apis/build/status/avaloniaui.net)](https://dev.azure.com/AvaloniaUI/avaloniaui.net/_build/latest?definitionId=1)

# Manual Build Instructions

1. Make sure you have [latest .NET Core SDK](https://dotnet.microsoft.com/) installed on your PC
2. Install the `Wyam.Tool` .NET Core Global Tool via `dotnet tool install -g Wyam.Tool`
3. Clone the repository and descend into repository root folder.
4. Use the command `wyam -i wwwroot` to build the website.

Alternatively, use `build.cmd` on Windows or `build.sh` on MacOS/Linux for a **regular build**. Or use `fast-build-without-api.cmd` on Windows or `fast-build-without-api.sh` on MacOS/Linux for a **faster build** that does not generate the API contents.

# View Build Artifacts

Use `wyam preview` to view what's built, or double-click `serve.cmd` on Windows or run `serve.sh` on MacOS/Linux.

Open `http://localhost:5080` in your browser!

