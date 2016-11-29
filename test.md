#Test

```powershell
$text =  [System.IO.File]::OpenText("C:\Users\NAME\Downloads\original_msg.txt").ReadToEnd()Select-String -Path "C:\Users\NAME\Downloads\original_msg.txt" -pattern "Received: from kulguger.com"
Function Process-ReceivedFrom{  Param($text)  $regexFrom1 = ‘Received: from([\s\S]*?)by([\s\S]*?)with([\s\S]*?);([(\s\S)*]{32,36})(?:\s\S*?)’  $fromMatches = $text | Select-String -Pattern $regexFrom1 -AllMatches
  
    Function Clean-String  {    Param([string]$inputString)      $inputString = $inputString.Trim()    $inputString = $inputString.Replace("rn","")      $inputString = $inputString.Replace("t"," ")      $inputString  } 
     if ($fromMatches)  {
    $rfArray = @()
    $fromMatches.Matches | foreach{
      $from = Clean-string $_.groups[1].value
      $by = Clean-string $_.groups[2].value
      $with = Clean-string $_.groups[3].value
      Switch -wildcard ($with)
      {
        “SMTP*” {$with = “SMTP”}
        “ESMTP*” {$with = “ESMTP”}
        default{}
      }
      $time = Clean-string $_.groups[4].value
      $fromhash = @{
        ReceivedFromFrom = $from
        ReceivedFromBy = $by
        ReceivedFromWith = $with
        ReceivedFromTime = [Datetime]$time
      }                      
      $fromArray = New-Object -TypeName PSObject -Property $fromhash                  
      $rfArray += $fromArray            
    }
    $rfArray
  }
  else
  {
    return $null
  }
}
```
