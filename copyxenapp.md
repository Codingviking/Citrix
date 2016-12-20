# Citrix
#Copy xenapp applications to another delivery group with renaming

#Trying to do something like below but can't get it right
# The idea is to read in Citrix applications then modified some of the data
# eventually I would use the info to create new applications in another delivery group

Add-PSSnapin Citrix.*
$apps = Get-BrokerApplication | Where-Object {($_.AssociatedDesktopGroupUids -eq "1") -and ($_.name -eq "TESTAPP") } 
$apps

foreach ($app in $apps) {

                        $modifiedapps = @{
                            $app.BrowserName = "Beta " + $app.BrowserName
                            $app.Name = "Beta " + $app.Name
                            $app.PublishedName = "Beta " + $app.PublishedName
                            $app.ClientFolder = "\Beta"
                            $app.AssociatedDesktopGroupUids = "5"
                            $app.AssociatedUserFullNames = {user}
                            $app.AssociatedUserNames = {domain\user}
                            $app.AssociatedUserUPNs = {user@FQDN}
                            $app.Description = ""
                            $results += New-Object psobject -Property $modifiedapps
                                        }
                        }
