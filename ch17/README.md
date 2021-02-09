# Chapter 17: Printing
- CUPS is the underlying software almost all Linux systems use to print from applications like a web browser or LibreOffice
- The print scheduler reads server settings from several configuration files, the two most important of which are cupsd.conf and printers.conf. These and all other CUPS related configuration files are stored under the /etc/cups/ directory.
- CUPS stores print requests as files under the /var/spool/cups directory (these can actually be accessed before a document is sent to a printer).
- Log files are placed in /var/log/cups and are used by the scheduler to record activities that have taken place. These files include access, error, and page records.
