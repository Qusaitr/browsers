(
echo @echo off
echo echo Merging part_*.bin into ms-playwright.zip...
echo powershell -Command "$out=[IO.File]::Create('ms-playwright.zip'); Get-ChildItem 'part_*.bin' | Sort-Object { [int]($_.BaseName -replace 'part_','') } | ForEach-Object { $bytes=[IO.File]::ReadAllBytes($_.FullName); $out.Write($bytes,0,$bytes.Length) }; $out.Close()"
echo echo Extracting ms-playwright.zip...
echo powershell -Command "Expand-Archive -Path 'ms-playwright.zip' -DestinationPath '.' -Force"
echo echo Cleaning up temporary files...
echo del /f /q part_*.bin ms-playwright.zip
echo echo Done! ms-playwright folder is ready.
echo pause
) > extract_browsers.bat
