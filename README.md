# Useful E-Prime Script

|         |                           |
| ------- | ------------------------- |
| Title   | Useful E-Prime Script    |
| Version | 5<sup>th</sup> June, 2023 |

</br>
</br>

A summery regarding E-Prime script.

</br>

## Set random interval

</br>

*In designing experiments, to avoid the influence of irrelevant variables caused by subject expectancy effects, it is necessary to randomize the presentation time of masked stimuli.*

</br>

**Method 1**

```visual basic
Object.duration = Random (200,600) 
```

</br>

**Method 2**

```visual basic
Object.duration = 2 * Random (100,300) 
```

</br>

## Have a rest during full session
</br>

*To avoid the fatigue effect caused by long-term experiments, it is necessary to set rest intervals between trials.*

</br>

Define E-Prime User Script 

```visual basic
Dim N as Integer
```

</br>

**Method 1**

```visual basic
c.GetAttrib (“ListName.sample”) 
if N mod 40 = 0 Then 
    msgbox (“It’s time to rest ! “Press SPACE to continue”)
End If
```
</br>

**Method 2**

```visual basic
N=N+1
If N Mod 40 = 0 Then
	GoTo label1
Else
	GoTo label2
End If
```

</br>

## Practice or real session
</br>

*Choose between practice and formal testing, it can be automatic (based on accuracy) or manual (based on selection).*

</br>


**Method 1**

```visual basic
If Object.RESP= 1 Then Goto Label1
Else
Goto Label2
End If
```
</br>

**Method 2**

Define E-Prime User Script 

</br>

```visual basic
Public N as Integer
```

</br>

```visual basic
If Object.ACC=1 Then
    N = N+1
End If
```
</br>

```visual basic
If (N/PracticeList.Size)<0.80 Then 
    N=0
GoTo label3 
Else
GoTo label4
End If 
```

</br>

## Open port

</br>

**Method 1**

Experiment properties - Devices add Parallel Port

</br>

**Method 2**


```visual basic
Object.OnsetSignalEnabled = True 
Object.OnsetSignalPort = &H0378
'Open Port
Object.OffsetSignalEnabled = True 
Object.OnsetSignalPort = &H0378
'Close Port
```


</br>

## Stimulus marker

</br>

**Parallel Port**

```visual basic
WritePort &H0378, 0
Object.OnsetSignalData = c.GetAttrib ("Code")
```

</br>

**Serial Port**

```visual basic
Object.Tasks.Reset If 
    Serial.GetState() = ebStateOpen Then
Object.Tasks.Add Serial.CreateTask ("Object.OnsetTime", 0, "WriteByte", "(custom)", c.GetAttrib("Mark"), "Byte", True)
End If

If Serial.GetState() = ebStateOpen Then
    Object.Tasks.Add Serial.CreateTask ("Object.OnsetTime", 10, "WriteByte", "(custom)", ebDigit_0, "Byte", True)
End If

```

</br>

**Socket Port**

```visual basic
Object.Tasks.Reset

Object.Tasks.Add Socket.CreateTask("Object.OnsetTime", 0, "WriteByte", "(custom)", c.GetAttrib("Code"), "Byte", True)
```

</br>

## Response marker

</br>

**Parallel Port**

```visual basic
If Object.Acc = 1 then 
    WritePort &H0378,77
Else If Object.Acc = 0 then 
        WritePort &H0378,88
else
        WritePort &H378,99
    End If
End If
```

</br>

**Serial Port**

Experiment properties - Devices add Parallel Port

</br>

```visual basic
Const sleeptime As Integer = 5
```



```visual basic
If target.acc=1 Then 
    Serial.WriteByte 77
Else Serial.WriteByte 88
End If 

Sleep(sleeptime)
Serial.WriteByte 0
```

</br>

**Socket Port**

Define E-Prime User Script 

</br>

```visual basic
Const sleeptime As Integer = 5
```



```visual basic
If target.acc=1 Then 
    Socket.WriteByte 77
Else Socket.WriteByte 88
End If 

Sleep(sleeptime)
Socket.WriteByte 0
```

</br>

## Others

</br>

**Custom response in a TextDisplay Object**

</br>

```visual basic
If Object.ACC = 1 Then

	Feedback.Text ="Correct!" 
	Feedback.ForeColor = Color("Blue")
    	Feedback.FontSize = 28

Else
	Feedback.Text ="Wrong!" 
	Feedback.ForeColor = Color("DarkRed")
    	Feedback.FontSize = 28

End If

```
</br>
For the color code pleae refer to https://shorturl.at/eiPS2 (PST support site) for reference.

</br>
</br>

# E-Prime online resource

</br>

E-Prime Command Reference  https://pstnet.com/ecr/

PST support service https://support.pstnet.com/hc/en-us

PST YouTube Channel https://www.youtube.com/@PSTNET

E-Prime Google Group https://groups.google.com/g/e-prime


</br>

**[TBC]**
