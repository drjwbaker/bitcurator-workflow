# Processing Workflow for Digital Media

## James Baker

### v0.2a (13 June 2016)

______
## Scope

University of Sussex Special Collections holds a small collection of digital media / data storage devices that contain both born digital objects and digital objects migrated to those data storage devices. This activity seeks to develop a workflow for making forensic captures of these media with a view to:

- a) Creating evidence around processes and outputs that can feed into future data management plans
- b) Preserving and stabilising these materials in line with best practice
- c) Establishing a set of shared principles in anticipation of future born digital deposits

This document captures our work in a reworked form appropriate for general use.

______
## Preparatory work

- Setup BitCurator OS (either as a Virtual Machine or native install; this process assumes the latter using BitCurator v1.6.12; process differs slightly if the former).
- Source appropriate hardware write-blockers (eg Wiebetech ComboDock)
- Source drives to read media (floppy, CD, DVD).
- Source flash drive as temporary storage.
- Adjust power save settings on PC/laptop to ensure that machine does not switch off or hibernate during processing (note: this can kill the process and waste lots of time!)

______
## Actions

- Investigate private shared network for deposit of outputs.
- Investigate acquisition of further forensic hardware and software tools: 
	- For source media processing: AccessData FTK Imager; KryoFlux.
	- For curatorial arrangement and description: Quick View Plus.
- Repeat process for complex source media (including Mac and legacy Linux OS filesystems).
- Integrate virus and malware check steps.
- Agree method/location for capturing processing work/decisions.

______
## Forensic Capture

- Undertake logical sort of all source media. Depending on collection, this might include:
	- Sort source media by container type.
	- Sort source media by file system. For disks, this might include an attempt to read write-protected source media on a Windows or Mac OS machine.
	- Set aside for storage (but not capture) installer/software disks.
	- Any difficult or unusual media set to one side for bespoke processing after business as usual.
	- Capture these decisions.
- Start BitCurator (see latest at [http://wiki.bitcurator.net/downloads/](http://wiki.bitcurator.net/downloads/) and if virtual machine use [VirtualBox default settings](http://wiki.bitcurator.net/index.php?title=BitCurator_Virtual_Machine_Install)).
- Connect external flash drive as writeable temporary storage for forensic captures. Either: A) First mount ‘read-only’ using `Forensic Tools / BitCurator Mounter`. Note the path for this disk in the ‘raw device’ column. Then in Terminal do `sudo mount –w /dev/xxxx /media/xxxx` where ‘xxxx’ is the value after / in the previous ‘raw device column’ (eg `sdb1`); or B) Click on the disk icon on the top bar and select 'Set mount policy WRITEABLE'. Click ok and connect external flash drive. Open `Forensic Tools / BitCurator Mounter` and mount drive (the device path will start `/dev/sdb..`. Click on the disk icon on the top bar and select 'Set mount policy READ-ONLY'. It is now safe to connect your source media.
- Connect source media. Ensure media to be processed is write-protected when connecting media to workstation. BitCurator sets mount policy to ‘read-only’ by default. For different drive types following connection is advised:
	- Hard drive: use hardware write blocker. For bare drives, also ensure that drive is placed on a surface on which it will not overheat (for example a metal sheet).
	- Floppy drive: use on-disk write blocker tag.
	- USB stick: no hardware write blocker required (see Kessler & Carlton, [2014](http://ojs.jdfsl.org/index.php/jdfsl/article/view/249)).
	- Other media: case-by-case basis.
- Open `Forensics Tools / BitCurator Mounter` to ensure media is mounted correctly.
- Create forensic disk image in E01 format using Guymager and store in appropriate folder in file system:
	- Open `Imaging Tools / Guymager`.
	- Select media, right-click, select ‘Acquire Image’.
	- In ‘Acquire Image Screen’, enter as follows then hit Start:
		- File Format: Expert Witness Format.
		- Split size: 2047 MiB.
		- Case Number: TBC
		- Evidence Number: TBC
		- Examiner: Sussex ITS username.
		- Description: [case number]-[evidence number]-[examiner].
		- Notes: media type (e.g. cdd, fdd, hdd).
		- Image directory: select location on external flash drive (in the /media folder)
		- Image filename: [case number][evidence number].
	- Hash calculation / verification:
		- Calculate MD5: yes.
		- Calculate SHA-1: yes.
		- Calculate SHA-256: yes.
		- Re-read source after acquisition: no.
		- Verify image after acquisition: yes.
- When process is complete (Guymager should report ‘Finished – Verified & Ok’ in the ‘State’ column), make a copy of capture and metadata in a backup folder.

______
## Reporting

- To create a directory and file listing for your disk image, open `Forensic Tools / BitCurator Reporting Tool`
- Select Fiwalk XML tab and enter:
	- Image File: location of captured image (‘filename [case number][evidence number].E01’) on external drive
	- Output XML File: location of captured image on external drive with filename ‘[case number][evidence number].xml’
- Hit Run. When output reads ‘Success!!!’ check .xml output

______
## Image Access

- To access files on your disk image, open `Forensic Tools / BitCurator Disk Image Access`
	- Select ‘Open disk image’
	- Navigate to forensic capture (the .E01 file) and choose open
	- Browse the disk image and check the box for files you want to export from the image.  When you are done, hit ‘Export selection’ and choose a location to export the files to (such as ‘/media/XXXX/’)
	- Open files in your normal PC environment for curation and description. Note that specialist software may be required for legacy file formats.

______
## Post-processing

- Original digital media stored or decommissioned as appropriate. 
- Optional: Photography of digital media and hardware undertaken if deemed appropriate and stored in appropriate folder alongside forensic capture and metadata (this is useful when the media contains handwritten notes, for example)

____
### Some admin...

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

***Exceptions: embeds to and from external sources, and direct quotations from speakers***
