# eanubis

sourcecode below
p.s. make sure you use a gmail account when asked

```
#Persistent

; FUNCS()

xString(charlim) {
cl1 = a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z,0,1,2,3,4,5,6,7,8,9
Sort, cl1, Random D,
azstring:=RegExReplace(cl1, ",")
StringLeft, azstring, azstring, %charlim%
return %azstring%
}

; HOTKEY

CleanAndRun() {
FileDelete, %A_AppData%\Origin\local.xml
RegRead, REG_ORIGIN, HKEY_CLASSES_ROOT, origin\shell\open\command
Run, %REG_ORIGIN%
return
}

WriteThatIni(V,K,S) {
IniWrite, %V%, settings.ini, %S%, %K%
return
}

CheckSettings(pVar) {
	if FileExist("settings.ini") {
		IniRead, sumVar, settings.ini, Settings, %pVar%, ERROR
		if (sumVar == "ERROR") || (StrLen(sumVar) == 0) {
			GetDatPrompt()
		}
	}
	else {
		GetDatPrompt()
	}
return
}

GetDatPrompt() {
InputBox, myNAME, EAnubis, Enter the first part of your email address.`nFor example if your email was Anubis@email.com you would now write Anubis
InputBox, myDOMAIN, EAnubis, Enter the second part of your email address`nFor example if your email was Anubis@email.com you would now write email.com
InputBox, NickN, EAnubis, Enter a username you like.`n Don't worry we will randomize it a little >:D
;InputBox, Pwd, EAnubis, Enter a password to login into your fresh account`nAll info is store safely into your PC but not encrypted

WriteThatIni(myNAME,"User","Settings")
WriteThatIni(myDomain,"Domain","Settings")
WriteThatIni(NickN,"Nickname","Settings")
;WriteThatIni(Pwd,"Password","Settings")
return
}


F1::
CheckSettings("User")
BlockInput, on
CleanAndRun()
WinWaitActive, Origin,,5
if ErrorLevel {
	BlockInput, off
	MsgBox, Error
	return
}
else {
	Sleep 1000
	IniRead, NickN, settings.ini, Settings, Nickname, ERROR
	IniRead, myNAME, settings.ini, Settings, User, ERROR
	IniRead, myDOMAIN, settings.ini, Settings, Domain, ERROR
	;IniRead, myPWD, settings.ini, Settings, Password, ERROR
	myRNDM := xString(3)
	myPOSTFIX := xString(2)
	myPWD1 := xString(3)
	myPWD2 := xString(3)1337
	StringUpper, myPWD1, myPWD1
	StringLower, myPWD2, myPWD2
	myPWD := myPWD1 . myPWD2
	WriteThatIni(myPWD,"Password","Settings")
	; Nightmare mode begins
	SendInput +{TAB}
	Sleep 50
	Send {Enter}
	Sleep 1000
	SendInput {TAB}{TAB}{TAB}{TAB}
	Sleep 50
	SendInput {Down}
	Sleep 50
	SendInput {TAB}
	Sleep 50
	SendInput {Down}
	Sleep 50
	SendInput {Tab}
	SendInput {Numpad1}{Numpad9}{Numpad6}{Numpad6}
	SendInput {Tab}{Space}
	SendInput {Tab}{Tab}{Tab}{Enter}
	Sleep 500
	SendInput {Tab}
	Sleep 100
	SendInput %myNAME%{+}%myRNDM%{@}%myDOMAIN%
	Sleep 200
	SendInput {Tab}
	SendInput %myPWD%
	Sleep 200
	SendInput {Tab}
	SendInput %NickN%%myPOSTFIX%
	SendInput {Tab}{Tab}{Tab}
	SendInput {Enter}
	Sleep 500
	SendInput {Tab}
	Sleep 50
	SendInput {Down}
	SendInput {Tab}
	SendInput whatever
	SendInput {Tab}
	SendInput {Down}{Down}
	SendInput {Tab}{Tab}
	SendInput {Space}
	SendInput {Tab}
	SendInput {Enter}
	BlockInput, off
	Sleep 100
	MsgBox, 48,EAnubis, Your password is stored in the settings.ini file in the same folder as this .exe - btw it's %myPWD%
	Exitapp
	return
}
return
```
