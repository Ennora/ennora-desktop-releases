# Ennora Desktop

Ennora Desktop records a meeting on your computer and lets Ennora write the
notes, the summary and any forms you chose, into your home's Ennora.

## Download

Every version is on the [Releases](../../releases) page. Pick the one for
your region and your computer:

| Your Ennora | Mac (Apple silicon) | Windows (64-bit) |
|---|---|---|
| UK homes (portal.uk.ennora.ai) | `Ennora-UK.dmg` | `Ennora-UK-Setup.exe` |
| US homes (portal.ennora.ai) | `Ennora-US.dmg` | `Ennora-US-Setup.exe` |

Not sure which region you are in? Use the same one as the Ennora web address
you sign in to.

**For your home's IT.** If your home's computers are managed with Intune,
Jamf, Workspace ONE or a similar tool, IT can install Ennora for every
account on a computer instead:

| | Mac (Apple silicon, macOS 14.2 or later) | Windows 10 or 11 (64-bit) |
|---|---|---|
| File | `Ennora-UK.pkg` (`Ennora-US.pkg`) | `Ennora-UK.msi` (`Ennora-US.msi`) |
| Installs into | `/Applications` | `C:\Program Files\Ennora UK` |
| Silent install | Deploy the package with your MDM | `msiexec /i Ennora-UK.msi /qn /norestart` |

Neither copy updates itself: IT deploys each new version, which replaces the
old one in place. Your Ennora contact can send IT the full guide.

## Installing

**Mac.** Open the `.dmg` and drag Ennora into Applications. The first time
you open it, your Mac says it was downloaded from the internet: press
**Open**. Sign in with your Ennora account, and press **Allow** when your
Mac asks about the microphone. Ennora Desktop is signed by Ennora's US
company, Ethero, Inc., and checked by Apple.

**Windows.** Run the `Setup.exe`. Windows may show "Windows protected your
PC": press **More info**, then **Run anyway**. Sign in with your Ennora
account. If Ennora says the microphone is not allowed, follow the steps it
shows, then reopen it.

## Check a download before you install it

Every release has a file called `SHA256SUMS.txt` beside the downloads. It
lists the SHA-256 checksum of each file: a fingerprint that changes if even
one byte of the file is different. If the checksum of the file you
downloaded matches the one in `SHA256SUMS.txt`, you have exactly the file
Ennora published, not a damaged or altered copy.

Download `SHA256SUMS.txt` into the same folder as the file you want to check.

**On a Mac**, in Terminal:

```bash
cd ~/Downloads
shasum -a 256 --check --ignore-missing SHA256SUMS.txt
```

Every file you downloaded should say `OK`. To see one file's checksum on
its own, run `shasum -a 256 Ennora-UK.pkg` and compare it with its line in
`SHA256SUMS.txt`.

**On Windows**, in PowerShell, in the folder with the download:

```powershell
$file = "Ennora-UK.msi"
$expected = ((Get-Content .\SHA256SUMS.txt) -match [regex]::Escape($file)).Split(" ")[0]
(Get-FileHash $file -Algorithm SHA256).Hash -eq $expected
```

It should print `True`. To see the checksum on its own, run
`Get-FileHash .\Ennora-UK.msi -Algorithm SHA256`, or in Command Prompt
`certutil -hashfile Ennora-UK.msi SHA256`, and compare it with the line in
`SHA256SUMS.txt` (capital or small letters do not matter).

**If a checksum does not match, do not install the file.** Download it
again. If it still does not match, write to contact@ennora.ai.

A checksum on this page proves the file matches this page. For a second
check from another place, compare it with the checksum Ennora sends your IT
contact with each version, and check the signature as well:

**Mac signature.** For the package:

```bash
pkgutil --check-signature Ennora-UK.pkg
spctl --assess --type install -vv Ennora-UK.pkg
```

The first should say `signed by a developer certificate issued by Apple for
distribution` and name `Developer ID Installer: Ethero, Inc. (3H588DAJDC)`.
The second should say `accepted` and `source=Notarized Developer ID`. For
the app, once it is in Applications:

```bash
spctl --assess --type execute -vv "/Applications/Ennora UK.app"
```

It should say `accepted` and `source=Notarized Developer ID`.

**Windows signature.** In PowerShell:

```powershell
Get-AuthenticodeSignature .\Ennora-UK.msi
```

The Windows downloads are not signed yet, so today this says `NotSigned`;
rely on the checksum until they are. Once they are signed, it will say
`Valid`, with the publisher Ethero, Inc., Ennora's US company, as on the
Mac.

## Help

Ask your home's Ennora administrator.
