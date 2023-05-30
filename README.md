# Useful E-Prime Script



## Set random interval



**Way 1**

```visual basic
Object.duration = Random (200,600) 
```



**Way 2**

```visual basic
Object.duration = 2 * Random (100,300) 
```



## Have a rest



Define E-Prime User Script 

```visual basic
Dim N as Integer
```



**Way 1**

```visual basic
c.GetAttrib (“ListName.sample”) 
if N mod 40 = 0 Then 
    msgbox (“It’s time to rest ! “Press SPACE to continue”)
End If
```



**Way 2**

```visual basic
N=N+1
If N Mod 40 = 0 Then
	GoTo label1
Else
	GoTo label2
End If
```



## Practice or real session



**Way 1**

```visual basic
If Object.RESP= 1 Then Goto Label1
Else
Goto Label2
End If
```



**Way 2**

Define E-Prime User Script 

```visual basic
Public N as Integer
```



```visual basic
If Object.ACC=1 Then
    N = N+1
End If
```



```visual basic
If (N/PracticeList.Size)<0.80 Then 
    N=0
GoTo label3 
Else
GoTo label4
End If 
```



## Open port



**Way 1**

Experiment properties - Devices add Parallel Port



**Way 2**



```visual basic
Object.OnsetSignalEnabled = True 
Object.OnsetSignalPort = &H0378
'Open Port
Object.OffsetSignalEnabled = True 
Object.OnsetSignalPort = &H0378
'Close Port
```



## Stim marker



**Parallel Port**

```visual basic
If Object.Acc = 1 then 
    WritePort &H0378,7
Else If Object.Acc = 0 then 
        WritePort &H378,8
    Else
        WritePort &H378,9
	End If
End If
```



**Serial Port**

```visual basic
If target.acc=1 Then 
    Serial.WriteByte 7
Else Serial.WriteByte 8
End If 

Sleep(sleeptime)
Serial.WriteByte 0
```



**Socket Port**

```visual basic
Object.Tasks.Reset

Object.Tasks.Add Socket.CreateTask("Object.OnsetTime", 0, "WriteByte", "(custom)", c.GetAttrib("Code"), "Byte", True)
```



## Resp marker



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



**Serial Port**

Experiment properties - Devices add Parallel Port

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



**Socket Port**

Define E-Prime User Script 

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



## Others



**Custom response in a TextDisplay Object**



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

'For the color code pleae refer to https://shorturl.at/eiPS2
```

