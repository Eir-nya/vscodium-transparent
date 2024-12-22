# vscodium-transparent
Allows VSCodium transparency.

## ORIGINAL TRANSPARENCY PATCHES BY Kyle Smith

From [Reddit](https://www.reddit.com/r/unixporn/comments/wlowdu/oc_transparency_patches_for_vscodium/) and [GitHub](https://github.com/EggAllocationService/vscodium-transparency)

## Guide

1. Clone vscodium to your desktop: `git clone https://github.com/VSCodium/vscodium`
2. Drop these three files (`transparency.patch`, `transparent-titlebar.patch`, `transparent-workbench.patch`) inside the `patches` folder
3. Open a terminal in the vscodium directory
4. Follow [VSCodium's build instructions](https://github.com/VSCodium/vscodium/blob/master/docs/howto-build.md) to build. On Linux, I had to run `./build/build.sh -l`. My output appeared in a new folder `VSCodium-Linux-x64`in the project root.
5. Open compiled VSCodium - enter folder and open `codium`
6. Open command palette and enter "Open User Settings (JSON)"
7. Add some customizations that change window transparency. For instance:

```
"workbench.colorCustomizations": {
    "editor.background": "#00000000",
    "titleBar.inactiveBackground": "#00000000",
    "titleBar.activeBackground": "#00000000",
    "editorGroupHeader.tabsBackground": "#00000000",
    "tab.inactiveBackground": "#00000000",
    "activityBar.background": "#00000000",
    "statusBar.background": "#00000000",
    "sideBar.background": "#00000000",
    "sideBarSectionHeader.background": "#00000000",
    "editorPane.background": "#00000000",
},
```
The above makes the window background completely transparent. Great for testing if the patches have worked, but don't keep it forever.

8. (KDE Plasma) add a Window Rule matching windows with name `codium`. Set "active opacity" to 99%. This will fix the background image "freezing" because the compositor still believes it's an opaque window.

## If build says patches failed/corrupt patch files

1. Clone vscode to your desktop: `git clone https://github.com/microsoft/vscode`
2. Open each patch in an editor of choice
3. For each file modified by the patch (on lines that start with `diff --git a/...`), open the respective file in the `vscode` repository
4. Find the relevant area modified by the patch. Since the patch failed it's likely code was moved around a bit in an update to vscode.
5. Apply the same changes from the patch file. Removed lines start with `-`, added lines start with `+`.
6. Open a terminal in the vscode directory
7. Run `git diff > ../transparency.path`, rename if needed
8. Replace matching downloaded file in `vscodium/patches` with this new one
9. Don't forget to run `git restore *` in vscode directory between each operation if you need to update multiple patches!
