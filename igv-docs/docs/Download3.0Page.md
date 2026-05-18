<!---
The page title should not go in the menu
-->
<script src="../js/ua-parser.min.js"></script>
<script>
document.addEventListener("DOMContentLoaded", function os() {
    const parser = new UAParser()
    const osName = parser.getOS().name
    const cpu = parser.getCPU()

    let href = null
    let imgAlt = null
    let imgSrc = null

    if (osName.indexOf('Mac OS') !== -1) {
        // This is mac.
        // Note the following values did NOT identify M1 macs:
        //  * parser.getResult().cpu.architecture
        //  * window.navigator.platform
        //  * window.navigator.userAgent
        // Thus, the ugliness that follows:
        const w = document.createElement("canvas").getContext("webgl")
        const d = w.getExtension('WEBGL_debug_renderer_info')
        const g = d && w.getParameter(d.UNMASKED_RENDERER_WEBGL) || ""
        if (g.match(/Apple/)) {
            console.log("Apple Silicon")
            href = 'https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_MacApp_3.0_WithJava.zip'
            imgAlt = 'MacApp Apple with java'
            imgSrc = '../img/DownloadYMacWithJavaApple.png'
        } else {
            console.log("Apple Intel")
            href = "https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_MacAppIntel_3.0_WithJava.zip"
            imgAlt = "MacApp Intel with java"
            imgSrc = "../img/DownloadYMacWithJavaIntel.png"
        }
    } else if (osName.indexOf('Windows') !== -1 || cpu === 'amd64') {
        console.log("Windows")
        href = "https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_Win_3.0-WithJava-installer.exe"
        imgAlt = "Windows snapshot with java"
        imgSrc = "../img/DownloadYWindowsWithJava.png"
    } else if (osName.indexOf('Linux') !== -1 || osName.indexOf('Ubuntu') !== -1) {
        console.log("Linux")
        href = "https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_Linux_3.0_WithJava.zip"
        imgAlt = "Linux with Java"
        imgSrc = "../img/DownloadYLinuxWithJava.png"
    }

    if(href) {
        const cell = document.getElementById('download_container')
        const anchor = document.createElement("a")
        anchor.href = href
        const element = document.createElement("img")
        element.setAttribute("height", "80")
        element.setAttribute("alt", imgAlt)
        element.setAttribute("src", imgSrc)
        anchor.appendChild(element)
        cell.appendChild(anchor)
    }
    else {
        console.log("Platform not detected")
    }

})
</script>


<p class="page-title" style="color: DarkRed;"> IGV 3.0 Beta </p>

<div id="download_container"></div>

**What's New:** See the [Release Notes](ReleaseNotes/3.0.x.md) for what's new in IGV 3.0.


# All platforms

**IGV 3.0 requires Java 21 or greater**. If you download one of the IGV versions that does not include Java, make sure you have Java 21 installed and in your path.

**Mac users:** The IGV 3.0 Mac apps require **MacOS 11 (Big Sur)** or greater.

**Linux users:** The *IGV for Linux* download includes AdoptOpenJDK (now Eclipse Temurin) version 21 for x64 Linux. See their list of supported platforms [here](https://adoptium.net/supported-platforms/). If your platform is not on the "x64 Linux" list, or the packaged Java does not work on your version of Linux, download the *"Command line IGV for all platforms"* and use it with your own Java installation.
<br> 

[![MacApp Apple with java](img/DownloadYMacWithJavaApple.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_MacApp_3.0_WithJava.zip)
[![MacApp Intel with java](img/DownloadYMacWithJavaIntel.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_MacAppIntel_3.0_WithJava.zip)
[![MacApp no java](img/DownloadYMacNeedsJava21.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_MacApp_3.0.zip)
<br>
[![Windows snapshot with java](img/DownloadYWindowsWithJava.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_Win_3.0-WithJava-installer.exe)
[![Windows no java](img/DownloadYWindowsNoJava21.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_Win_3.0-installer.exe)
<br>
[![Linux with Java](img/DownloadYLinuxWithJava.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_Linux_3.0_WithJava.zip)
<br>
[![Command line no java](img/DownloadYCommandLineNoJava21.png){height=80}](https://data.broadinstitute.org/igv/projects/downloads/3.0/IGV_3.0.zip)



