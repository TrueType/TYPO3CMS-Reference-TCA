.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../../Includes.txt
.. include:: Images.txt


.. _columns-group:

TYPE: "group"
^^^^^^^^^^^^^

The group element in TYPO3 makes it possible to create references to
records from multiple tables in the system. This is especially useful
(compared to the "select" type) when records are scattered over the
page tree and requires the Element Browser to be selected. In this
example, Content Element records are attached (taken from the "Insert
records" content element):

|img-35| The "group" element is also the element you can use to bind files to
records in TYPO3. In this case image files:

|img-36| One thing to notice about such a field is that the files that are
referenced actually get moved into an internal file folder for TYPO3!
It does not create references to the files' original positions!


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Key
         Key

   Datatype
         Datatype

   Description
         Description

   Scope
         Scope


.. container:: table-row

   Key
         type

   Datatype
         string

   Description
         *[Must be set to "group"]*

   Scope
         Display / Proc.


.. container:: table-row

   Key
         internal\_type

   Datatype
         string

   Description
         **Required!**

         Configures the internal type of the "group" type of element.

         There are four possible options to choose from:

         - "file" - this will create a field where files can be attached to the
           record

         - "file\_reference" - this will create a field where files can be
           referenced. In contrast to "file", referenced files (usually from
           fileadmin/) will not be copied to the upload folder.  **Warning:** use
           this carefully.  *Your references will be broken if you delete
           referenced files in the filesystem!*

         - “folder” - this will create a field where folders can be attached to
           the record

         - "db" - this will create a field where database records can be attached
           as references.

         The default value is none of them - you must specify one of the values
         correctly!

   Scope
         Display / Proc.


.. container:: table-row

   Key
         allowed

   Datatype
         string

         (list of)

   Description
         **For the "file" internal type (Optional):**

         A lowercase comma list of file extensions that are permitted. E.g.
         'jpg,gif,txt'. Also see 'disallowed'.

         **For the "db" internal type (Required!):**

         A comma list of tables from $TCA.

         For example the value could be "pages,be\_users".

         Value from these tables are always the 'uid' field.

         First table in list is understood as the  *default table* , if a
         table-name is not prepended to the value.

         If the value is '\*' then all tables are allowed (in this case  *you
         should set "prepend\_tname"* so all tables are prepended with their
         table name for sure).

         *Notice* , if the field is the foreign side of a bidirectional MM
         relation, only the first table is used and that must be the table of
         the records on the native side of the relation.

   Scope
         Proc. / Display


.. container:: table-row

   Key
         disallowed

   Datatype
         string

         (list of)

   Description
         *[internal\_type =  **file** ONLY]*

         Default value is '\*' which means that anything file-extension which
         is not allowed is denied.

         If you set this value (to for example "php,php3") AND the "allowed"
         key is an empty string all extensions are permitted  *except* ".php"
         and ".php3" files (works like the [BE][fileExtensions] config option).

         In other words:

         - If you want to permit  *only certain* file-extensions, use 'allowed'
           and not disallowed.

         - If you want to permit  *all file-extensions* except a few, set
           'allowed' to blank ("") and enter the list of denied extensions in
           'disallowed'.

         - If you wish to  *allow all extensions* with no exceptions, set
           'allowed' to '\*' and disallowed to ''

   Scope
         Proc. / Display


.. container:: table-row

   Key
         MM

   Datatype
         string

         (table name)

   Description
         Defines MM relation table to use.

         Means that the relation to the files/db is done with a M-M relation
         through a third "join" table.

         A MM-table must have these four columns:

         - **uid\_local** - for the local uid.

         - **uid\_foreign** - for the foreign uid.If the "internal\_type" is
           "file" then the "uid\_foreign" should be a varchar or 60 or so (for
           the filename) instead of an unsigned integer as you would use for the
           uid.

         - **tablenames** - is required if you use multi-table relations and this
           field must be a varchar of approx. 30In case of files, the tablenames
           field is never used.

         - **sorting** - is a required field used for ordering the items.

         *see ['columns'][fieldname]['config'] / TYPE: "select" => MM for
         additional features.*

   Scope
         Proc.


.. container:: table-row

   Key
         MM\_opposite\_field

   Datatype
         string

         (field name)

   Description
         *see ['columns'][fieldname]['config'] / TYPE: "select" =>
         MM\_opposite\_field*

   Scope
         Proc.


.. container:: table-row

   Key
         MM\_match\_fields

   Datatype
         array

   Description
         *see ['columns'][fieldname]['config'] / TYPE: "select" =>
         MM\_match\_fields*

   Scope


.. container:: table-row

   Key
         MM\_insert\_fields

   Datatype
         array

   Description
         *see ['columns'][fieldname]['config'] / TYPE: "select" =>
         MM\_insert\_fields*

   Scope


.. container:: table-row

   Key
         MM\_table\_where

   Datatype
         string (SQL WHERE)

   Description
         *see ['columns'][fieldname]['config'] / TYPE: "select" =>
         MM\_table\_where*

   Scope


.. container:: table-row

   Key
         MM\_hasUidField

   Datatype
         boolean

   Description
         *see ['columns'][fieldname]['config'] / TYPE: "select" =>
         MM\_hasUidField*

   Scope


.. container:: table-row

   Key
         max\_size

   Datatype
         integer

   Description
         *[internal\_type =  **file** ONLY]*

         Files: Maximum file size allowed in KB

   Scope
         Proc.


.. container:: table-row

   Key
         uploadfolder

   Datatype
         string

   Description
         *[internal\_type =  **file** ONLY]*

         Path to folder under PATH\_site in which the files are stored.

         Example: 'uploads' or 'uploads/pictures'

         **Notice:** TYPO3 does NOT create a reference to the file in its
         original position! It makes a  *copy* of the file into this folder and
         from that moment that file is not supposed to be manipulated from
         outside. Being in the upload folder means that files are understood as
         a part of the database content and should be managed by TYPO3 only.

         **Warning:** do NOT add a trailing slash (/) to the upload folder
         otherwise the full path stored in the references will contain a double
         slash (e.g. “uploads/pictures//stuff.png”).

   Scope
         Proc.


.. container:: table-row

   Key
         prepend\_tname

   Datatype
         boolean

   Description
         *[internal\_type =  **db** ONLY]*

         Will prepend the table name to the stored relations (so instead of
         storing "23" you will store e.g. "tt\_content\_23").

   Scope
         Proc.


.. container:: table-row

   Key
         dontRemapTablesOnCopy

   Datatype
         string

         (list of tables)

   Description
         *[internal\_type =  **db** ONLY]*

         A list of tables which should  *not* be remapped to the new element
         uids if the field holds elements that are copied in the session.

   Scope
         Proc.


.. container:: table-row

   Key
         show\_thumbs

   Datatype
         boolean

   Description
         Show thumbnails for the field in the TCEform

   Scope
         Display


.. container:: table-row

   Key
         size

   Datatype
         integer

   Description
         Height of the selector box in TCEforms.

   Scope
         Display


.. container:: table-row

   Key
         autoSizeMax

   Datatype
         integer

   Description
         If set, then the height of element listing selector box will
         automatically be adjusted to the number of selected elements, however
         never less than "size" and never larger than the integer value of
         "autoSizeMax" itself (takes precedence over "size"). So "autoSizeMax"
         is the maximum height the selector can ever reach.

   Scope
         Display


.. container:: table-row

   Key
         selectedListStyle

   Datatype
         string

   Description
         If set, this will override the default style of element selector box
         (which is “width:200px”).

   Scope
         Display


.. container:: table-row

   Key
         multiple

   Datatype
         boolean

   Description
         Allows the  *same item* more than once in a list.

         If used with bidirectional MM relations it must be set for both the
         native and foreign field configuration. Also, with MM relations in
         general you must use a UID field in the join table, see description
         for “MM”

   Scope
         Display / Proc.


.. container:: table-row

   Key
         maxitems

   Datatype
         integer > 0

   Description
         Maximum number of items in the selector box. (Default = 1)

   Scope
         Display / Proc?


.. container:: table-row

   Key
         minitems

   Datatype
         integer > 0

   Description
         Minimum number of items in the selector box. (Default = 0)

   Scope
         Display / Proc?


.. container:: table-row

   Key
         disable\_controls

   Datatype
         string

   Description
         Disables sub-controls inside "group" control. Comma-separated list of
         values. Possible values are: browser (disables browse button for list
         control), list (disables list and browse button, but not delete
         button), upload (disables upload control) and delete (disables the
         delete button). See example image below.

         **NOTE:** if you use the delete button when the list is disabled,
         **all** entries in the list will be deleted.

         |img-37|

   Scope
         Display / Proc.


.. container:: table-row

   Key
         wizards

   Datatype
         array

   Description
         [See section later for options]

   Scope
         Display


.. container:: table-row

   Key
         appearance

   Datatype
         array

   Description
         Options for refining the appearance of group-type fields.

         - *elementBrowserType* (string) (since TYPO3 CMS 6.0)
           Makes it possible to set an alternative element browser type ("db" or "file")
           than would otherwise be rendered based on the "internal_type" setting.
           This is used internally for :ref:`FAL<t3fal:start>` file fields, where internal_type is "db"
           but the element browser should be the file element browser anyway.

         - *elementBrowserAllowed* (string)  (since TYPO3 CMS 6.0)
           Makes it possible to set an alternative element browser allowed string
           than would otherwise be taken from the "allowed" setting of this field.
           This is used internally for :ref:`FAL<t3fal:start>` file fields,
           where this is used to supply the comma list of allowed file types.

   Scope
         Display


.. ###### END~OF~TABLE ######


.. _columns-group-examples:

Examples
""""""""

.. _columns-group-examples-records:

References to database records
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The "Insert records" content element can be used to reference records
from the "tt\_content" table (and possibly others, like "tt\_news" in
the screenshot below):

|img-35| The corresponding TCA code::

   'records' => array(
           'label' => 'LLL:EXT:cms/locallang_ttc.xml:records',
           'config' => array(
                   'type' => 'group',
                   'internal_type' => 'db',
                   'allowed' => 'tt_content',
                   'size' => '5',
                   'maxitems' => '200',
                   'minitems' => '0',
                   'show_thumbs' => '1',
                   'wizards' => array(
                           'suggest' => array(
                                   'type' => 'suggest',
                           ),
                   ),
           ),
   ),

Note in particular how the "internal\_type" of the group field is set
to "db". Then the allowed tables is defined as "tt\_content" (Content
Elements table). This could very well be a list of tables which means
you can mix references as you like!

The limit is set to a maximum of 200 references and thumbnails should
be displayed, if possible. Finally a suggest wizard is added.

In this case it wouldn't have made sense to use a "select" type field
since the situation implies that records might be found all over the
system in a table which could potentially carry thousands of entries.
In such a case the right thing to do is to use the "group" field so
you have the Element Browser available for selector of the records.


.. _columns-group-examples-page:

Reference to another page
~~~~~~~~~~~~~~~~~~~~~~~~~

You will often see "group" type fields used when a reference to
another page is required. This makes sense since pages can hardly be
presented effectively in a big selector box and thus the Element
Browser that follows the "group" type fields is useful. An example is
the "General Record Storage page" reference:

|img-38| The configuration looks like::

   'storage_pid' => array(
           'exclude' => 1,
           'label' => 'LLL:EXT:lang/locallang_tca.php:storage_pid',
           'config' => array(
                   'type' => 'group',
                   'internal_type' => 'db',
                   'allowed' => 'pages',
                   'size' => '1',
                   'maxitems' => '1',
                   'minitems' => '0',
                   'show_thumbs' => '1',
                   'wizards' => array(
                           'suggest' => array(
                                   'type' => 'suggest',
                           ),
                   ),
           ),
   ),

Notice how "maxitems" is used to ensure that only one relation is
created despite the ability of the "group" type field to create
multiple references.


.. _columns-group-examples-images:

Attaching images
~~~~~~~~~~~~~~~~

Attaching files to a database record is also achieved with group-type
fields:

|img-36| Notice how all the image names end with "\_0" and some number. This
happens because all files attached to records through a group-type
field are copied to a location defined by the "uploadfolder" setting
in the configuration (see below). When a file is referenced several
times, it is also copied several times. TYPO3 automatically appends a
number so that each reference is unique. ::

   'image' => array(
           'label' => 'LLL:EXT:lang/locallang_general.xml:LGL.images',
           'config' => array(
                   'type' => 'group',
                   'internal_type' => 'file',
                   'allowed' => $GLOBALS['TYPO3_CONF_VARS']['GFX']['imagefile_ext'],
                   'max_size' => $GLOBALS['TYPO3_CONF_VARS']['BE']['maxFileSize'],
                   'uploadfolder' => 'uploads/pics',
                   'show_thumbs' => '1',
                   'size' => '3',
                   'maxitems' => '200',
                   'minitems' => '0',
                   'autoSizeMax' => 40,
           ),
   ),

Notice how the "group" type is defined to contain files. Next the list
of allowed file extensions are defined (here, taking the default list
of image types for TYPO3). A maximum size (in kilobytes) for files is
also defined. The "uploadfolder" property indicates that all files
will be copied to the "uploads/pics" folder. Notice that this path is
relative to the PATH\_site of TYPO3, one directory below PATH\_typo3.


.. _columns-group-data:

Data format of "group" elements
"""""""""""""""""""""""""""""""

Since the "group" element allows to store references to multiple
elements we might want to look at how these references are stored
internally.


.. _columns-group-data-storage:

Storage methods
~~~~~~~~~~~~~~~

There are two main methods for this:

- Stored in a comma list

- Stored with a join table (MM relation)

The default and most wide spread method is the comma list.


.. _columns-group-data-reserved:

Reserved tokens
~~~~~~~~~~~~~~~

In the comma list the token "," is used to separate the values. In
addition the pipe sign "\|" is used to separate value from label value
when delivered to the interface. Therefore these tokens are not
allowed in reference values, not even if the MM method is used.


.. _columns-group-data-commalist:

The "Comma list" method (default)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When storing references as a comma list the values are simply stored
one after another, separated by a comma in between (with no space
around!). The database field type is normally a varchar, text or blob
field in order to handle this.

From the examples above the four Content Elements will be stored as
"26,45,49,1" which is the UID values of the records. The images will
be stored as their filenames in a list like "DSC\_7102\_background.jpg
,DSC\_7181.jpg,DSC\_7102\_background\_01.jpg".

Since "db" references can be stored for multiple tables the rule is
that uid numbers  *without* a table name prefixed are implicitly from
the first table in the allowed table list! Thus the list "26,45,49,1"
is implicitly understood as
"tt\_content\_26,tt\_content\_45,tt\_content\_49,tt\_content\_1". That
would be equally good for storage, but by default the "default" table
name is not prefixed in the stored string. As an example, lets say you
wanted a relation to a Content Element and a Page in the same list.
That would look like "tt\_content\_26,pages\_123" or alternatively
"26,pages\_123" where "26" implicitly points to a "tt\_content" record
given that the list of allowed tables were "tt\_content,pages".


.. _columns-group-data-mm:

The "MM" method
~~~~~~~~~~~~~~~

Using the MM method you have to create a new database table which you
configure with the key "MM". The table must contain a field,
"uid\_local" which contains the reference to the uid of the record
that contains the list of elements (the one you are editing). The
"uid\_foreign" field contains the uid of the reference record you are
referring to. In addition a "tablename" and "sorting" field exists if
there are references to more than one table.

Lets take the examples from before and see how they would be stored in
an MM table:


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   uid\_local
         uid\_local

   uid\_foreign
         uid\_foreign

   tablename
         tablename

   sorting
         sorting


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         26

   tablename
         tt\_content

   sorting
         1


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         45

   tablename
         tt\_content

   sorting
         2


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         49

   tablename
         tt\_content

   sorting
         3


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         1

   tablename
         tt\_content

   sorting
         4


.. ###### END~OF~TABLE ######


Or for "tt\_content\_26,pages\_123":


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   uid\_local
         uid\_local

   uid\_foreign
         uid\_foreign

   tablename
         tablename

   sorting
         sorting


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         26

   tablename
         tt\_content

   sorting
         1


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         123

   tablename
         pages

   sorting
         2


.. ###### END~OF~TABLE ######


Or for "DSC\_7102\_background.jpg,DSC\_7181.jpg,DSC\_7102\_background\
_01.jpg":


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   uid\_local
         uid\_local

   uid\_foreign
         uid\_foreign

   tablename
         tablename

   sorting
         sorting


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         DSC\_7102\_background.jpg

   tablename
         N/A

   sorting
         1


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         DSC\_7181.jpg

   tablename
         N/A

   sorting
         2


.. container:: table-row

   uid\_local
         [uid of the record you are editing]

   uid\_foreign
         DSC\_7102\_background\_01.jpg

   tablename
         N/A

   sorting
         3


.. ###### END~OF~TABLE ######


.. _columns-group-data-api:

API for getting the reference list
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In t3lib/ the class "t3lib\_loaddbgroup" is designed to transform the
stored reference list values into an array where all uids are paired
with the right table name. Also, this class will automatically
retrieve the list of MM relations. In other words, it provides an API
for getting the references from "group" elements into a PHP array
regardless of storage method.


.. _columns-group-data-tceforms:

Passing the list of references to TCEforms
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Regardless of storage method, the reference list has to be "enriched"
with proper title values when given to TCEforms for rendering. In
particular this is important for database records. Passing the list
"26,45,49,1" will not give TCEforms a chance to render the titles of
the records.

The t3lib/ class "t3lib\_transferdata" is doing such transformations
(among other things) and this is how the transformation happens:


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Int. type
         Int. type:

   In Database
         In Database:

   When given to TCEforms
         When given to TCEforms:


.. container:: table-row

   Int. type
         "db"

   In Database
         26,45,49,1

   When given to TCEforms
         tt\_content\_26\|%20adfs%20asdf%20asdf%20,tt\_content\_45\|This%20is%2
         0a%20test%20%28copy%203%29,tt\_content\_49\|%5B...%5D,tt\_content\_1\|
         %5B...%5D


.. container:: table-row

   Int. type
         "file"

   In Database
         DSC\_7102\_background.jpg,DSC\_7181.jpg,DSC\_7102\_background\_01.jpg

   When given to TCEforms
         DSC\_7102\_background.jpg\|DSC\_7102\_background.jpg,DSC\_7181.jpg\|DS
         C\_7181.jpg,DSC\_7102\_background\_01.jpg\|DSC\_7102\_background\_01.j
         pg


.. ###### END~OF~TABLE ######


The syntax is::

   [ref. value]|[ref. label rawurlencoded],[ref. value]|[ref. label rawurlencoded],....

Values are transferred back to the database as a comma separated list
of values without the labels but if labels are in the value they are
automatically removed.

Alternatively you can also submit each value as an item in an array;
TCEmain will detect an array of values and implode it internally to a
comma list. (This is used for the "select" type, in renderMode
"singlebox" and "checkbox").


.. _columns-group-data-files:

Managing file references
~~~~~~~~~~~~~~~~~~~~~~~~

When a new file is attached to a record the TCE will detect the new
file based on whether it has a path prefixed or not. New files are
copied into the upload folder that has been configured and the final
value list going into the database will contain the new filename of
the copy.

If images are removed from the list that is detected by simply
comparing the original file list with the one submitted. Any files not
listed anymore are deleted.

Examples:


.. ### BEGIN~OF~TABLE ###

.. container:: table-row

   Current DB value
         Current DB value

   Submitted data from TCEforms
         Submitted data from TCEforms

   New DB value
         New DB value

   Processing done
         Processing done


.. container:: table-row

   Current DB value
         first.jpg,second.jpg

   Submitted data from TCEforms
         first.jpg,/www/typo3/fileadmin/newfile.jpg,second.jpg

   New DB value
         first.jpg,newfile\_01.jpg,second.jpg

   Processing done
         /www/typo3/fileadmin/newfile.jpg was copied to "uploads/[some-
         dir]/newfile\_01.jpg". The filename was appended with "\_01" because
         another file with the name "newfile.jpg" already existed in the
         location.


.. container:: table-row

   Current DB value
         first.jpg,second.jpg

   Submitted data from TCEforms
         first.jpg

   New DB value
         first.jpg

   Processing done
         "uploads/[some-dir]/second.jpg" was deleted from the location.


.. ###### END~OF~TABLE ######
