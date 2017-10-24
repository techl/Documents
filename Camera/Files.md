# Camera Files

# Exif Tag

- 0x882a Time zone

## ExifTool

http://www.sno.phy.queensu.ca/~phil/exiftool/

시간 단위로 변경할 경우

> exiftool -AllDates-=9 FolderName

연도부터 초까지 원하는 값으로 시간을 더하거나 뺄 수 있다.

> exiftool "-DateTimeOriginal-=0:0:0 9:0:0" FolderName