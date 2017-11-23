# Processing Workflow for Digital Media

## James Baker

______
## Scope

This workflow is an adaptation of [a workflow developed in 2016](https://github.com/drjwbaker/bitcurator-workflow/blob/master/documents/2016-06-13_digitalmedia-processingworkflow-v02a.md) in collaboration with University of Sussex Special Collections.

It is intended for use during the 'Forensic Recovery from Data Storage' workshop run 13 December 2017 as part of the [Sussex Humanities Lab](http://www.sussex.ac.uk/shl/) [Digital Methods Open Workshop Series](http://www.sussex.ac.uk/shl/events/open_workshop_series).

______
## Preparatory work

- Setup [BitCurator](https://wiki.bitcurator.net/index.php?title=Main_Page) (either as a Virtual Machine or native install). This process assumes the former using BitCurator v1.8.12.

______
## Forensic Capture

- Open Virtual Box. Go to 'Machine' then 'Add'. Navigate to 'BitCurator-1.8.12.vbox' and select it.
- Once selected, right click on the machine, choose 'Settings', 'Shared Folders', then the add icon on the right. Choose a folder path, select 'auto-mount', and click ok, ok, then power up the machine (with the 'Start' button)
- Once BitCurator boots, you are effectively in a adapted Ubuntu/Linux environment. On the adaptations, note for example you have lots of folders in place with software in, and - the far left icon of the top bar - that right policy is set to read-only.
- Connect source media. Ensure media to be processed is write-protected when connecting media to workstation. BitCurator sets mount policy to ‘read-only’ by default. For different drive types following connection is advised:
	- Hard drive: use hardware write blocker. For bare drives, also ensure that drive is placed on a surface on which it will not overheat (for example a metal sheet).
	- Floppy drive: use on-disk write blocker tag (down is not-writable)
	- USB stick: no hardware write blocker required for pre-2016 flash drives (see Kessler & Carlton, [2014](http://ojs.jdfsl.org/index.php/jdfsl/article/view/249)).
- In the event that 'BitCurator Mounter' does not open, try mounting the source media by clicking on it in a finder window.
- If you can't find it here, use the 'Devices' and 'USB menu in VirtualBox to connect the device to BitCurator, then repeat the finder window step.
- Create forensic disk image in E01 format using Guymager and store in appropriate folder in file system:
	- Open `Imaging and Recovery` then `Guymager`.
	- Select media, right-click, select ‘Acquire Image’.
	- In ‘Acquire Image Screen’, enter as follows then hit Start:
		- File Format: Expert Witness Format.
		- Split size: 2047 MiB.
		- Case Number: TBC
		- Evidence Number: TBC
		- Examiner: Sussex ITS username.
		- Description: [case number]-[evidence number]-[examiner].
		- Notes: media type (e.g. cdd, fdd, hdd).
		- Image directory: select location of the local share (in the /media folder)
		- Image filename: [case number][evidence number].
	- Hash calculation / verification:
		- Calculate MD5: yes.
		- Calculate SHA-1: yes.
		- Calculate SHA-256: yes.
		- Re-read source after acquisition: no.
		- Verify image after acquisition: yes. (NB: if you find the 'Time Remaining Field' growing exponentially during capture, try aborting and re-running with this option deselected)
- When process is complete (Guymager should report ‘Finished – Verified & Ok’ in the ‘State’ column). Eject the source media. Now go look at what you've made!

______
## Reporting

### Simple

- To create a directory and file listing for your disk image, open `Forensic Tools / BitCurator Reporting Tool`
- Select Fiwalk XML tab and enter:
	- Image File: location of captured image (‘filename [case number][evidence number].E01’) on external drive
	- Output XML File: location of captured image on external drive with filename ‘[case number][evidence number].xml’
- Hit Run. When output reads ‘Success!!!’ check .xml output

### Detailed

- To create a series of reports on your disk image (deleted files, counts of file types, semantic features, et cetera), open `Forensic Tools / BitCurator Reporting Tool`
- Select 'Launch BEViewer'.
- In the 'Bulk Extractor Viewer', select the 'Tools' tab and the 'Run bulk extractor' option.
	- Image file: location of captured image (‘filename [case number][evidence number].E01’) on external drive
	- Output Feature Directory: recommend a new folder within the location of captured image on external drive named after the captured image
	- Select the 'Scanners' you want to use on the right-hand side (for more info in Scanners see the [BitCurator Wiki](http://wiki.bitcurator.net/index.php?title=Bulk_Extractor_Scanners))
	- When you are ready, click 'Submit Run'
- When this is complete, return to the 'BitCurator Reporting Tool' and enter:
	- Image File: location of captured image (‘filename [case number][evidence number].E01’) on external drive
	- Bulk Extractor Feature Directory: the new folder within the location of captured image on external drive where you saved the Bulk Extractor Features
	- Output Directory: recommend the same folder as the Bulk Extractor Features.
	- When you are ready, click 'Run'

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
