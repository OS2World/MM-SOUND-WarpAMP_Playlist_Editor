This is the readme file for the WarpAMP Playlist Editor.

This program was written to facilitate the editing and creation of playlist
files for the WarpAMP MPEG audio player program, which only uses the
standard file dialog for adding files.

It's not particularly fancy, but it should be easier to use than what
WarpAMP itself provides.

This program is provided free of charge, with no guarantees as to its
utility and safety.  I am not responsible for any damage it may cause.
You know the drill.

The program was written in C++ with IBM's VisualAge C++ 3.0 for OS/2, using
the OpenClass library.

It is a learning experience for me, and I'll probably be fixing things and
adding things until I get bored with it.

=============================================================================

Basic Operation:

Virtually every control has a mnemonic, which means you can press 
Alt+[letter] or Ctrl+[letter] to select them.  In the case of the text 
labels, you jump to the following listbox.  

In addition, there are five hotkeys not visible in any way:
            
F5        - refresh the drive, directory, and file lists
F6        - select all items in the file listbox
F7        - deselect all items in the file listbox
F8        - select all items in the chosen listbox
F9        - deselect all items in the chosen listbox

The drivelist can be dropped down by clicking on the entry field as well as 
the button, which is a departure from standard behavior, but one I think 
good.

In addition to pressing F5, you can refresh the drive listbox by 
double-clicking in the entry field with mouse button number 2 or 3 (if 
there is one).

To select a directory, either double-click on it, or hit enter or space 
while it's hilited.

In addition to hitting the Add button, you can add files to the chosen list 
by double clicking (one at a time), or hitting enter while the file listbox 
has focus (all selected files added).  The same behavior is true of the 
chosen listbox as well, though the corresponding result is files removed.

The program remembers the last directory you added files to the chosen list 
from, and will open that directory on startup.  It also remembers the last 
directory you opened a file from, and the last one you saved a file to, 
independently.  These will be the default directories for the open and 
save dialogs.

You can drag and drop fonts to anything on the window that has text, and 
those fonts will be remembered. 

Also remembered is the position of the window on the desktop.  You can 
disable this last behavior, and save the position only when pressing the 
button on the settings dialog.

=============================================================================

Frequently and Unfrequently Asked Questions:

Q:  Who wrote it?
A:  Me, of course.  Mike Ruskai, reachable at thanny@home.com.

Q:  Why did you write it?
A:  Because it's somewhat useful, and it's also a good way to learn C++ and
    the OpenClass libraries.

Q:  Why is the executable so big?
A:  OpenClass and C++, I gather.  It'd be smaller if I did it in C, but
    would require more work on my part.

Q:  Can I have the source?
A:  Won't be any use to you unless you have VisualAge C++ 3.0 for OS/2 or 
    later.  If you're a developer and want a peek, then just ask.  But be
    gentle in any criticisms of my code :)

Q:  Why is your About window so lame?
A:  Because I'm new to C++ and OpenClass.  It was hard to get that much.

Q:  Why is the Help button disabled?
A:  Because I haven't put together a help file yet.

Q:  Why won't it run under OS/2 2.1x?
A:  Because the executable has both code and data compressed, which OS/2
    2.1x doesn't support.  The resources are also compressed in a non-2.x
    compatible way.  This was done because WarpAMP doesn't run on sub-Warp 3
    installations.  It'd be a simple matter to link together a 2.x compatible
    executable, of anyone really wants it.  It'd also be a simple matter
    for anyone to use LxLite to recompress the executable to function under
    OS/2 2.x, since there are no Warp-specific functions used in the 
    program. 

Q:  Can I create my own interface for the program?
A:  Yes, in a manner of speaking.  Included in the archive is another 
    archive with the resource files necessary to modify the existing 
    interfaces, or create an entirely new one.  You can't, however, add
    any new controls, or remove any.  The result of that would be a program
    that crashes.  You must also use the same integer values for controls, 
    as defined in the included .h file.  While it's possible to edit the
    dialogs with just a text editor, you'll want a dialog editor of some 
    sort.  Most OS/2 compiler packages have one, and they may be available
    elsewhere as well.  You will also need a resource compiler (rc.exe), 
    which is also possibly available apart from compiler packages.  I don't
    recommend you fool around with this unless you know what you're doing.

=============================================================================

History:

09-10-98  -  Initial beta release.

---

Fixed:  Had the DosError() API call pointed out to me, so no SYS0039's when
        constructing the drive list.  Left them enabled when selecting a
        drive.

Added:  Double-clicking with mouse button 2 or 3 in the entry field of the
        drive list will repopulate it, and in the process refresh the
        directory and file lists.  It will remain on the current drive and
        in the current directory.

Changed:  Just about everything is done in a separate thread now, including
          all calls to DosSetDefaultDisk.  The app will hang until the API
          returns, but keep answering messages so you can go about your
          business while you wait.

Fixed:  Directory list will no longer act on a double click that doesn't hit
        any directory names.

09-13-98  -  0.99.1 Beta release

---

Fixed:  There was a bug that would cause the app to silently crash if no
        profile existed with a certain directory stored.  Fixed.

Added:  The playlist editor will now keep track of all font changes.

09-13-98  -  0.99.2 Beta release (quick maintenance)

---

Fixed:  App would crash after clicking Open or Save when the stored last
        directory for each is on a drive that's no longer valid.  Now
        checks drive before passing it onto the file dialog.

Fixed:  The file deselect all button would flicker when deselecting all
        items.  Had the select handler ignore selection messages while
        that thread was running.

Fixed:  Neglected to clear out the drive listbox, so each refresh was
        causing it to fill up with duplicate drive letters.

Fixed:  There will be no more SYS0039's at all.  Had to jump through a 
        couple hoops to do it, though, since DosSetDefaultDisk() and
        DosSetCurrentDir() both return NO_ERROR so long as the drive and
        directory (respectively) exists, regardless of whether or not the
        drive is in a ready state.  DosFindFirst/DosFindNext, luckily, 
        return ERROR_NOT_READY, even though they're not documented to do 
        so.  

Added:  Changed the mnemonics of some buttons to allow for more mnemonics
        on the text controls, to select the listboxes with a hotkey.

Changed:  Due to something of a peculiarity with the VisualAge C++ compiler
          when using C++ templates, the executable was larger than it
          should have been.  It's now about half the size, though still
          nice and bulky.

Changed:  Shortened the chosen string, since it was clipping on 640x480
          displays.

09-15-98  - 0.99.3 Beta release (for the SYS0039 final fix)

---

Fixed:  Closed up all remaining holes for SYS0039's to sneak in, though
        they probably never would.

Fixed:  Introduced problem with Move Up and Move Down with last build, when
        trying to utilize a collection class to speed the Add function up.
        Didn't speed things up (slowed them down, due to the extra work), 
        so I took it out.  Forgot to change those two functions back, 
        though, so the results were contrary to intentions.  This has been
        fixed.

Fixed:  For some reason, the drive list wouldn't behave itself and stay
        disabled, so holding the up or down arrows in it would start a 
        new thread for each drive selection, eventually causing a resource
        conflict, which ended with a SYS3175.  Modified the drive thread
        to exit immediately if one was already executing.

Fixed:  The file list was flickering on an add operation, due to the 
        one-by-one deselection of files as they were added.  More an 
        annoyance than a problem, I nevertheless disabled updates while
        an add operation was going on. 

Changed:  Used LxLite 1.21 to cut the executable size down even more, to
          below 400K now, over 80% of which is OpenClass library code 
          (the executable is about 64K linked dynamically).

09-16-98  -  0.99.4 Beta release (maybe I'll stop breaking things to
                                  have more time between releases soon)

---

Fixed:  The IFont::setPointSize() function of the OpenClass library has
        a memory leak.  This caused the loss of some memory on startup that
        needn't have been used up, and a recurring loss of memory each 
        time the About window was displayed.  Worked around by deleting
        and recreating IFont's instead of using that function.

Changed:  Created new interface with wider file listboxes, and added a 
          settings dialog to choose between it and the old format (which
          is still there but widened a bit).  The change takes place upon
          hitting OK on the settings dialog, and unless I've screwed up,
          the current state should be restored when the new dialog opens,
          which is done by essentially restarting the app.

Added:  The aforementioned settings dialog allows you to toggle whether or
        not exits are confirmed when unsaved changes have been made.  It
        also allows you to toggle whether or not the window position is
        automatically saved.  When the latter is disabled, a button is
        enabled to let you save the position at will.

Added:  Added a borderless entry field to display the current directory.  
        It appears to be a static control with black text, but it is in 
        fact an entry field, which will scroll to the right for longer
        pathnames.  You can also select the text in it, but not alter it
        directly.

Added:  The resource files necessary to make modifications to the existing
        dialogs, or create entirely new ones, have been included, in the
        file dialog.zip.  See the readme inside for more information.

09-28-98  -  0.99.5 Beta, though I scrapped it before it was archived...

---

Fixed:  Bug that's been there since I attempted to use a collection view
        listbox, preventing files from being saved properly, and crashing
        the program just for a bonus.

Added:  Put an Include button, to add the contents of a playlist file to 
        the chosen list, rather than replace what's there.

Fixed:  All actions which add to the chosen list first check to see if the
        file in question is already present therein.  If so, it doesn't add
        it.  If all items requested to be added already exist, and nothing
        is in fact added, the program was incorrectly setting the modified
        flag, when no changes have really occurred.  A comparison is done
        between the count before and after in the chosen list.  If the 
        latter isn't greater than the former, nothing has been added, and
        the modified flag isn't set.

Fixed:  The open command wasn't using the settings value of exit 
        confirmation, but only the '/NOCONFIRM' parameter (which is now
        completely ignored).  Fixed.

Fixed:  Original window position would possibly be off the screen for lower
        resolutions.  Set it so that unless otherwise specified (by an INI
        entry or what have you), the bottom left corner will be at 5x5.

09-29-98  -  0.99.6 Beta, which should be bug-free and actually useful...

=============================================================================

Known Issues/Problems:

Problem:  Clicking on drive list entry field doesn't allow one to slide the
mouse cursor down to select a drive before releasing the button.  Working
on a solution to this.

Workaround:  None.  Have to click twice.

Problem:  With certain font sizes, the listboxes will have a region at the
bottom that's updated only in one direction.

Workaround:  None.  This is an OS/2 problem that can't be worked around 
without doing all the drawing of the listbox, something I'm not prepared to 
do right now.
=============================================================================

Contact Information:

I can be reached in many different ways, but I'm only going to list one:

E-mail to thanny@home.com

You should use this to report a problem, make a suggestion, or bombard me 
with comments.

If you're a programmer who knows how to get around any of the problems 
listed above, I'd especially like to hear from you.
