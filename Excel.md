[Copy your macros to a Personal Macro Workbook]
This way each time you open Excel you will have your Macro

1. Open Excel
2. Click on the ribbon, more commands
3. Go to Customize ribbon on the left
4. Check Developer on the right, click OK

5. Developer > Record Macro (Store macro in: Personal Macro Workbook), click OK
6. Stop recording Macro
7. Developer > Macros > select Macro > Options
8. Set ctrl+e to it, click ok
9. Still in the Macros window, select Macro > Edit
10. Delete all and paste the following
Sub SaveWorkbookAsPDF()
  wbPath = ActiveWorkbook.Path + "\"
  wbName = Left(ActiveWorkbook.Name, InStr(ActiveWorkbook.Name, ".") - 1)

  ActiveWorkbook.ExportAsFixedFormat _
    Type:=xlTypePDF, _
    Filename:=wbPath + wbName + ".pdf", _
    Quality:=xlQualityStandard, _
    IncludeDocProperties:=True, _
    IgnorePrintAreas:=False, _
    OpenAfterPublish:=True
End Sub
11. Close VBA
12. In the PERSONAL excel, View > Hide

Now, every time you open an excel, PERSONAL will also open in hidden mode, allowing you to CTRL+E and export your "Print area" to .pdf


> Where does the PERSONAL.xlsb lurk?
[en-us] -> C:\Users\%username%\AppData\Local\Microsoft\Excel\XLStart
[pt-br] -> C:\Users\%username%\AppData\Roaming\Microsoft\Excel\XLINÍCIO 

> Has it suddenly stopped working?
Sometimes a Personal workbook gets disabled.
Try this in Office 2016;
File>> Options>> Add-ins
Go to manage (bottom of box) and choose Disabled Items
If your personal.xlsb file is in the list, select it and click on the enable button
Restart Excel



------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

> ENCODING UTF-8

I answered a similar question at Default character encoding for Excel Text Wizard?.

I found my answer at Changing default text import origin type in Excel.

Close Excel, if it is open.
Open the Registry Editor.
Navigate to HKEY_CURRENT_USER → Software → Microsoft → Office → ▒▒ → Excel → Options, where ▒▒ is your version of Office, mostly likely the largest number you see there.
Right-click an empty space on the right side and select New → DWORD.
Name the item DefaultCPG, and press Enter to save.
Right-click on DefaultCPG and select Modify.
Set the Base to Decimal.
For Value data, enter 65001 to set your default to UTF-8. For some other encoding, use the code page identifier, which you can find in the Text Import Wizard in Excel or in this list.
Click OK.
Like Vasille says in the comment to this question, if your file is not actually in UTF-8 format, you may technically want to convert the characters within the file to the encoding you want before opening in Excel. For my purposes, though, UTF-8 does a good enough job of displaying non-corrupted characters.

Not working? Make sure you set Base to Decimal (Step 7).
<https://superuser.com/questions/911369/excel-change-default-encoding-file-origin-of-text-import-wizard-to-utf-8-650#:~:text=Open%20the%20Registry%20Editor.,and%20press%20Enter%20to%20save.>