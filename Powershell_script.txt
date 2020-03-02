# Started By: Sameera Kalgudi
# Updated By: Sameera Kalgudi
$p = " - "
$p1 = "min:"
#iterating through each line
foreach($line in Get-Content -Path "C:\Users\Samee\Desktop\GlassDoor\config.yaml") {
	#matching multiple patterns
	Switch ($line )
	{	   {$_ -match 'search-app:'} {
				exit
			}
		   {$_ -match $p} {
				Write-Host("----------------------")
				$allhosts = $line.split(' ')[-1]
				Write-Host($allhosts)
				
			}
		   {$_ -match $p1} {
			Write-Host("Replacing {threads.min} in server.xml with value from config.yaml")
			$min = $line.split(' ')[-1]
			$min = "'$min'"
			$temp = Get-Content .\server.xml
			$temp.replace('"${threads.min}"', $min) | set-content .\server.xml -force
			Write-Host("Printing all the hosts")
			$p1 = "----"
		   }
		   
}
}



